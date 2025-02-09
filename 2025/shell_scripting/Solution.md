Week 3 Challenge 1: User Account Management

Logic behind my implementation:
1. With just the command ./user_management.sh, the following message pops up:
```bash
Please specify what to do using the script ./user_management.sh
For Help or Usage Info use any:	 ./user_management.sh -h or ./user_management.sh --help
```
 This directs the user to use help option, where the whole command line options can be displayed.

```bash
/scripts$ ./user_management.sh -h

Displaying the purpose and corresponding argument to be used with the script: 
1. Create User	 ./user_management.sh -c or ./user_management.sh --create 

2. Delete User	 ./user_management.sh -d or ./user_management.sh --delete 

3. Reset Password  ./user_management.sh -r or ./user_management.sh --reset

4. List Users	 ./user_management.sh -l or ./user_management.sh --list

5. Help and Usage Info	 ././user_management.sh -h or ././user_management.sh --help
```
  Now the user can opt which action has to be carried out and hence the corresponding argument can be used.
  1. Create user
     1. The script checks if the user already exist in /etc/passwd
        ```bash
        ~/scripts$ ./user_management.sh -c
        Enter username: Ram
        User already exists
        ```
     2. If not, new user is added and passwd is entered
         ```bash
        ~/scripts$ ./user_management.sh -c
         Enter username: Hanuman
         New User
         Enter password: asdf
         User Hanuman has been created successfully.
         ============Creation of new user completed========
            ```
2. Delete user
     1. The script checks if the user already exist in /etc/passwd. If so, a prompt appears to confirm the deletion. If yes is entered, the username is deleted
        ```bash
        ~/scripts$ ./user_management.sh -d
        Enter the username: rohan
        User exists
        Are you sure to delete rohan (yes/no) ?yes
        ============User Deleted Successfully========

        ```
     2. If the username does not exitst, the script returns a message conveying username not found
       
```bash
      ~/scripts$ ./user_management.sh -d
      Enter the username: rahul
      User not found in Database
```
3. Reset Password
     1. The script checks if the user already exist. If so, a prompt appears for New password followed by its confirmation. The script checks if these both entires match, if yes, password is changed.
        ```bash
        ~/scripts$ ./user_management.sh -r
        Enter the username: Ammu
        User exists
        Enter the new password: asdf
        Confirm password: asdf
        Password Reset successfully
        ```
     2. If the password entries mismatch, a message is displayed to try again
         ```bash
         ~/scripts$ ./user_management.sh -r
          Enter the username: Ram
          User exists
          Enter the new password: asdf
          Confirm password: lkjh
          Password Mismatched. Try again.
         ```
     3. If the username does not exits, it displays so
        ```bash
        ~/scripts$ ./user_management.sh -r
        Enter the username: gautam
        User does not exist
        ```
4.  List Users
     1. The script lists all the users in /etc/passwd with the columns for Name and ID displayed
        ```bash
        ~/scripts$ ./user_management.sh -l
        ubuntu                1000
        Reeta                 1003
        Ram                   1004
        sita                  1005
        adi                   1006
        anum                  1008
        Amma                  1009
        Amritha               1012
        tomy                  1014
        Arya                  1015
        Ammu                  1016
        Jayan                 1017
        Hanuman               1018
        ```
        
    
   
 
