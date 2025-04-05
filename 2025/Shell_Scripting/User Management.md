#!/bin/bash
#
<<info 
This is shell script to create the user
info


function create_user {

echo "================Creation of the user================"

read -p " enter the username that you wish to create: " username

# id cmd will filter out the username if it is already there then it come out 1 and if user is not there then outcome will be 0

id=$(cat /etc/passwd | grep "$username" | wc | awk '{print $1}' )

# if else statment the check the outcome of id variable if it is 0 then it will create the user and if it 1 then it will show that user is already there
#
if [ $id == 0 ];
then
        sudo useradd -m "$username"

read -p "enter the password: " password

echo -e "$password\n$password" | sudo passwd "$username"

else
        echo " user already exist "
fi


}

function delete_user {

echo " =========== Account deleletion ========="

read -p "enter the user you wish to delete: " username

id=$(cat /etc/passwd | grep "$username" | wc | awk '{print $1}')

if [ $id != 0 ];
then
        sudo userdel -r "$username"
echo " $username has been deleted "
else
        echo "user do not exist"
fi


}


function password_reset {

echo " ============= Password Reset =========== "

read -p " please enter the username to reset the password : " username

id=$(cat /etc/passwd | grep "$username" | wc | awk '{print $1}')

if [ $id != 0 ];

then 
        read -p " enter the new password : " password
        echo -e "$password\n$password" | sudo passwd "$username"
else
        echo " user does not exist"
fi
}

function list_user {

echo " ============ listing the users ================="

cat /etc/passwd 

}



echo "Enter -c or --create to Create a new User"

echo "Enter -d or --delete to Delete the User"

echo "Enter -r or --reset to Reset the password"

echo "Enter -l or --list to Display the Users."



read -p " Enter your option " option

case "$option" in

        -c | --create)
        echo "You choose the option to create user "
        create_user;;

-d |--delete)
        echo "You choose the option to delete user "
        delete_user;;

-r | --reset)
        echo "You choose the option to reset the password "
        password_reset;;

-l | --list)
        echo "You choose the option to list user "
        list_user;;

esac
