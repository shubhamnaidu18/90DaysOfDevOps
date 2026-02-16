#!/bin/bash

# This is a 'here-document' (info block) used to describe the purpose of the script.
<<info
        this is a shell script that build for user managemnet
info

# Define a function to handle creating multiple users
function create_user {
echo " ====== Account Creation ===== "
# Ask the user for the total count of accounts they want to set up
read -p "Enter the number of user's to be created: " num

# Standard C-style for loop: starts at 1, runs until it reaches $num, increments by 1
for (( i=1; i<=$num; i=i+1 )) do
        # Prompt for individual account details inside the loop
        read -p "enter the username: " username
        read -p "enter the password: " password

        # Check if user exists by searching /etc/passwd. wc -l returns 1 if found, 0 if not.
        count=$(cat /etc/passwd | grep $username | wc | awk '{print $1}')

# Logic: If count is 0, the username is available
if [ $count == 0 ];
then
        # Create user with a home directory (-m)
        sudo useradd -m $username
        # Automate the password prompt by piping the password twice (for confirmation) to the passwd command
        echo -e "$password\n$password" | sudo passwd "$username"

        echo "======= User is created ========"
else
        # If count is not 0, inform the admin to avoid duplicates
        echo "User already exist in the system"
fi
done

}

# Define a function to handle deleting multiple users
function user_deletion {

        echo " ===== Account deletion ====="

        # Ask how many users need to be removed in this session
        read -p "Enter the number of user's to be delete: " num

# Loop through the deletion process based on the number provided
for (( i=1; i<=$num; i=i+1 )) do

        read -p "enter the username: " username

        # Verify if the user exists before attempting deletion
        count=$(cat /etc/passwd | grep $username | wc | awk '{print $1}')

# Logic: If count is 1, the user exists and can be deleted
if [ $count == 1 ];
then
        # Delete user and remove their home directory (-r) to save disk space
        sudo userdel -r "$username"

        echo "======= User is deleted ========"
else
        echo "User does not exist in the system"
fi
done

}

# Define a function to change the password of an existing user
function password_reset {

        echo "====== Password reset ======"
read -p " enter the username to reset the password: " username

# Verify user existence before asking for a new password
count=$(cat /etc/passwd | grep $username | wc | awk '{print $1}')

if [ $count == 1 ];
then
        read -p " enter the new password: " password
        # Update the system password database using the new input
        echo -e "$password\n$password" | sudo passwd "$username"
        echo "Password has been reset"
else
        echo "User does not exist in the system"
fi
}

# Define a function to show all users currently on the system
function list_user {

echo " ============= listing the users ================"

# Displays the content of the password file (where user identities are stored)
cat /etc/passwd

}

# Print the visual menu for the administrator
echo "Enter -c or --create to Create a new User"
echo "Enter -d or --delete to Delete the User"
echo "Enter -r or --reset to Reset the password"
echo "Enter -l or --list to Display the Users."

# Capture the admin's choice from the menu above
read -p "Enter your option " option

# Switch-case block to execute the correct function based on the input 'option'
case "$option" in

                # Match either the short flag or the long flag
                -c | --create)
                echo "You choose the option to create user "
                create_user;; 
# Call the creation function and stop case

                -d |--delete)
                echo "You choose the option to delete user "
                user_deletion;; # Call the deletion function and stop case

                -r | --reset)
                echo "You choose the option to reset the password "
                password_reset;; # Call the password reset function and stop case

                -l | --list)
                echo "You choose the option to list user "
                list_user;; # Call the list function and stop case

esac
