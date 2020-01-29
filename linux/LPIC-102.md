### hardware (clock)
$ hwclock --systohc--> set the hardware clock to the current system time (to software clock)
$ hwclock --hctosys --> set the system time (software clock) to the hardware clock

### /ect/crontab

$ sudo crontab -e --> roots cron jobs
$ crontab -u tbaker my-cron
- /etc/crontab --> configuration file
- /var/spool/cron --> user crontab files

### ssh_config / sshd_config


### cups location

- /etc/cups/cups.conf
- /etc/cups/cupsd.conf --> main configuration
- /etc/cups/printers.conf --> add or delete printers
- /etc/cups/ppd --> additional Postscript Printer Definition
- /var/spool/cups --> queues
- http://localhost:631 --> CUPS Web-Based Utilities


### X servers

- XFree86
- X.org-X11
- Accelerated-X
- /etc/X11/xorog
- xorg.conf
- XF86Config

### display info

$ xdpyinfo --> diplay info
$ xwininfo --> window info
- $DISPLAY --> env variable

### NTP

- /etc/ntp
- /etc/ntp.conf
$ date
$ service ntpd start
$ ntpq --> interarctive mode


### X Login Managers

- /etc/sysconfig/desktop
- /etc/X11/xdm/Xaccess

### X Accessibility

$ kmag --> magnifier
- orca
- Emacspeak

### Email software

- Sendmail
- Postfix
- Exim
- Qmail

### syslogd

- facility.priority action

### IPv4 and IPv6

- 10.0.0.0 - 10.255.255.255 --> reserved IPs for class A
- 172.16.0.0 - 172.31.255.255 --> class B
- 192.168.0.0 - 192.168.255.255 --> class C

- A 1.0.0.0 - 127.255.255.255
- B 128.0.0.0 - 191.255.255.255

- fe80:: --> local address
- fec, fed, fee, fef -->

### bash script

- var $0, $1, $2

### inted and xinted

- /etc/inetd.conf
- /etc/xinetd.conf

### TCP Wrappers
