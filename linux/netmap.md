### Nmap

### Scanning for SMB vulnerabilities (server message block)

$ nmap —script [scriptname] -p[port][host] 
$ nmap -script=smb-vuln-ms17-010.nse [host-range]

$ nmap —script smb-os-discovery.nse —script-args=unsafe=1 -p 445 [host]

$ nmap -p 445 -script=smb-vuln-ms17-010.nse [host-range]

### Scanning for Open Ports 

$ nmap -sP 192.168.0.0-100 —> ping scan for live hosts
$ nmap -sS [IP address]-O —> SYN scan OS detection 

$ nmap -sV 192.168.0.1 -A —> port scan 
$ nmap -sV 192.168.0.1 -A -v —> verbose port scan  

$ sudo nmap -O remote_host —> scan OS system 
$ sudo nmap -PN remote_host 
$ sudo nmap -PN xxx.xxx.xxx.xxx-xxx —> scan multiple hosts 
$ sudo nmap -sP network_addr_range —> scan available services 

$ sudo nmap -n remote_host —> no reverse DNS scan 
$ sudo nmap -p port_number remote_host —> scan specific port 

$ sudo nmap -sT remote_host —> scan for TCP connections 
$ sudo nmap -sU remote_host —> scan for UDP connections 

$ sudo nmap -n -PN -sT -sU -p remote_host —> scan every open TCP and UDP port 

$ sudo nmap -PN -p port_number -sN remote_host 

$ sudo nmap -PN -p port_number -sV remote_host —> scan services and their versions 

### Detecting Live Hosts 

$ sudo nmap -sn 192.168.56.0/24 
$ sudo nmap -iL / file.txt
$ sudo nmap 192.168.57.0/24 —exclude 192.168.1.5
$ sudo nmap -iL /tmp/scanlist.txt —exclude /tmp/exclude.txt

### Firewall Scanning 

$ sudo tcpdump host target_ip_addr -w /tmp/scan_results/packets

$ sudo nmap -sS -Pn -p-p -T4 -vv —reason -oN /tmp/scan_results/nmap.results target_ip_addr

$ sudo tcpdump -nn -r /tmp/scan_results/packets | less 

### Scanning for Open UDP Ports 

$ sudo sysctl -w net.ipv4.icmp_ratelimit=0  —> ICMP ping limit 
$ sudo sysctl net.inet.icmp.icmplim —> macOS 

### Layer 2 Discovery 

$ sudo nmap 172.16.36.133 -sn

### Banner Grabbing

$ sudo nmap -sT 172.16.36.133 -p 22 —script=banner

### Information Gathering 

$ sudo nmap —script ip-geolocation-* hostname
$ sudo nmap -p80 --script dns-brute hostname
$ sudo nmap -p80 —script http-reverse-ip hostname

### Penetrating into Servers 

$ sudo nmap -p1433 —script ms-sql-info 192.168.1.77
$ sudo nmap -p1433 —script ms-sql-brute 192.168.1.77

$ sudo nmap -p1433 -script ms-sql-brute -script-args userdb=/var/usernames.txt,passdb=/var/passwords.txt —> check for users and passwords passed as arguments 

$ sudo nmap -p1433 —script ms-sql-empty-password 192.168.1.77 —> check for null password 

$ sudo nmap -p1433 —script ms-sql-hasdbaccess.nse —script -args mussel.username=sa 192.168.1.77 —> SA has no password and DBs are known 

$ sudo nmap -p1433 —script ms-sql-tables —script -args mssql.username=sa 192.168.1.77

$ sudo nmap -p1433 —script ms-sql-xp-cmdshell —script -args mssql.username=sa 192.168.1.77 —> for SQL server 2000 

### Hacking 

$ sudo nmap -p80,443 --script http-waf-detect --script-args="http-waf-detect.aggro,http-waf-detect.detectBodyChanges" targetWebsite.com —> WAF detection 

$ sudo nmap -p80,443 --script http-waf-fingerprint targetWebsite.com —> WAF fingerprint detection 

$ sudo nmap -p80,443 --script http-waf-fingerprint --script-args http-waf-fingerprint.intensive=1 targetWebsite —> intensive 

$ sudo nmap -p80,443 --script http-errors targetWebsite.com —> HTTP errors codes 

$ sudo nmap -vv -p80,443 --script http-errors --script-args "httpspider.url=/docs/,httpspider.maxpagecount=3,httpspider.maxdepth=1" targetwebsite.com —> likewise (intensive)

$ sudo nmap -p80,443 --script dns-brute targetWebsite.com —> find shares and new servers 

$ sudo nmap -p80,443 --script dns-brute --script-args dns-brute.threads=25,dns-brute.hostlist=/root/Desktop/custom-subdomain-wordlist.txt targetWebsite.com —> intensive 

$ sudo nmap -p80,443 --script http-exif-spider targetWebsite.com —> EXIF 

$ sudo nmap -p80,443 --script http-exif-spider --script-args="http.max-cache-size=99999999" targetWebsite.com —> intensive 