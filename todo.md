## In Progress


- Prometheus vs. InfluxDB vs. TimescaleDB
- Mention local InfluxDB: https://www.influxdata.com/products/influxdb-edge-data-replication/

- Query timeouts

- RevPi 4: https://revolutionpi.com/shop/en/revpi-connect4 459 statt 415
- BA Kai    
-  marge: Sep 10 15:38:15 marge influxd-systemd-start.sh[620]: ts=2025-09-10T13:38:15.953191Z lvl=info msg="Post http://127.0.0.1:8186/write?consistency=&db=monitoring&precision=ns&rp=autogen: dial tcp 127.0.0.1:8186: connect: connection refused" log_id=0wdqfe3G000 service=subscriber


## My Day

- [ ] alle Repos über HTTPS

## Long List

- [ ] Keba tauschen 
- [ ] Mender Liste: paul (AEB), paulina (WiBu) 
- [ ] Wünsche asyncio Schulung 

- [ ] always set -o vi
- [ ] `tach-check` is slow -> action instead of pre-commit hook?
- [ ] Doku: tcpdump und DHCP Logs 
- [ ] Dojo: Skalierbarkeit 
- [ ] OJR Definition 
- [ ] Rollendefinition 
- [ ] Dojo: logging module (hierarchies) 
- [ ] Dojo: functional python: frozen dataclass, Option, Result, reduce / compose 
- [ ] SOLID an unserer Code Base Dojo Session 
- [ ] asyncio pitfalls + ruff rules + BlockingTask, InterruptibleTask und TaskSetManager Dojo session 
    - pit falls: not re-creating coroutines 


## Done

### 03.09.25

- [x] get tests to pass
- [x] suspended_current = 1A
- [x] UI Change Projekt: Beauftragung 

### 04.09.25

- [x] Anleitung: WSL Turn on feature

- [x] Kann man sich das Sender der EVSE-ID an die Oakbox sparen (Ein Konfig-Parameter weniger)? BMP
- [x] EVSE-ID vom Backend kriegen? Wahrscheinlich nicht

- [x] Update elinor
- [x] Test Real Current detection
- [x] Test SuspendedEV mit Keba
- [x] Test VPN Client (CHC-883)
- [x] Fix Test plan with BRUSA

## 05.09.25

- [x] Backlog-Pflege
- [x] die Capacity-Group-Sum wird jetzt wieder zu selten geloggt. Es sieht so aus als wäre Capacity Group 1 5 Minuten lang überlastet gewesen, es waren aber nur wenige Sekunden. Das sieht man am EMS-Signal
- [x] Aakarsh Review
- [x] der Alpi ging initial wieder kurz in eine Überlast, weil das Transaction Profile nicht gesetzt wurde, nachdem der Alpi den BootNotificaiton-Trigger rejected hat. In dem Fall sollten wir wohl trotzdem synchronize_config anstoßen
- [x] Fix EMS tests: `RuntimeError: Runner.run() cannot be called from a running event loop`
- [x] allow_offline_tx (+ Epic Eintrag für globalen Konfig-Parameter)
- [x] VSCode profile for notes

## 08.09.25
- [x] Rebuild post uv resolution fixes
- [x] Update mira
- [x] Release Notes updaten
- [x] BANF Mender
- [x] Automatische Simulations Tests: Epic
- [x] Testing EPIC: Perfomance Tests 
- [x] merge back release
- [x] Aakarsh: re-added `allow_offline_tx_for_unknown_id`
- [x] Klären: Vertretung für Testing mit Brusa: neues Task? https://chargehere.atlassian.net/browse/CHC-915