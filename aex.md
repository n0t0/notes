[databases.core]
driver = "mysql"
user = "ambry_exchange"
passwd = "S7buFTHJwa7oLHgkD3Ve1Ea1mZanWXAK"
addr = "usav1svHAPp10:3307"
dbname = "core"

[databases.lab_director]
driver = "mysql"
user = "ambry_exchange"
passwd = "S7buFTHJwa7oLHgkD3Ve1Ea1mZanWXAK"
addr = "usav1svHAPp10:3308"
dbname = "lab_director"
collation = "utf8mb4_unicode_ci"
interpolateParams = true
parseTime = true
net = "tcp"

[databases.portal]
driver = "mysql"
user = "ambry_exchange"
passwd = "S7buFTHJwa7oLHgkD3Ve1Ea1mZanWXAK"
addr = "usav1svHAPp10:3308"
dbname = "portal"

[databases.portal_ro]
driver = "mysql"
user = "ambry_exchange"
passwd = "S7buFTHJwa7oLHgkD3Ve1Ea1mZanWXAK"
addr = "usav1svHAPp10:3307"
dbname = "portal"
collation = "utf8mb4_unicode_ci"
interpolateParams = true
parseTime = true

[databases.ambry_telcor]
driver = "mysql"
user = "ambry_exchange"
passwd = "cA3DQMEzncnGgdyu"
addr = "usav1svhapp50:3308"
dbname = "telcor"

[databases.ambry_telcor_ro]
driver = "mysql"
user = "ambry_exchange"
passwd = "cA3DQMEzncnGgdyu"
addr = "usav1svhapp50:3307"
dbname = "telcor"
ss