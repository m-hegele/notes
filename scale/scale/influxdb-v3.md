
# InfluxDB v3

built on FDAP stack:

- Flight: columnar data transfer
- DataFusion: high-performance querying
- Arrow: optimized in-memory columnar analytics
- Parquet: high-compression storage

Storage costs down 90% compared to v1
- v1 requires SSD
- v3 can work on S3


Variants:
- Core: open source 
- Enterprise: self-managed, HA
- Cloud Serverless: Fully managed, Pay by use
- Cloud Dedicated: dedicated infrastructure
- Clustered: scale horizontally
- Edge: Its storage system is designed to organize data in bulk chunks that can be quickly processed and kept in highly compressed Parquet files. This means that it is optimized for queries against the leading edge of data and time series and analytic queries in particular. InfluxDB 3 Edge will not include a compactor for re-organizing the data for deletes or query optimization over longer time periods, which means its sweet spot will be for collecting and querying recent data.
    - never released?
- Community: supposed to be successory of v1 and v2, not released

# just stick with v1 (OSS) and scale the server?

https://docs.influxdata.com/influxdb/v1/guides/hardware_sizing/

our metrics: https://marge.chargehere.de/grafana/d/Ekiwl0Jmz/influxdb-oss-stats-monitoring-dashboard?var-Interval=$__auto&orgId=1&from=now-7d&to=now&timezone=browser&var-datasource=fd291221-08f7-4d53-be47-8723731b9bc1&var-hostname=$__all

If your InfluxDB performance requires any of the following, a single node (InfluxDB OSS) may not support your needs:

- more than 750,000 field writes per second: 
    - we have ~ 175 writes requests / minute
    - we have ~ 46.000 point throughput per minute = 766 point throughput per second

- more than 100 moderate queries per second (see Query guides)
    - we have ~ 175 writes requests / minute
    - peak: 125 read requests / minute

- more than 10,000,000 series cardinality
    - monitoring: 75 K series cardinality



Other stats:
    - HTTP request 99th percentile:
        - write 30 ms
        - read: 836 ms


marge aktuell: 
- 4 Kerne
- RAM: 13.3 GB von 15.6 GB
    - InfluxDB = 65% = 8.64 GB
- SSD IOPS?

Ineffiziente Queries auf ChargeHere B34 Information Board (Analytics)
- [jede halbe Stunde (Interval Info Dashboard eine sehr langsame Query mit 4s)](https://marge.chargehere.de/grafana/d/Ekiwl0Jmz/influxdb-oss-stats-monitoring-dashboard?var-Interval=1m&orgId=1&from=now-3h&to=now&timezone=browser&var-datasource=fd291221-08f7-4d53-be47-8723731b9bc1&var-hostname=$__all&viewPanel=panel-9)
- Vorberechnung mit continuous queries
    - must include a GROUP BY time
- separation of databases for monitoring and for analytics use case

Glossary:
- bucket = database + retention policy