## Logstash

### Version

bin/logstash --version

systemctl daemon-reload

## Kibana

systemctl daemon-reload'

## Filebeat


## Elastic Search


### Version

curl -XGET 'localhost:9200'

### Health

curl -XGET 'localhost:9200/_cat/health?pretty'

### Cluster Status

curl -XGET 'localhost:9200/_cluster/health?pretty'

### Delete Indices

/usr/bin/curator_cli --host localhost delete_indices --filter_list '[{"filtertype":"age","source":"creation_date","direction":"older","unit":"days","unit_count":90},{"filtertype":"kibana"},{"filtertype":"pattern","kind":"prefix","value":"bucket-","exclude":"true"}]'

### Show Indices

/usr/bin/curator_cli --host localhost show_indices --filter_list '[{"filtertype":"kibana"},{"filtertype":"pattern","kind":"prefix","value":"api-","exclude":"false"}]'

### Listing Index's Fields

curl -XGET 'localhost:9200/api-*/_mapping?pretty'


### Shards Status

curl -XGE 'localhost:9200/_cat/shards'


### No Shards Replicas

curl -XPUT 'localhost:9200/_settings' -H'Content-Type: application/json' -d '
{
    "index" : {
        "number_of_replicas" : 0
    }
}'

### Allocate Shards

curl -XPUT -H'Content-Type: application/json' 127.0.0.1:9200/_cluster/settings?pretty -d '{
"persistent" : {
"cluster.routing.allocation.enable" : "all"
    }
}'


### Find UNASSIGNED Shards

curl -XPUT -d '{​​​​​​​​"index":{​​​​​​​​"number_of_replicas":1}​​​​​​​​}​​​​​​​​' -H "Content-Type:application/json"  http://umgsvrmesln01:30040/zipkin:span-2020-10-08/_settings

### Delete Shards

for i in `curl  http://umgsvrmesln01:30040/_cat/shards | grep UNASSIGNED | awk '{​​​​​​​​print $1}​​​​​​​​'`; do curl -XPUT -d '{​​​​​​​​"index":{​​​​​​​​"number_of_replicas":1}​​​​​​​​}​​​​​​​​' -H "Content-Type:application/json"  http://umgsvrmesln01:30040/$i/_settings; done


for i in `curl localhost:9200/_cat/shards | grep UNASSIGNED | awk '{print $1}'`; do curl -XPUT -d '{"index":{"number_of_replicas":1}}' -H "Content-Type:application/json" localhost:9200/$i/_settings; done