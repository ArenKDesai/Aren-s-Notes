#CS544 #Cloud #GoogleCloud #UWMadison #BigQuery

### VMs
Multi-tenant hosts are VMs with multiple customers, sole-tenant are VMs what all share one customer

## BigQuery
- When doing a query, the ```FROM``` clause has to have an ```AS``` statement since you can't typically reference the dataset itself. For example, 
```SQL
FROM 'bigquery-public-data.geo_us.boundaries.counties' AS counties
```
