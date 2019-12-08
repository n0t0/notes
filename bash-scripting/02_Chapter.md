# argument
# option
# parameter
# variable

#### Defined variables

# static: VARNAME=value
# as an argument $1, $2
# using 'read'

#### Defining variables with 'read'

# bash -x scriptname --> show every line from the script

#### Variables and subshells

# export --> exports variables to subshells

# /etc/profile
# /etc/bashrc

#### Quoting

# ' - strong
# " - weak

#### Arguments

# ${nn} or shift more than 9 arguments
# use 'for' to evaluate all possible arguments
# $@ to refer to all arguemnts provided
# $# to count the amount of arguments provided
# $* if you need a single string that contains all arugments

# bash -x scriptname --> executes the script in bash

#### Shift

# ${10}

#### Command substition

# `command`
# $(command)

#### String Verification

# test -z --> check if a string is empty

# use [[ $1 == '[a-z]*' ]] to check for specific patterns

#### Test command
