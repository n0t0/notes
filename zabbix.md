### Add Repo

$ rpm -ivh http://repo.zabbix.com/zabbix/3.2/rhel/7/x86_64/zabbix-release-3.2-1.el7.noarch.rpm

### Install Agent

$ yum install zabbix-agent

### Copy docker.py and Zabbix Module (3.2 or 3.4)

- copy docker.py script
- copy zabbix_module.so 3.2 or 3.4

### Update Config

/etc/zabbix/zabbix_agentd.conf 

- Server=10.1.51.134
- ServerActive=10.1.51.134
- Hostname=<hostname>
- LoadModulePath=/etc/zabbix/modules
- LoadModule=zabbix_module_docker.so
- AllowRoot=1

### Docker Permissions

usermod -aG docker zabbix


### Hipchat Zabbix

Zabbix agent on {HOST.NAME} is unreachable for 30 seconds - sms test 

{usav1svAPIs7:agent.ping.nodata(30s)}=1

yum install perl-JSON-XS perl-libwww-perl perl-LWP-Protocol-https

1V09V1JNkfPknqy3Cnm6rUTD8sYuS4DQemrbENL1

Yr9U4QZSQSxfGx4POwIl0boRBzNUApTgTmaVOPkC


perl Makefile.PL INSTALLSITESCRIPT=/usr/lib/zabbix/alertscripts


curl -d '{"message": "A new migration was created by <xxxx>", "notify": false, "message_format": "text"}' -H 'Content-Type: application/json' 'https://hipchat.ambrygen.com/v2/room/Zabbix/message?auth_token=Yr9U4QZSQSxfGx4POwIl0boRBzNUApTgTmaVOPkC'


curl  -XPOST 'https://hipchat.ambrygen.com/v2/room/Zabbix/notification' -d '{"color":"green","message":"Test2"}' -H 'content-type:application/json' -H 'Authorization: Bearer Yr9U4QZSQSxfGx4POwIl0boRBzNUApTgTmaVOPkC'




su -c "./zbx-notify 'Zabbix' 'PROBLEM:myHOSTNAME Temperature Failure on DAE5S Bus 1 Enclosure 1' 'Host: myHOSTNAME Trigger: PROBLEM: myHOSTNAME temp Failure on DAE5S Bus 1 Enclosure 1: High Timestamp: 2016.03.14 11:57:10 eventid: 100502' --hipchat_api_url=https://hipchat.ambrygen.com/v2/room/Zabbix/notification --api_token=Yr9U4QZSQSxfGx4POwIl0boRBzNUApTgTmaVOPkC --hipchat --nofork" -s /bin/sh zabbix


./zbx-notify 'Zabbix' 'THIS IS A TEST' 'Host: myHOSTNAME Trigger: PROBLEM: THIS IS A TEST: High Timestamp: date' \
--hipchat_api_url=https://hipchat.ambrygen.com \
--api_token=Yr9U4QZSQSxfGx4POwIl0boRBzNUApTgTmaVOPkC \
--hipchat



curl -H "Content-Type: application/json" \
     -X POST \
     -d "{\"color\": \"purple\", \"message_format\": \"text\", \"message\": \"$MESSAGE\" }" \
     https://api.hipchat.com/v2/room/$ROOM_ID/notification?auth_token=$AUTH_TOKEN






./zbx-notify 'Zabbix' 'THIS IS A TEST' 'Host: myHOSTNAME Trigger: PROBLEM: THIS IS A TEST Timestamp: date' \
--hipchat_api_url=https://hipchat.ambrygen.com \
--api_token=Yr9U4QZSQSxfGx4POwIl0boRBzNUApTgTmaVOPkC \
--hipchat



echo "{TRIGGER.STATUS}: {TRIGGER.NAME} | /usr/local/bin/hipchat_room_message -t HzWYVBJBLNLHTXXKeo2qEKcEDtmbsSBXownvpVk6 -f "Zabbix" -r 29 -n -c red


Zabbix agent on {HOST.NAME} is unreachable for 5 minutes
{Template App Zabbix Agent:agent.ping.nodata(30sec)}=1

{TRIGGER.DESCRIPTION}
Status: {STATUS}
Severity: {TRIGGER.SEVERITY}
Timestamp: {EVENT.DATE} {EVENT.TIME}
eventid: {EVENT.ID}


{TRIGGER.DESCRIPTION}
Status: {STATUS}
Severity: {TRIGGER.SEVERITY}
Timestamp: {EVENT.DATE} {EVENT.TIME}
eventid: {EVENT.ID}
Event Acknowledgement history: {EVENT.ACK.HISTORY}
Escalation history: {ESC.HISTORY}


{
            "fallback": "[[{HOST.NAME}:{TRIGGER.NAME}:{STATUS}]]",
            "pretext": "New Alarm",
            "author_name": "[[{HOST.NAME}]]",
            "title": "[[{TRIGGER.NAME}]]",
            "fields": [
                {
                    "title": "Status",
                    "value": "{STATUS}",
                    "short": true
                },
                {
                    "title": "Severity",
                    "value": "{TRIGGER.SEVERITY}",
                    "short": true
                },
                {
                    "title": "Time",
                    "value": "{EVENT.DATE} {EVENT.TIME}",
                    "short": true
                },
                {
                    "title": "EventID",
                    "value": "eventid: {EVENT.ID}",
                    "short": true
                }
                
                
            ]
        }


### Portal Redis

Portal staging 
REDIS PASSWORD

staging: LfKQBNe12dfakJAB
prod:    K5MFNSLoi3fasd4A
