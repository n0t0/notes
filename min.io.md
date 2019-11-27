### Install

wget https://dl.min.io/server/minio/release/linux-amd64/minio
chmod +x minio
./minio server /data

### Firewall

firewall-cmd --get-active-zones

firewall-cmd --zone=public --add-port=9000/tcp --permanent

firewall-cmd --reload


### Minio Client

wget https://dl.min.io/client/mc/release/linux-amd64/mc
chmod +x mc
./mc --help


