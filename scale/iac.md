# IaC & Cloud

- OpenTofu
- FinOps mit IaC
- KRITIS?
- Flux für Kubernetes
- OpenLense
- GitOps
- Portainer


## OnePlatform

- gibt uns einen/mehrere AWS / Azure Account
- Abrechnung
- Standard-Policies
- kein managed Kubernetes (mehr)

## IAM

Entra ID Application: z.B. Mender / Grafana

Entra ID Technical User: für Pipelines

Entra ID Administrative Unit: eigener AD Space mit EnBW-unabhängigen Accounts

Entra ID Group: neue Gruppe für EnBW user

IAM AD Tenant mit eigenen Usern (inkl. extern)
Azure Entra

für
- Grafana
- Mender
- Config-Tool (FastAPI middlewares, AuthN)

## Runtime


Kubernetes vs. Container Runtime
- Konfiguration der Anwendung
    - Kube: Config Maps
    - ECS: eigenes Image

Bevorzugt: Container Runtime
- Spec-Definition: aws_ecs_cluster + aws_ecs_task_definition
- horizontal Skalieren
- Connecting containers: VPC
- von außen zugreifen: Load balancer
- storage: 
    - block storage (EWS)
        - kein prefixing möglich
        - resizing nötig
        - i.d.R. nicht zu nutzen
    - object storage (S3) = überall gleich, Anbindung über VPC
        - prefixed z.B. nach location
        - resizing nicht nötig
- cpu definition: Zeit, nicht Kerne
    - 1 = jede 100 ms hab ich 100 ms Zeit
    - throttling möglich
        - wenn ja: zu viele threads?
        - oder: allgmeine mehr zu rechnen

Deployment in ECS:
- One repo: version als input für terraform
- zwei repos: software & ops komplizierter

## Services

- InfluxDB
- Grafana
- Mender
- Packages & Images
- Aggregationsplattform
- Inventory DB (?)

## Off-Topic

Mender Hosted on AWS / Azure?

