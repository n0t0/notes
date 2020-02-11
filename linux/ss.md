### ss (netstat)

$ ss -l --> display listening sockets 
$ ss -tu --> tcp/udp connections 
$ ss -t -a --> list all 

$ ss -4 state all --> FILTER all
$ ss -4 state listening

$ ss dst 192.168.1.139 

$ ss -n --> don't resolve services, just port 
$ ss -r --> resolve IP
$ sudo ss -tp --> list process ID 
$ ss -s --> summary statistics 

$ ss -nt dst :443 or dst :80 --> filter by destination port 

$ ss -m --> display memory usage per socket 
$ ss -ltp sport le 500 --> list ports <= 500

$ ss -ltZ --> show SELinux security 
$ ss -te --> extended information 
$ ss -tn -o --> timer information 