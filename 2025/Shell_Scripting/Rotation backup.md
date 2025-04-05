#!/bin/bash

<<info 
        this is backup sheel script which will backup the file in roation
It will contain only last 3 backups

info

# path of the files 

src="/home/ubuntu/devops_workspace"
dest="/home/ubuntu/documents"

# Number of backup copies to retain 

num_backup_to_keep=3

# date format for backup file

date=$(date '+%Y-%m-%d-%H-%M-%S')

# perform the backup

zip -r "$dest/backup_$date.zip" $src

echo " backup done "

# remove old backup exceeding the specified limit

num_backup=$(ls -l "$dest" | grep -c "backup")

num_backup_to_remove=$((num_backup - num_backup_to_keep))

if [ $num_backup_to_remove > 0 ]; then
        # List old backup, sort by timestamp, and remove the excess
        old_backup=$(ls -l "$dest" | grep "backup" | sort | head -n $num_backup_to_remove)

        for old_backup in $old_backup; do
                rm "$dest/$old_backup"
                echo "Removed old Back : $old_backup"
        done
fi
                                                                                                                                                                       1,8           Top
