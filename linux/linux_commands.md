### Linux Commands

$ chsh -s /bin/bash --> change shell

### Symbolic Links (shortcuts)

$ ln -s prog.1.1 prog
$ ls -l prog
lrwxrwxrwx   2 mdw      users           8 Nov 17 14:35 prog -> prog.1.1

### Printing the shell’s pathname, home, user, path* and all in env command
$ echo $SHELL
$ echo $HOME
$ echo $USER
$ echo $PATH
$ env

### Redirecting Output and Appending

$ ls /usr/bin > ~/Binaries

$ ls /bin >> ~/Binaries
#Send to a Black Hole

$ gcc invinitjig.c 2>error-msg >/dev/null

### Using Pipes

$ du > du_output
$ sort -nr du_output

$ du | sort -nr
$ du | sort -nr | head; tail

### File Command to Look File Type Description

$ file my_file.txt

### !! - Runs the Very Last Command

### Creating an Alias

$ alias keyword=‘ls -la’

- then add to ~/.bashrc

### Showing All Virtual HDDs
*****************************

### List Mounted Drives

$ lsblk
$ df

### Check Disk for a Data Before Mounting

$ file -s /dev/xvdf

### Formatting Disk and Making a File System

$ mkfs -t ext4 /dev/xvdf

### Create Dir in Root

$ mkdir /fileserver

### Mounting Disk

$ mount /dev/xvdf/ /fileserver/

### Unmount

$ umount /dev/xvdf/

### Bash Script for installing Apache Server
*********************************************

	#!/bin/bash

	$ sudo su
	$ yum update -y
	$ yum install httpd -y
	$ service httpd start
	$ chkconfig httpd on
	$ d /var/www/html/
	$ aws s3 cp s3://inverto-web/index.html /var/www/html/


### Prints NAME for a Command From All Manual Pages

$ apropos ls

### List all Processes + deamons

$ ps ax | more

### Look Up for a Name or Partial Name on a Process

$ ps -C httpd

### Entire Unix System

$ ps aux

### Miscs

$ namei -l /var/www/html/ —> lists path directions
$ lscpu —> cpu info
$ nproc —> number cpu cores
$ ssh remote-host:/directory mountpoint
$ fusermount -u mountpoint

### Replace a String in Multiple Files and Create a Backup Before

$ find /path -type -f exec sed -i.bak 's/string/replacement/g' {} \;

### Backup

$ tar -czvf destination/file.tgz    source/ —> creates a file to local directory from a source
$ tar -xzvf file.tgz -C /some/local/dir/ —> extracts a file to a local dir (must exists)

$ rsync -avzh —delete ~/docs /Volumes/agent/docs/ —> syncs files and deletes files/folders that exist in the target directory

Bash Scripting 

### Variables

s=$(pwd)
echo $s
ls $s

### read

read myvalue
<enter text>
echo $myvalue

read -p "type your age " age
echo $age
echo "you are $age old"

read -s password
<enter password> --> (not visible)
echo $password

### Aritmethic

echo " $((2+3)) "
echo " SUM $(( number1 + number2 )) "
echo " PRODUCT $(( number1 * number2 )) "
echo " DIVISION $(( number1 - number2 )) "
echo " REMINDER $(( 10 % 3 )) "
echo " POWER $(( 3**2 )) "

- increase a variable
number1=$(( number1 + 1))
echo " $(( number1++ ))

- short way of operating on a variable
num=10
num=$(( num + 3 ))
echo "ADD $(( num+=3 ))
echo "SUBSTRACT $(( num-=6 ))
echo "MULTI $(( num*=10 ))

### Arithmetic Conditions

- [ 3 -eq 3 ] same as [ 3 = 3 ] --> equal
- [ 3 -nq 4 ] same as [ 3 is not 4 ] --> not equal
- [ 3 -qt 2 ] same as [ 3 > 2 ] --> greater than
- [ 3 -lt 7 ] same as [ 3 < 7 ] --> less than

- [ 3 -qe 3 ] same as [ 3 >= 3 ] --> greater or equal
- [ 3 -le 3 ] same as [ 3 <= 3 ] --> less or equal

### Exit Status

0 - good
1+ - error