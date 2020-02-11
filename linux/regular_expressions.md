### Regular Expressions

### Basics

- ^ - beginning of line
- $ - end of line 
- . - a single character 
- ? - preceding character matches 0 or 1 times only
- * - preceding character matches 0 or more times
- + - preceding character matches 1 or more times  
- [] - range
- [xyz] - on of the characters in the set range
- [^xyz] - negate of occurrence of a character set 
- {n} - the preceding character matches at least n times 
- {n,m} - the preceding character matches at least n times and not more than m times
- <word> - word matching 
- Escape character
- | - pipe or logical symbol 

### ^

$ ls -l | grep ^d - directories 
$ ls -l | grep ^c - character files 
$ ls -l | grep ^b - block files 
$ ls -l | grep ‘^#’ filename - finding commented lines 
$ ls -l | grep ‘^abc’ filename - finding lines ‘abc’ in a file 

### $

$ ls -l | grep sh$
$ ls -l | grep ‘dead$’ filename - finding a line in a file ending with dead
$ grep ‘^$’ filename - finding empty lines in a file  

### *

$ ls -l | grep ‘g*ro’
$ grep ‘ap*le’ - useful for misspelled words in a file 

### .

$ ls -l | grep ’t.t’ - matching a single character 
$ ls -l | grep ‘a.*x’ - matching file names starting with a and finishing with x 
- .* combination - . - any character ; * - and it’s repeated 0 or any number of times 

### []

$ ls -l | grep ‘a[0-9]x’ - finding files names with a number in between a and x 
- [a-z] - matching any single character between a to z
- [A-Z] - matching any single character between A to Z
- [0-9] - matching any single character between 0 to 9
- [a-zA-Z0-9] - matching any single character from the above 3 
- [!@#$%^] - matching any characters in the brackets 

### [^CHAR]

$ ls -l | grep ‘[^abc] - all files that don’t contain a, b or c 

$ grep ‘<abc>’ filename  - search for a word exclusively 
$ egrep ‘word’ filename - print the entire line that contains the ‘word’
$ egrep -n ‘word’ filename - add the line number 
$ egrep -c ‘word’ filename - counts the line matched  
 

### ESCAPE

$ grep “[“ filename
$ grep ‘[[]’ filename 