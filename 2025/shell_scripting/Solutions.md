#!/bin/bash
if [[ $# == 0 ]];
then
echo "Please specify what to do using the script $0"
echo -e "For Help or Usage Info use any:\t $0 -h or $0 --help"
exit
fi
<<AccountCreation
1. Create a new username and password
AccountCreation

Create_User() {
read -p "Enter username: " username

count=$(cat /etc/passwd | grep "$username" |wc | awk '{print $1}')
if [ $count != 0 ];
then
        echo "User already exists"
        exit
fi

echo "New User"
read -p "Enter password: " password

if sudo useradd -m "$username";
then
    echo "$username:$password" | sudo chpasswd
    echo "User $username has been created successfully."
fi

count=$(cat /etc/passwd | grep "$username" |wc | awk '{print $1}')

if [ $count == 1 ]
then
        echo "============Creation of new user completed========"
exit
fi
}

#::::::::::::::::::::::::::::Condition for the argument of the script:::::::::::::::::::::::::::
if [[ $1 == -c || $1 == --create ]]
then
        Create_User
fi


<<AccountDeletion
1. Delete an existing user account
AccountDeletion

Delete_User() {
read -p "Enter the username: " username

count=$(cat /etc/passwd | grep "$username" |wc | awk '{print $1}')
if [ $count != 0 ];
then
        echo "User exists"
        read -p  "Are you sure to delete $username (yes/no) ?" answer
if [ "$answer" = "yes" ];
then
        sudo userdel $username > /dev/null
        echo "============User Deleted Successfully========"
else
        echo "Deletion discarded"
fi
else
        echo "User not found in Database"
fi
}

#::::::::::::::::::::::::::::Condition for the argument of the script:::::::::::::::::::::::::::
if [[ $1 == -d || $1 == --delete ]]
then
        Delete_User
fi


<<ResetPassword
1. Reset the password of an existing user account
ResetPassword

Reset_Password () {
read -p "Enter the username: " username
count=$(cat /etc/passwd | grep "$username" |wc | awk '{print $1}')
if [ $count != 0 ];
then
        echo "User exists"
read -p "Enter the new password: " password
read -p "Confirm password: " confirm_password

if [ $password == $confirm_password ];

then
echo "$username:$password" | sudo chpasswd
echo "Password Reset successfully"
else
        echo "Password Mismatched. Try again."
        exit
fi
else
        echo "User does not exist"
fi
}
#::::::::::::::::::::::::::::Condition for the argument of the script:::::::::::::::::::::::::::
if [[ $1 == -r || $1 == --reset ]]
then
        Reset_Password
fi

<<ListUserAccounts
1. list all user accounts on the system
ListUserAccounts

List_Users() {

awk -F: '{print $1, $3}' /etc/passwd | column -t
}
#::::::::::::::::::::::::::::Condition for the argument of the script:::::::::::::::::::::::::::
if [[ $1 == -l || $1 == --list ]]
then
        List_Users
fi

<<HelpandUsageInformation
1. To display usage information and the available command-line options for the script.
HelpandUsageInformation

Usage_Information() {
        echo -e "Displaying the purpose and corresponding argument to be used with the script: \n"
        echo -e "1. Create User\t $0 -c or $0 --create \n" 
        echo -e "2. Delete User\t $0 -d or $0 --delete \n"
        echo -e "3. Reset Password  $0 -r or $0 --reset\n"
        echo -e "4. List Users\t $0 -l or $0 --list\n" 
        echo -e "5. Help and Usage Info\t ./$0 -h or ./$0 --help"
}
#::::::::::::::::::::::::::::Condition for the argument of the script:::::::::::::::::::::::::::
if [[ $1 == -h || $1 == --help ]]
then
        Usage_Information
fi
