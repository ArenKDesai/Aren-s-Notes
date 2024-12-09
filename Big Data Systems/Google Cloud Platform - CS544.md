#CS544 #Cloud #GoogleCloud #UWMadison #BigQuery

## Compute
### VMs
Virtual machines that you can specify GPU type, number of GPUs, machine type, etc. 
Multi-tenant hosts are VMs with multiple customers, sole-tenant are VMs what all share one customer. 
#### Billing Models
VM deployment has on-demand instances of a constant high price and spot instances.
The billing models include fixed, auto scaling (cloud detects high/low load and scales), or pay-as-you-go with fine-

## Memory
IaaS - Memory oriented and optimized, more expensive but more freedom. 
PaaS - full service. Less freedom, cheaper. Caches rows. 

## Storage
HDDs and SDDs, price depends on size and type

## Network
Continents > regions > zones
A region is a data center consisting of 1 or more buildings. Zones are regions, so certain subsets of one data center are certain zones. 
Ingress (data coming in) is usually free, egress (data going out) you pay for. It also depends on internet, continent, region, zone, etc. 



## BigQuery
- When doing a query, the ```FROM``` clause has to have an ```AS``` statement since you can't typically reference the dataset itself. For example, 
```SQL
FROM 'bigquery-public-data.geo_us.boundaries.counties' AS counties
```
BigQuery uses Colossus Storage, so that is what's billed. 

