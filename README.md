information = ["Name","Age","Nationality"]
def infor():
    information = []
    while True:
        in4 = input("Type of information you want: ")
        if in4 == "done":
            break
        else:
            information.append(in4)
    return information
def add():
    while True:
        try:
            time = int(input("How many times do you want to enter: "))
            break
        except:
            print("Only number")
    a = []
    z = ""
    for i in range(time):
        for j in range(len(information)):
            x = input(information[j] + ": ")
            y = information[j] + ": " + x + ". "
            z = z + y
        a.append(z)
        z = ""
    return a
def scan(a):
    for i in range(len(a)):
        print(a[i])

add_request = False
add_request2 = False
add_key = False
search_request = False
write_request = False
begin = True

while begin:
    request = input("\nwhat do you want to do? add or search?('done' to close): ")
    if request == "add":
        add_request = True
    elif request == "search":
        search_request = True
    elif request == "done":
        begin = False
        add_request = False
        search_request = False
    else:
        print("Your request is not valid")

    while add_request:
        while True:
            information_key = input("The form of information is" + str(information) +" do you want to change it?(yes/no): ")
            if information_key == "yes":
                information = infor()
                break
            elif information_key == "no":
                break
            else:
                print("Your request is not valid")
        student = add()
        while True:
            check = input("All of informations are corrected???(yes/no): ")
            if check == "yes":
                add_key = True
                add_request2 = True
                break
            elif check == "no":
                break
            else:
                print("your request is not valid")
        while add_key:
            add_check = input("\ndo you want to add this into .txt file???(yes or no): ")
            if add_check == "yes":
                while True:
                    txt_file = input("Txt file' name: ")
                    try:
                        file = open(txt_file + ".txt", "r")
                        file.close()
                        file = open(txt_file + ".txt", "a")
                        break
                    except:
                        ask = input("there no file " + txt_file +" Do you want creat a new file?(yes/no)")
                        if ask == "yes":
                            file = open(txt_file + ".txt","a")
                            break
                        elif ask == "no":
                            pass
                        else:
                            print("Your request is not valid")
                for i in range(len(student)):
                    for j in range(len(student[i])):
                        file.write(student[i][j])
                    file.write("\n")
                file.close()
                add_key = False
            elif add_check == "no":
                add_key = False
            else:
                print("Your request is not valid")
        if add_request2:
            add_request = False
            add_request2 = False

    if search_request:
        while True:
            txt_file = input("Txt file' name: ")
            try:
                file = open(txt_file + ".txt", "r")
                output_list = file.readlines()
                file.close()
                break
            except:
                print("there no file : " + txt_file)

        scan_list = []
        search = input("""\nWhat do you want to see 
Enter 'all' to see all of information or person's name to see only that person's information: """)

        if search == "all":
            scan(output_list)
        else:
            for i in range(len(output_list)):
                if search in output_list[i]:
                   scan_list.append(output_list[i])
            if len(scan_list) > 0:
                scan(scan_list)
            else:
                print("There is no information likes " + search)

        search_request = False
