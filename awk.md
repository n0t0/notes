### Getting Started 

pattern { action }
pattern { action }
...


awk '/foo/ { print $0 }' input-file --> prints lines found "foo" lines 

awk '/foo/' input-file --> likewise 

### Two Rules 

awk '/12/ { print $0 }
     /21/ { print $0 }' input-file1 input-file2


ls - l | awk '$5 == "Nov" { sum += $4 }
              END { print sum }' 

### How to Run awk Programs

awk 'program' input-file1 input-file2 --> run short program

awk -f program-file input-file1 input-file2 --> long program 

### Running awk Without Input Files

awk 'program' 

awk '/th/' --> end with Ctrl+D

### Running Long Programs 

awk -f source-file input-file1 input-file2 
awk -f th-prog.awk input-file1 input-file2 

### Executable awk Programs 

'''
#! /bin/awk -f 

# a sample awk program 
BEGIN { print "hello, world" }
'''

awk 'program' "$@" --> $@ forward all argument to awk program 

awk '/12/ { print $0 } 
     /21/ { print $0 }' input-file1 input-file2

### Reading Input Files and Split Records

input-file --> awk divides it by records and fields 

Change built-in variable RS --> assign a new record separator (\n by default)

awk 'BEGIN { RS = "/" } ; { print $0 }' input-file 
awk '{ print $0 }' RS="/" input-file --> var assignment 

### Examinig Fields 

- separated by white space by default 

$ --> refer to a field in awk program e.g. $1 
$NF --> last field ot the record 
$0 --> represents the whole input method 

awk '$1 ~ /foo/ { print $0 }' input-file --> print lines with first field "foo" ; ~ --> matching operator 

awk '/foo/ { print $0, $NF }' input-file --> print first and last field of a record containing the match

### Non-constant Field Numbers

awk '{ print $(2*2) }' input-file 

### Changing the Contents of a Field 

awk '{ $3 = $2 - 10; print $2, $3 }' input-file 

awk '{ $3 = $2 - 10; print $0 }' input-file 

awk '{ $4 = ($3 + $2 + $1); print $4 } input-file 


echo a b c d | awk '{ OFS = ":"; $2 = "" ; print ; print NF }'

### Specifying how Fields are Separated 

FS = ","

awk 'BEGIN { FS = "," } ; { print $2 }'

FS = ", \t" --> change field separator 

awk -F, 'program' input-files --> delimeter by ","

awk -F: '$2 == ""' /etc/passwd --> look for users without password 


sed 1q /etc/passwd | awk '{ FS = ":" ; print $1 }'


### Multiple-Line Records 

RS = "\f" --> making a record a page of a file 

RS = null string 
FS = "\n" --> separate fields by blank lines

### Explicit Input with getline 

```
aws '{
    if (t = index($0, "/*")) {
        if (t > 1)
            tmp = substr($0, 1, t - 1)
        else
            tmp = ""
        u = index(substr($0, t + 2), "*/" )
        while (u == 0) {
            getline
            t = -1
            u = index($0, "*/")
        }
        if (u <= lenght($0) - 2)
            $0 = tmp substr($0, t + u + 3)
        else
            $0 = tmp
    }  
    print $0
}'


