# Installation

SanteMPI is installed and configured in an identical manner to the [SanteDB iCDR ](../installation/installation/)Installation. This section will only discuss the delta (differences) between installing SanteDB iCDR ad dCDR.

## Docker Containers

The `santedb-mpi `docker container is derived from the [SanteDB iCDR docker container](../installation/installation/santedb-server/docker-containers/#santempi-application). When using SanteMPI you should reference the `santedb-mpi:latest` docker image.

```
version: "3.3"

services:
  db:
    image: postgres
    container_name: sdb-postgres
    ports:
      - "5432:5432"
    environment:
      POSTGRES_USER: santedb
      POSTGRES_PASSWORD: SanteDB123
    restart: always

  santedb:
    image: santesuite/santedb-mpi:latest
    container_name: santedb-mpi
    environment:
      - SDB_FEATURE=LOG;DATA_POLICY;AUDIT_REPO;ADO;PUBSUB_ADO;RAMCACHE;SEC;SWAGGER;OPENID;FHIR;HL7;HDSI;AMI;BIS;MDM;MATCHING;IHE_PIXM;IHE_PDQM;IHE_PMIR;IHE_PIX;IHE_PDQ
      - SDB_MATCHING_MODE=WEIGHTED
      - SDB_MDM_RESOURCE=Patient=org.santedb.matching.patient.default
      - SDB_MDM_AUTO_MERGE=false
      - SDB_DB_MAIN=server=sdb-postgres;port=5432; database=santedb; user id=santedb; password=SanteDB123; pooling=true; MinPoolSize=5; MaxPoolSize=15; Timeout=60;
      - SDB_DB_AUDIT=server=sdb-postgres;port=5432; database=auditdb; user id=santedb; password=SanteDB123; pooling=true; MinPoolSize=5; MaxPoolSize=15; Timeout=60;
      - SDB_DB_MAIN_PROVIDER=Npgsql
      - SDB_DB_AUDIT_PROVIDER=Npgsql
      - SDB_DATA_POLICY_ACTION=HIDE
      - SDB_DELAY_START=5000
    ports:
      - "8080:8080"
      - "2100:2100"
    depends_on:
      - db
    restart: always
```

### MPI Docker Features

The SanteMPI docker containers add five new features in the `SDB_FEATURE` environment variable.

| IHE\_PIX  | Enables the HL7v2 Patient Identity Cross Referencing features in SanteMPI (ITI-8 and ITI-9)                                                        |
| --------- | -------------------------------------------------------------------------------------------------------------------------------------------------- |
| IHE\_PDQ  | Enables the HL7v2 Patient Demographics Query features in SanteMPI (ITI-21)                                                                         |
| IHE\_PMIR | Enables the IHE Patient Master Identity Registry (PMIR) FHIR services on the docker container.                                                     |
| IHE\_PDQm | Enables the IHE Patient Demographics Query for Mobile FHIR behaviors (specifically the mothersMaidentName extension and error condition behaviors) |
| IHE\_PIXm | Enables the IHE Patient Identity Cross-Reference Manager FHIR behaviors (specifically the cross referencing operation)                             |

## Microsoft Windows Operating Systems

The setup procedure is identical to SanteDB iCDR on Windows Operating Systems. The major differentiator is that the [Configuration Tool](../operations/system-administration/host-administration/configuration-tool/#template) Template for **SanteMPI Server **should be selected on initial configuration. This template:

* Configures the necessary HL7v2 handlers to use PIX and PDQ specified behaviors.
* Configures the necessary FHIR extensions and profiles for PIXm, PDQm and PMIR
* Enables Master Data Management services
