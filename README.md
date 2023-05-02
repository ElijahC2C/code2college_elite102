import mysql.connector
username = 0
bank_name = 0
temp = 0
user_list = []
password_list = []
amount_list = []


def sql_info():
    connection = mysql.connector.connect(user = 'root', database = 'the_thing', password = 'S00perm@n')
    cursor = connection.cursor()
    testQuery = ('SELECT * FROM bank')
    cursor.execute(testQuery)
    
    for item in cursor:
        user_list.append(item)
        if(username == str(user_list[1])):
            print("Welcome! Here are your current account details.")
            print("\n\n")
            for item in cursor:
                print(item)
            print("\n\n")
        else:
            print("**not here")
    cursor.close()
    connection.close()
def add():
    connection = mysql.connector.connect(user = 'root', database = 'the_thing', password = 'S00perm@n')
    cursor = connection.cursor()
    alteration = ("INSERT INTO `the_thing`.`bank` (`int`, `name`, `password`, `amount`) VALUES ('4', 'name_to_be_added', 'password_to_be_added', 'amount_to_be_added'); ")
    cursor.execute(alteration)
    cursor.close()
    connection.close()

selection = int(input("Welcome to the bank!\n\nWhat would you like to do?\n\n1.Check your account\n2.Create a new account\n3.Close an account\n4.Modify an existing account\n5.End\n"))
while(selection != 5):
    if(selection == 1):
        username = str(input("Please enter the name your account is under: "))
        for i in range(len(user_list)):
            if(username == user_list[i]):
                entered_password = str(input("What is the password of that account"))
                for n in range(len(password_list)):
                    if(entered_password == password_list[n]):
                        print("Account info\n")
                        print("Name: " + str(user_list[i]))
                        print("Password: " + str(password_list[i]))
                        print("Balance: " + str(amount_list[i]))

        #sql_info()
    if(selection == 2):
        name_to_be_added = str(input("What would you like to call your account?\n"))
        user_list.append(name_to_be_added)
        password_to_be_added = str(input("What would you like your password to be?\n"))
        password_list.append(password_to_be_added)
        amount_to_be_added = str(input("How much would you like to make for your inital deposit?\n"))
        amount_list.append(amount_to_be_added)
    #add()
    #somehow sync all of these together to mysql
        print("New account added: " + str(user_list[0]))
        print("New password added: " + str(password_list[0]))
        print("Amount added: " + str(amount_list[0]))
        print("Your account has been added!\n")
    if(selection == 3):
        #sql_info()
        name_to_be_deleted = str(input("What is the name of the account you want to be deleted?\n"))
        for i in range(len(user_list)):
            if(name_to_be_deleted == user_list[i]):
                user_list.remove(name_to_be_deleted)
                entered_password = str(input("What is the password of that account"))
                for n in range(len(password_list)):
                    if(entered_password == password_list[n]):
                        password_list.remove(entered_password)
    #if(entered_password == password_list[i]#make a def func for i):
    #delete from the database
        print("Your account has been deleted")
    if(selection == 4):
        #sql_info()
        account_to_be_modded = str(input("What is the name of the account that you would like to modify?\n"))
        for i in range(len(user_list)):
            if(account_to_be_modded == user_list[i]):
                #temp = i
                alter = int(input("What would you like to do to the account?\n\n1.Change the name\n2.Change the password\n3.Change amount"))
                if(alter == 1):
                    name_to_be_modded = str(input("What do you want to change the name to? "))
                    user_list[i] = name_to_be_modded
                    print("Name changed to " + str(name_to_be_modded))
                if(alter == 2):
                    password_to_be_modded = str(input("What do you want to change the name to? "))
                    password_list[i] = password_to_be_modded
                    print("Password changed to " + str(password_to_be_modded))
                if(alter == 3):
                    amount_to_be_modded = str(input("What do you want to change the name to? "))
                    amount_list[i] = amount_to_be_modded
                    print("Amount changed to " + str(amount_to_be_modded))
    selection = int(input("Welcome to the bank!\n\nWhat would you like to do?\n\n1.Check your account\n2.Create a new account\n3.Close an account\n4.Modify an existing account\n5.End\n"))
