# Software Architecture

The SanteDB iCDR, dCDR and its related components are designed in a modular fashion. These modules are intended to maximize code reuse, and provide consistent services across the iCDR and dCDR environments. 

## Service Architecture

SanteDB uses the service locator pattern \([https://en.wikipedia.org/wiki/Service\_locator\_pattern](https://en.wikipedia.org/wiki/Service_locator_pattern)\) via the IServiceProvider instance called  the ApplicationContext. The application context is responsible for loading the appropriate implementation \(or provider\) of a particular strategy \(or contract\) based on the configuration of the environment. 

Take, for example, the auditing which is implemented as:

![](../../.gitbook/assets/image%20%28174%29.png)

Here, the SecretClass instance relies on the contract IRepositoryService, which may be implemented by an ADO.NET implementation, an RFC3881 implementation and a FHIR implementation. At runtime, when SecretClass wishes to send an audit, it will call the ApplicationServiceContext instance, which will return an appropriate implementation based on the runtime environment.

![](../../.gitbook/assets/image%20%28176%29.png)

This means that the implementer of SecretClass doesn't need to worry about which audit service is being used, it merely executes the business function for auditing.

This service pattern, and the fact the solution is implemented in .NET Standard, means that most service implementations can be used in the iCDR and dCDR environments without re-compiling.

{% hint style="info" %}
Dependency Injection from the ApplicationServiceContext is being implemented and should be available in future releases of SanteDB's core libraries.
{% endhint %}

## Service Relationships

SanteDB's overall architecture is really a composition of services which have been configured by the developer of the SanteDB solution. For example, SanteMPI may have a different series of services configured to act as an MPI whereas SanteIMS will have different services configured to behave as an EIR \(however the two would share services\).

Most SanteDB services are implemented assuming a service relationship as illustrated below:

![](../../.gitbook/assets/image%20%28173%29.png)

### Messaging Services

Messaging services represent the primary presentation layer for SanteDB. These services are responsible for:

* Handling transport layer security \(authentication of clients, tokens, decrypting network traffic, etc.\)
* Translating messages from a wire-level format \(like HL7, FHIR, GS1\) into the common information model \(RIM\)
* Performing auditing based on the requirements of the transport standard
* Translating responses into appropriate behaviors \(like a NACK in HL7v2 or a 422 in HTTP\)

### Auditing Services

The auditing services in SanteDB are responsible for facilitating the audit process. This process in SanteDB includes:

* Storing a local copy of the audit information within the SanteDB service \(this is really a repository service\)
* Shipping appropriate audits to centralized infrastructure as required

### Repository Services

In SanteDB, the repository service layer is responsible for the "behaviors", or the coordination activities to accomplish a particular task. Repository services:

* Ensure that the appropriate authentication context is established and used / shared
* Use the policy enforcement mechanism to demand appropriate permission to perform an action
* Call necessary business rule triggers for the action being executed
* Raise pre/post events which event listeners may use to perform extended behaviors \(for example, the MDM layer is implemented in this manner\)
* Interacting with the data persistence services to store/read data

Messaging services primarily interact with repository services as these services are responsible for abstracting the individual data layer calls.

### Policy Enforcement Services

The policy services in SanteDB consist of:

* Policy Information Service - Which stores information about security and data policies in SanteDB such as whether the policy can be overridden, and its place in the policy hierarchy.
* Policy Decision Service - Which determines appropriate access decisions \(GRANT, ELEVATE, DENY\) given a securable \(the thing which is being done or acted on\) and the principal \(the user, app, and device being used\).
* Policy Enforcement Service - Which takes appropriate actions based on the outcome of the policy decision made. This might be masking data, throwing an exception, etc.

{% hint style="info" %}
SanteDB is based on OpenIZ which was written in .NET PCL. This means some interfaces in SanteDB use declarative policy demands \(via CAS\) while others use imperative policy demands \(via the IPolicyEnforcementService\). 
{% endhint %}

### Business Rule Services

Business rule services are specialized interfaces which can be chained together and act on data before and after a repository service actions it. Business rule services are user defined behaviors and have the ability to:

* Validate an object before it is acted on
* Modify an object prior to an action \(insert, update, etc.\) being performed
* Call other services \(like notifying another system, etc.\) 
* Modify and/or manipulate an object prior to the object being returned to the caller of the repository action \(after persisted but before returning\).

### Data Persistence Services

The data persistence services are typically the "last place" where services in SanteDB can interact with data. Unless services require direct access to the underlying storage technology, all interactions occur via these services. Data persistence services are responsible for:

* Translating object to and from the information model into appropriate storage models \(SQL tablets, FHIR objects, etc.\)
* Transactional control of the underlying storage technology \(commit, rollback, etc.\)
* Managing and interacting with the caching services to reduce load on the persistence technology

### Caching Services

The caching services are responsible for providing rapid access to cached objects, these services \(like REDIS or Memory Caching\) reduce load on the persistence layer as they typically provide rapid, non-relational access to models in the information object.

### ORM Providers

The object-relational-model providers are specialized classes which are used \(optionally\) by services which must directly interact with database software, however require abstraction on the persistence technology. ORM providers which exist in SanteDB include: PostgreSQL, Firebird, and SQLite, and are responsible for:

* Translating object/relational LINQ queries into appropriate SQL syntax for the storage technology
* Mapping logical keywords and operators to physical operators in SQL \(for example: .Contains\(\) becomes ILIKE in PostgreSQL but LIKE in Firebird\)
* Committing and rolling back transactions with the database provider
* Constructing dynamic SQL operations for result sets for order, count, etc.

### Business Intelligence Services

The BI services in SanteDB are responsible for interacting with the ORM providers to execute business intelligence assets \(queries, views, parameters, reports, etc.\) directly with the various connected SQL databases for the service.

### Synchronization Services

Synchronization services are responsible for integrating the SanteDB iCDR and dCDR with upstream services. These services:

* Manage the inbound/outbound and dead letter queues for synchronizations
* Interact with the persistence layer \(bypassing business rules which may already be executed\) directly
* Manage the retry and conflict resolution notifications process

### Additional Services

SanteDB contains hundreds of service contracts for various system tasks which are not covered at a high level on this page. These services can be found on the [Service Definitions](../extending-santedb/server-plugins/service-definitions/) page.

