# Prometheus

## Prometheus vs. OpenTelemetry

telemetry: agent scraped /metrics mit pull und macht push statt pull

Telemetry: three pillars
- metrics
- logs strukturiert
- distributed tracing (pro request - was synchrones)



## Prometheus vs. InfluxDB

Differences

- Write model: Prometheus: pull, InfluxDB = push
    - => InfluxDB better for irregular measurements
- InfluxDB is optimized for long-term storage



Prometheus ist besser, wenn:
    Du primär Monitoring und Alerting brauchst.
    Deine Daten in festen Intervallen gesammelt werden.
    Du ein einfaches Setup bevorzugst.

InfluxDB ist besser, wenn:
    Du komplexe Analysen und Langzeit-Speicherung brauchst.
    Deine Daten unregelmäßig eintreffen.
    Du mit großen Datenmengen arbeitest oder detaillierte Energieverbrauchsanalysen machen willst.


Vorteil gegenüber InfluxDB:
- alert rules
- built for monitoring
- kann die meisten Anwendungen überwachen (via Open metrics format)
    - hat man "sowieso am laufen" (?)
- alert manager

Nachteil
- unterschiedliche buckets mit unterschiedlichen Auflösungen (downsampling)

Alertmanager von Prometheus + InfluxDB?
- influxdb_exporter 

Warum kein Grafana Alerts? Berechnung der Verfügbarkeitskennzahl für Alerting: wir wollen duplizierte Definition von Alerts vermeiden