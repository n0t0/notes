nvalentine    zLa@&F434orR
wchoi         TEr2$5&8r123
iivanov       FM@(7fasmf>4
rmartin       B!K#Ft234o0W
sample_kits   DAKU@Hdsa2$$
sample_kits   ksluHFL#I$Yhf@

### Login

mongo -U <user> -P <pass> --host usav1svNOSp1 --port 28017 admin

### Add User 

db.createUser({ user: "user", pwd: "zLa@&F434orR", roles: [{role: "dbAdmin", db: "sessions" }]})

db.createUser({ user: "sample_kits", pwd: "KjFA@dasd^bm", roles: [{role: "application", db: "admin" }]})

### Grant Roles 

db.grantRolesToUser( "user", [ {role: "developer", db: "query_tool" } ], { <writeConcern> } )


### Update user 

db.updateUser( "user", { roles : [{ role: "developer", db: "admin" }], pwd: "    ",})

### Change password

db.changeUserPassword("sample_kits", "DAKU@Hdsa2$$")

### NOSp3

mongo --port 27017 -u "root" -p "f0xh0und" --authenticationDatabase "admin"
mongo --port 27017 -u "ITDevAdmin" -p "ambryitdevrules" --authenticationDatabase "admin"

mongo --port 27017 -u "portal" -p "qxJVLIrOGDSYnoBzcGVv^C" --authenticationDatabase "admin"


1cAuQnHhMMV7

u: iivanov p: s738 h: noss4
u: portal  p: 22AFM@Hdad2$ h: noss4