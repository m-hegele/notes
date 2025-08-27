# TimescaleDB

TODO:
- [ ] migrations

Why?

- scalability of InfluxDB v1
- pricing of InfluxDB v3
- Combining relational and timeseries data 
- Proper SQL > InfluxQL / Flux

Existing InfluxDB-based infrastructure

- gathering data: local InfluxDB + telegraf
- Kapacitor
  - aggregate and write data
    - charging sessions (maybe obsolete)
    - reliability metric
  - alerting
    - includes creating Jira tickets from Tick scripts


Kapacitor alternatives for TimescaleDB

- aggregation:
  - continuous aggregates = views (hourly / daily rollups), can be queried like normal tables
  - pg_cron: SQL on a schedule
- alerting: Grafana alerts
  - Webhook + Jira API for alerts


Kapacitor tasks

| ID                        | Type |
|---------------------------|------|
| backendConnection         |      |
| chargePointConnection     |      |
| chargingProcessSummarizer | agg  |
| connectorAlertsByHour     | agg  |
| cpuChargePoint            |      |
| cpuHost                   |      |
| dhcpService               |      |
| discChargePoint           |      |
| discHost                  |      |
| errorConnector            |      |
| fiTrigger                 |      |
| hostHeartbeat             |      |
| influxdbService           |      |
| logChargePoint            |      |
| manyStateChanges          |      |
| memoryChargePoint         |      |
| memoryHost                |      |
| noOaksystemService        |      |
| ntpService                |      |
| oaksystemService          |      |
| occupiedConnectors        |      |
| ocppproxyService          |      |
| temperatureChargePoint    |      |
| temperatureHost           |      |
