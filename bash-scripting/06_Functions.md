### Options 

- getops


### Functions 

- two approaches to define a function 

#### approach No.1 

function func_name
{
    echo this is how you do it
}


#### approach No.2

func_name ()
{
    echo this is how you do it
}

### Arrays

- names=(maria mila maya monika)
- names[0]=maria
- names[1]=mila
- names[2]=maya
- names[3]=monika

$ echo ${names[2]}
$ echo ${names[@])}
$ echo ${#names[@])}

- name[4]=mery

### Defining menu interfaces 

- select 
- break 

### trap

- trap --> can be used to redefine signals 
- man 7 signal 