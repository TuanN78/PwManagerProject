# PwManagerProject
test

def encrypt(data, shift):
    encrypted = ""
    for i in range(len(data)):
        char = data [i]
        if(char.isupper()):
            encrypted += chr((ord(char) + shift - 65) %26 + 65)
        elif(char.islower()):
            encrypted += chr((ord(char) + shift - 97) %26 +65)
        elif(char.isdigit()):
            number = int(char) + shift % 10
            encrypted += str(number)
        else:
            encrypted += char
    return encrypted
# test
def decrypt(data, shift):
    decrypted = ""
    for i in range(len(data)):
        char = data [i]
        if(char.isupper()):
            decrypted += chr((ord(char) - shift - 65) %26 + 65)
        elif(char.islower()):
            decrypted += chr((ord(char) - shift - 97) %26 +65)
        elif(char.isdigit()):
            number = int(char) - shift % 10
            decrypted += str(number)
        else:
            decrypted += char
    return decrypted


menu = " "
while menu != '1' or menu != '2':
    menu = input("Would you like to save a new password or view your old ones? "
                 "\n1. Input new password: "
                 "\n2. View passwords "
                 "\n3. Exit "
                 "\n:")
    
    if menu == '1': 
        appName = input("Enter the name of the app you are using: ")
        username = input("Enter your username for the app: ")
        password = input("Enter your password for the app: ")
        shift = 25
        file = open("myPasswords.txt", "a")
        file.write(encrypt(appName, shift) + ";|" + encrypt(username, shift) + ";|" + encrypt(password, shift) + "\n")
        file.close
    
    if menu == '2':
        print("App\tUsername\tPassword")
        file = open("mypasswords.txt", "r")
        for i in file:
            shift = 25
            data = i.split(";|")
            print(decrypt(data[0], shift) + "\t" + decrypt(data[1], shift) + "\t\t" + decrypt(data[2], shift))
        
    if menu == '3':
        exit()
    

