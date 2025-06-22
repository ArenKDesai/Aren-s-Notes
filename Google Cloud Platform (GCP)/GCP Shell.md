Services identities can be created with `gcloud beta services identity create`, with the tag `--service={service}.googleapis.com` to specify the service. 

BigQuery can be used with `bq` commands, such as `bq mk {dataset}` to create a new dataset. 
Here's another example:
```shell
bq mk \
--time_partitioning_field timestamp \
--schema ride_id:string,point_idx:integer,latitude:float,longitude:float,\
timestamp:timestamp,meter_reading:float,meter_increment:float,ride_status:string,\
passenger_count:integer -t taxirides.realtime
```