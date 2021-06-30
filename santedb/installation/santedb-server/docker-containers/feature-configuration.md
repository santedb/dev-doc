# Feature Configuration

## Core Services \(Recommended\)

### Diagnostic Logging

The diagnostic logging feature allows for logging to files, the console, or even via the trace writer in Mono. These settings provide access to the [Diagnostics Configuration ](../../../operations/host-administration/host-configuration-file/diagnostics-configuration.md)subsystem. 

```text
SDB_FEATURE=...;LOG;...
# Set the Logging Level
SDB_LOG_LEVEL=Error|Warning|Informational|LogAlways
```

### Data Privacy Controls

The privacy control services actively apply privacy policy protections on outbound messages, and ensure that inbound messages meet the minimum policy level for updating/creating records. For example, this service ensures that masked data, or sensitive data which may be inaccurate \(given the submitter's policy set\) cannot be recorded, and that any data is masked/hidden from the underlying repository.

```text
SDB_FEATURE=...;DATA_POLICY;...
# Set the action to apply when sensitive data is disclosed
SDB_DATA_POLICY_ACTION=hide|redact|nullify|error|audit|none
# Set the resources on which policies should be applied
SDB_DATA_POLICY_RESOURCE=AssigningAuthority|Patient|Person|Place|Observation|...
```

### Audit Repository

The audit repository feature enables the local audit repository on SanteSuite, meaning that audits are stored in the specified audit database.

```text
SDB_FEATURE=...;AUDIT_REPO;...
# Sets the RW connection
SDB_AUDIT_REPO_RW_CONNECTION=connection
# Create Connection Strings
SDB_DB_connection_PROVIDER=Npgsql
SDB_DB_connection=server=x;password=y;
```

### ADO Data Storage

The ADO data storage service should be enabled if you plan on using the PostgresSQL or another supported database to store data. 

```text
SDB_FEATURE=...;ADO;...
# Sets the Read/Write Master Connection
SDB_ADO_RW_CONNECTION=rwconnection
SDB_DB_rwconnection_PROVIDER=Npgsql
SDB_DB_rwconnection=server=x;password=y
# Sets the Read only Secondary Connection
SDB_ADO_RO_CONNECTION=roconnection
SDB_DB_roconnection_PROVIDER=Npgsql
SDB_DB_roconnection=server=x;password=y
# Set whether the provider will use fuzzy totals
# using fuzzy totals increases performance and merely indicates "another page is available"
# rather than counting the total result set size
SDB_ADO_FUZZY_TOTAL=true|false
```

{% hint style="info" %}
You can swap the SanteDB core storage technology to another technology, in this case do not use the ADO data storage feature.
{% endhint %}

### In-Memory Caching

The in-memory caching feature instructs the iCDR container to use a local RAM-based cache \(non-shared\) for data operations.

```text
SDB_FEATURE=...;RAMCACHE;...
# The time that cache entries should remain cached before RAM is cleaned
# in the format DAYS.HOURS:MINUTES:SECS
SDB_RAMCACHE_TTL=0.1:0:0
```

### REDIS Caching

The REDIS caching feature instructs the iCDR container to use a shared REDIS cache for data operations.

```text
SDB_FEATURE=...;REDIS;...
# The time that cache entries should remain cached before RAM is cleaned
SDB_REDIS_TTL=0.1:0:0
# The address/port of the REDIS server
SDB_REDIS_SERVER=server:port
```

### Core Security Services

The core security services should always be enabled, unless you're running a heavily customized version of the iCDR software which supplies its own security services.

```text
SDB_FEATURE=...;SEC;...
# The password validation/complexity validation regex
SDB_SEC_PWD_REGEX=regular expression
# The length of sessions issued by the service
SDB_SEC_POL_SESSION=0.1:0:0
# The number of invalid authentications before a user/device/application is locked
SDB_SEC_POL_LOCK=4
# Sets the secrets for the SanteDB data signing services
# You can specify either HS256, RS256 or RS512 signing algorithms
# Note: You will need to customize your own SanteDB iCDR instance with a custom
#       dockerfile if you choose to use RS256 as the certs need to be installed
#       into the mono keystore.
SDB_SIG_default=hs256:A_SECRET_PASSPHRASE_FOR_HMAC256_DATA_SIGNATURES
SDB_SIG_other=rs256:THUMBPRINT_OF_YOUR_RSA_CERT

```

### OpenID Connect IDP

The OpenID Connect IDP service enables the [OpenID Identity Provider](../../../extending-santedb/service-apis/openid-connect/) services.

```text
SDB_FEATURE=...;OPENID;...
# One or more claims which client systems can send. Default are:
# scope;PolicyOverride;ResourceId;PurposeOfUse;FacilityId;OrganizationId
SDB_OPENID_CLAIMS=scope;PolicyOverride;PurposeOfUse
# If you need to use a custom token type
SDB_OPENID_TOKEN=bearer
# When true, allows client_credentials grant without sending an 
# X-Device-Authorization header or an X509 client certificate
SDB_OPENID_INSECURE_CLIENT_AUTH=true|false
# The issuer ID of this IdP
SDB_OPENID_ISSUER=myrealm
# The key to use for signing the JWT key. Note: When using HMAC256
# the client secret is used to sign the JWT
SDB_OPENID_JWT_SIG_KEY=xxxx
# Set the address (port/url) where OpenID should be available
SDB_OPENID_LISTEN=http://0.0.0.0:8080/auth
```

### Core Health Data Service Interface

The core HDSI interface should always be enabled if you plan on using any of the SanteDB dCDR services. If you are just using the iCDR for other interfaces, you can disable this interface.

```text
SDB_FEATURE=...;HDSI;...
# The base URL where the HDSI should be bound
SDB_HDSI_LISTEN=http://0.0.0.0:8080/hdsi
# The authentication scheme to use for the HDSI
SDB_HDSI_AUTH=TOKEN|BASIC|NONE
# Enables or disables CORS
SDB_HDSI_CORS=true|false
```

### Core Administrative Management Interface

The core AMI interface should always be enabled if you plan on using any of the SanteDB dCDR services or services like the admin console which require API access. If you are just using the iCDR for other interfaces, and have no need to create users, policies, or other assets.

```text
SDB_FEATURE=...;AMI;...
# The base URL where the AMI should be bound
SDB_AMI_LISTEN=http://0.0.0.0:8080/ami
# The authentication scheme to use for the AMI
SDB_AMI_AUTH=TOKEN|BASIC|NONE
# Enables or disables CORS
SDB_AMI_CORS=true|false
```

### Core Business Intelligence Interfaces

The core BI services allow third party solutions to query and execute reports on the SanteDB server, as well as FHIR MeasureReport resources. 

```text
SDB_FEATURE=...;BIS;...
# The base URL where the AMI should be bound
SDB_BIS_LISTEN=http://0.0.0.0:8080/bis
# The authentication scheme to use for the BIS
SDB_BIS_AUTH=TOKEN|BASIC|NONE
# Enables or disables CORS
SDB_BIS_CORS=true|false
```

## Optional Services

### HL7 Fast Health Interoperability Resources \(FHIR\)

SanteDB's FHIR resources are enabled using the FHIR feature. The FHIR feature controls the exposed resources \(to minimize surface area\), location and options for FHIR.

```text
SDB_FEATURE=...;FHIR;...
# The base URL where the FHIR should be bound
SDB_FHIR_LISTEN=http://0.0.0.0:8080/fhir
# The authentication scheme to use for the FHIR
SDB_FHIR_AUTH=TOKEN|BASIC|NONE
# Enables or disables CORS
SDB_FHIR_CORS=true|false
# When emitting links for references, the external URL to use
SDB_FHIR_BASE=http://external-url/fhir
# The resources which should be exposed on the FHIR interface
SDB_FHIR_RESOURCE=Patient;Practitioner;Organization;...
```

### HL7 Version 2.x 

The HL7 Version 2.x interface allows the iCDR docker container to expose HL7 LLP or SLLP traffic to trading partners.

```text
SDB_FEATURE=...;HL7;...
# Indicates how the sending application should be authenticated.
# Note: When using SLLP the client certificate is used to authenticate the device
# .     this setting impacts how the application is authenticated.
# Note: When using regular LLP, the client and device are authenticated using this
#       mechanism
# Values:
#    MSH8 - Device authentication occurs via SSL
#           if regular LLP, device authentication occurs via MSH-3|MSH-4 and MSH-8
#    SFT4 - Device authentication occurs via SSL
#           if regular LLP, device authentication occurs via MSH-4 and MSH-8
#           and application authentication occurs via SFT-4 
SDB_HL7_AUTHENTICATION=MSH8|SFT4|NONE
# The namespace ID where internal UUIDs for patients are exposed (if opted)
SDB_HL7_LOCAL_DOMAIN=MY_DOMAIN
# If PID segment field for SSN is used, maps the value in that field to a domain
SDB_HL7_SSN_DOMAIN=SSN
# The port and protocol to listen on
#    LLP = Unsecure LLP
#    SLLP = SSL + LLP
#    TCP = TCP stream only
# The bind port is also specified here.
SDB_HL7_LISTEN=llp://0.0.0.0:2100
# The amount of time to keep the TCP channel open after sending a response
# this is used in batch or streaming mode.
SDB_HL7_TIMEOUT=100
# If using SLLP, this is thumbprint of the server's certificate
SDB_HL7_SERVER_CERT=thumbprint
# If using SLLP with client authentication via TLS, this is the thumbprint
# of a CA or chain to use for client authentication
SDB_HL7_CLIENT_AUTH=thumbprint
```

### Publish / Subscribe Functions

The pubsub feature enables the structured message notification system. This allows third party systems to setup standing queries which SanteDB will "notify" them of whenever new data becomes available.

```text
SDB_FEATURE=...;PUBSUB_ADO;...
# If the pub-sub subscriptions are being stored in a database different
# than the main database , indicate the name of the connection string here
SDB_PUBSUB_ADO_RW_CONNECTION=connectionString
```

### Record Matching Plugin

The record matching plugin registers the [SanteDB Matcher ](../../../../santempi/matching-engine/)plugin in the container. This service is used by other services to match and/or merge data.

```text
SDB_FEATURE=...;MATCHING;...
SDB_MATCHING_MODE=WEIGHTED|SIMPLE
```

The matching modes supported are:

* SIMPLE: Simple matching only performs block operations against the database, and performs no scoring. This mode is useful when your duplication detection is light. Records are given a score of 0.0 \(not match\) or 1.0 \(match\)
* WEIGHTED: Weighted matching uses the SanteDB Matching plugin to perform scoring. 

When composing your own image from SanteMPI you can copy match configurations to the ./match directory:

```text
FROM santesuite/santedb-mpi:latest
COPY ./my_match_config.xml /santedb/match/my_match_config.xml
```

### Master Data Management & Record Linking

The MDM feature sets up the MDM resource persistence strategy and subscribes one or more resources to one or more match configurations.

{% hint style="info" %}
When enabling the MDM service, you must also enable the MATCHING service.
{% endhint %}

```text
SDB_FEATURE=...;MDM;...
SDB_MDM_RESOURCE=Resource=Configuration;Resource=Configuration
SDB_MDM_AUTO_MERGE=true|false
```

The supported resources for MDM management are:

| Resource | Description |
| :--- | :--- |
| Person | Places any entity of type Person or its subclasses \(Provider / Patient\) under MDM storage management. |
| Patient | Places any entity of type Patient into MDM storage management. This is useful for Master Patient Index or Client Registry scenarios. |
| Provider | Places any entity of type Provider into MDM storage management. This is useful for centralized Provider Registries. |
| Material | Places any entity of Material or ManufacturedMaterial into MDM storage management. This includes kinds and instances of materials. Useful for centralized product registries. |
| ManufacturedMaterial | Places only ManufacturedMaterials into MDM storage management. |
| Place | Places the Place resource into MDM storage management. This is useful for centralized Geographic or Facility Registries |
| Organization | Organizations \(such as companies, government agencies, etc.\) in MDM control. |

## SanteMPI Features

You can enable specific SanteMPI features by enabling the `IHE_*` interfaces on the `santedb-mpi` container.

### IHE PIX for Mobile

To enable the `$ihe-pix` operation in the container:

```text
SDB_FEATURE=...;IHE_PIXM;...
```

### IHE PDQ for Mobile

To enable the PDQm behaviors on the `/Patient` resource:

```text
SDB_FEATURE=...;IHE_PDQM;...
```

### IHE PMIR Feature

To enable the `urn:ihe:iti:pmir:2019:patient-feed` operation:

```text
SDB_FEATURE=...;IHE_PMIR;...
```

