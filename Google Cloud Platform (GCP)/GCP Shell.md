
### Service Identities
Services identities can be created with `gcloud beta services identity create`, with the tag `--service={service}.googleapis.com` to specify the service. 

## BigQuery

BigQuery can be used with `bq` commands, such as `bq mk {dataset}` to create a new dataset. 
Here's another example:
```shell
bq mk \
--time_partitioning_field timestamp \
--schema ride_id:string,point_idx:integer,latitude:float,longitude:float,\
timestamp:timestamp,meter_reading:float,meter_increment:float,ride_status:string,\
passenger_count:integer -t taxirides.realtime
```
More details can be found on the [official BQ CMD docs](https://cloud.google.com/bigquery/docs/reference/bq-cli-reference).
The bucket can be created with `export BUCKET_NAME={bucket_name}` and `gsutil mb gs://$BUCKET_NAME/`.

An example for running a dataflow template:
```shell
gcloud dataflow jobs run iotflow \
    --gcs-location gs://dataflow-templates-us-east1/latest/PubSub_to_BigQuery \
    --region us-east1 \
    --worker-machine-type e2-medium \
    --staging-location gs://qwiklabs-gcp-03-15ae07c6740c/temp \
    --parameters inputTopic=projects/pubsub-public-data/topics/taxirides-realtime,outputTableSpec=qwiklabs-gcp-03-15ae07c6740c:taxirides.realtime
```

## 