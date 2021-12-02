# Reviewing Audits

SanteDB iCDR and dCDR instances implement a local [iauditrepositoryservice.md](../../../../developers/server-plugins/service-definitions/security-services/auditing-services/iauditrepositoryservice.md "mention")where local audits are stored for events related to SanteDB , as well as an [iauditdispatchservice.md](../../../../developers/server-plugins/service-definitions/security-services/auditing-services/iauditdispatchservice.md "mention")which is responsible for shipping audits to a centralized audit repository (if the iCDR or dCDR are participating in an OpenHIE instance).

In the SanteDB administrative panel, audits are accessed using the `Audit Repository` function in the `Security` section of the Administrative Panel.&#x20;

## Audit List

The audit list provides an overview of the complete audit trail available in the SanteDB iCDR or dCDR instance to which the administrative panel is connected.&#x20;

![](<../../../../.gitbook/assets/image (428).png>)

Audits are displayed with the event summary fields visible.

### Action

The action field in an Audit indicates the overall operation which was performed which resulted in the audit being created.&#x20;

| Code    | Description                                                                                                                                                                                           |
| ------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Create  | The event was triggered by an explicit request to create new data in the SanteDB CDR datastore.                                                                                                       |
| Read    | The event was triggered by an explicit request to retrieve a record. Reads are used only when the requestor has specifically asked the SanteDB server for a piece of information via its primary key. |
| Update  | The event was triggered by an explicit request to update a record. Note that on Create or Update operations the Create operation is used.                                                             |
| Delete  | The event was triggered by an explicit request to remove data from the CDR. Note that the DELETE may have resulted in a logical deletion of data rather than a permanent erasure of data.             |
| Execute | The event was an execution of a process (such as a query, a job, a startup or stopping of a service, etc.)                                                                                            |

### Event

The event code is context specific (i.e. it depends on the interface, the transaction, and standard being implemented), and describes the specific operation which occurred and resulted in the audit being created.

Event codes on the summary screen have a badge with an event classification, and a detailed code. Common badges for events are:

| Code                    | Description                                                                                                                                                                     |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Query                   | The event is a query event where data is either read (via action Read) or a query executed (via Execute).                                                                       |
| Security Alert          | The event is classified as related to security of the overall SanteDB solution. Security alerts include session failures, changing of user attributes (like roles, or policies) |
| Network Activity        | Network activity events are used to classify any event which is related to the sending or receiving of data (usually when failed) from a remote system.                         |
| User Authentication     | User authentication event classifications are raised when a user establishes a session (an interactive login) or when a device logs in.                                         |
| Access Control Decision | The event indicates the outcome of an ACS access control decision or policy failure. These events are usually limited to failures only (unless full audit logging is enabled)   |
| ApplicationActivity     | The event is an internal application event.                                                                                                                                     |
| Import / Export         | The event reflects data being read (exported) or created (imported) from an external source like a data feed.                                                                   |

&#x20;Internal event codes for SanteDB start with a `SecurityAuditCode` prefix, representing their concept registration.

| Code                            | Description                                                                                                                                                                                       |
| ------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| SessionStarted / SessionStopped | The event reflects the establishment or abandonment of a user session.                                                                                                                            |
| Login                           | The event reflects the transformation of an identity (an unauthenticated object) to a principal (authenticated). For interactive sessions these are typically related with a session start event. |
| SecurityAttributeChanged        | The event represents an action where the security attributes of an object were modified.                                                                                                          |
| NetworkActivity                 | A generic network request was issued and could not be fulfilled.                                                                                                                                  |
| AuditLogUsed                    | A user read, queried, or altered an audit event. Audits can contain sensitive information, this type of event helps administrators understand the use of the audit log.                           |
| Purge Queue                     | A user has purged data from a waiting dispatch queue. This usually indicates some sort of data may have been lost.                                                                                |

### Outcome

The outcome indicator of the audit summary view indicates the overall result of the action which is represented in the detail view

| Code          | Description                                                                                                                                                              |
| ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Success       | The in the log was successfully transacted.                                                                                                                              |
| Minor Failure | The event in the audit failed, or the request to perform the action failed. The failure is minor, and has been handled. Impact to privacy or security should be minimal. |
| Serious Fail  | The event in the audit failed, or the request to perform the action failed. The failure was handled, however system stability or security may be impacted.               |
| Major Failure | The event in the audit failed, the request to perform the action failed. The failure was detected, but the state of the system is unknown.                               |

### Timestamp

The timestamp of the audit represents the exact moment in time that the action described in the audit event occurred.&#x20;

## Audit Details

When clicking the `View` button on an audit, you will be presented with a long-form data view of the audit information contained in the event. The screen is broken into 4 sections.

### Event Information

The event information section of an audit indicates the overall metadata about the event.

![](<../../../../.gitbook/assets/image (444).png>)

The event metadata is the same as that shown in the summary list, with additional context fields.

| Code    | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| ------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| EID     | The SanteDB audit event UUID assigned when the audit was created.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| Process | The name of the operating system process which generated the event data, as well as the operating system process identifier.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
| Source  | <p>The type of source application which generated the audit:</p><ol><li>End User Interface Application - Such as a windows form application</li><li>Device or Instrument - A headless device like an MRI or CT scan</li><li>Web Server Process - A web server application which service multiple concurrent users.</li><li>Application Server Process - A back-end application server which exposes APIs which other systems, in turn, consume.</li><li>Database Server Process - A database process which is responsible for storing and indexing data directly on disk.</li><li>Security Server Process - An intermediary service responsible for the securing, encryption or privacy protection of data.</li></ol> |

### Network Information

The network information section shows information about the network infrastructure when the request was made.

![](<../../../../.gitbook/assets/image (450).png>)

### Users and Computers

The users and computers section of the audit detail show the information about the actors involved in the event.&#x20;

![](<../../../../.gitbook/assets/image (494).png>)

Each actor has four attributes expressed in the table:

* **User Name**: Which shows the device, application or user name of the principal which was involved in the transaction.
* **Machine**: Showing the IP address or hostname of the machine on which the transaction was executed.
* **R**: An indicator showing if the specified event was triggered by the action (i.e. the user is the requestor)
* **Roles**: Shows the role which played, roles are:
  * 110150 - Application Process
  * 110152 - Source
  * 110153 - Destination
  * humanuser - A human who is accessing the system

### Data and Objects

The data and objects section shows the objects which were involved in the event. That is, the records, or objects which were impacted, created, deleted, executed, etc. The data and objects section differs between each type of object.

#### Lifecycles

Each object has a lifecycle attached to it which identifies the action or state within the object's overall lifecycle which the event interacted with.



| Code              | Description                                                                                                           |
| ----------------- | --------------------------------------------------------------------------------------------------------------------- |
| Creation          | The event resulted in the object being created.                                                                       |
| Amendment         | The event resulted in the object being amended / updated.                                                             |
| Disclosure        | The event resulted in the object being disclosed to the requestor.                                                    |
| Logical Deletion  | The event resulted in the object being logically deleted.                                                             |
| Permanent Erasure | The event resulted in the permanent erasure of the object.                                                            |
| Access            | The object was accessed / used in the event.                                                                          |
| Deidentification  | The object was masked/pseudonymized/redacted or otherwise altered from its original state to protect patient privacy. |
| Translation       | The object was translated.                                                                                            |

#### Session Objects

Session objects represent a security session which was established for a user. The object carries additional contextual data about the policies with which the session was authenticated.&#x20;

![](<../../../../.gitbook/assets/image (438).png>)

#### Query Objects

Query events will typically append the original query being executed against the CDR as a query structure. The format of the query data will depend on the source of the audit and the event but typically the query data is represented as:

* SQL Query definition which was executed
* HDSI Query definition which was executed
* The HL7v2 QBP `QPD` segment data
* The HL7 FHIR REST Request with Headers

![](<../../../../.gitbook/assets/image (431).png>)

#### De-Identification Objects

Whenever a policy decision is made, and the CDR needs to de-identify patient data to protect privacy of the patient, a deidentification object will be registered. This contains the identifier of the object which was the target of masking, as well as the policy which resulted in the masking occurring.

![](<../../../../.gitbook/assets/image (491).png>)

#### Policy Decision

When an access control decision is performed, and a policy violation exception thrown, the SanteDB audit log will carry a copy of the policy outcome object indicating the policy which failed validation and the overall action taken.

![](<../../../../.gitbook/assets/image (495).png>)
