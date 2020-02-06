### Basics 

$ sudo tcpdump -nvvv -i any -c 100 -s 100

### Filters

$ sudo tcpdump -nvvv -i any -c 3 host 10.0.3.1 --> search traffic to and from host 
$ sudo tcpdump -nvvv -i any -c 3 src host 10.0.3.1 --> show only specific source of the packet
$ sudo tcpdump -nvvv -i any -c 3 dst host 10.0.3.1 --> destination 

$ sudo tcpdump -nvvv -i any -c 3 port 22 and port 6061 --> 'and' and 'port 22 && port 443' operators
$ sudo tcpdump -nvvv -i any -c 3 port 80 or port 8080 --> 'or' and 'port 22 || port 443' operators

$ sudo tcpdump -nvvv -i any -c 3 '(port 80 || port 8080) and host 10.0.3.169' --> 'or' and 'port 22 || port 443' operators

$ sudo tcpdump -nvvv -i any -c 3 '(port 80 || port 8080) and (host 10.0.3.169 or host 10.0.3.10)' --> 'or' and 'port 22 || port 443' operators

### Identifying Packets Type

- [S] --> SYN (Start Connection)
- [.] --> No Flag
- [P] --> PSH (Push Data)
- [F] --> FIN (Finish Connection)
- [R] --> RST (Reset Connection)

- [S.] --> SYN-ACK


### Packet Inspection 

$ sudo tcpdump -nvvv -i any -c 1 -XX 'port 80 and host 10.10.10.54' --> print in hes and ascii
$ sudo tcpdump -nvvv -i any -c 1 -A 'port 3306 and host 10.3.24.15' --> print in ascii only

### Non-TCP Traffic 

$ sudo tcpdump -nvvv -i any -c 2 icmp
$ sudo tcpdump -nvvv -i any -c 2 udp 