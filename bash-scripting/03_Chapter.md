### Substitution Operator Examples

- **${VAR:-word}** if $VAR exists, use its value; if not, return the value "word"
- **${VAR:=word}** if $VAR exists, use its value; if not, set the default value to "word"
- **${VAR:?wessage}** if $VAR exists, show its value, if not, display $VAR followed by message
- **${VAR:offset:length}** if $VAR exists, show the substring of $VAR, starting at _offset_ with a lenght of _lenght_.

### Pattern matching

- ${VAR#pattern} search for pattern from the beginning of variable's value, delete the shortest part that matches, and return the rest

```
FILENAME=/usr/bin/blah
echo ${FILENAME#*/}
usr/bin/blah
```

- ${VAR##pattern} search for pattern from the beginning of variable's value, delete the longest part that matches, and return the rest

```
FILENAME=/usr/bin/blah
echo ${FILENAME##*/}
blah
```
- ${VAR%pattern} search for pattern from the end of variable's value, delete the shortest part that matches, and return the rest

```
FILENAME=/usr/bin/blah
echo ${FILENAME%/*}
usr/bin
```

- ${VAR%%pattern} search for pattern from the end of variable's value, delete the logest part that matches, and return the rest

```
FILENAME=/usr/bin/blah
echo ${FILENAME%%/*}
```

### REGex

- grep, awk, sed

### Calculating

$ echo $(( 10 + 10 ))

```
let x="$1 $2 $3"
echo $x
```
$ lets 1 + 2
