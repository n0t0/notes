### if then fi

if expression 
then
    command 1
    command 2
fi

else 

if expression
then
    command 1
else
    command 2
fi

if expression
then
    command 1
elif expressions 2
then 
    command 2
fi 

### && and ||

[ -z $1 ] && echo $1  is not defined 

### for 

for i in something
do
    command 1
    command 2
done

for i in `cat users`; do echo useradd $i; done

### case

case $VAR in 
    yes)
    echo ok;;
    no|nee)
    echo too bad
    ;;
    *)
    echo try again
    ;;
esac

### while and until 

$ while true; do true; done & --> infinitive loop (CPU maxed out)
