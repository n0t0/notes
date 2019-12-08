### grep

$ grep -i --> case insenstive
$ grep -r --> recursive for directories
$ grep -e --> REGex
$ grep -v --> ignore

### test

[[ $VAR=a* ]] || echo string doesn't start with "a"

### cut & sort

$ cut -f 1 -d : /etc/passwd
$ du -h | sort -rn | head 
$ sort -n -k3 -t : /etc/passwd 

### tail and head 

$ head -5 /etc/passwd | tail -1

### sed 

$ sed -n 5p /etc/passwd 
$ sed -i s/old-text/new-text/g ~/myfile --> substitute 
$ sed -i -e '2d' ~/myile --> edit and delete second line 
$ sed -i -e '2d;20,25d' ~/myfile 

### awk 

$ awk -F : '{ print $4 }' /etc/passwd 
$ awk -F : '/user/ { print $4 }' /etc/passwd
$ awk -F : '$3 > 500' /etc/passwd 
$ awk -F : '$NF ~/bash/' /etc/passwd --> first and last field 

### tr

$ echo hello | tr [a-z][A-Z] 
$ echo hello | tr [:lower:][:upper:]
