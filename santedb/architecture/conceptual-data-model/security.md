# Security

One of the key tenants of the SanteDB immunization management system is privacy and security by design. To that end, SanteDB’s HDS supports not only external policy enforcement decisions and role providers, but also provides access to internal policy engines \(when external policy decision points are not available\).

In SanteDB there are five key security classes:

![](../../../.gitbook/assets/image%20%2827%29.png)

* **Users** - A security user represents security information related to a user. This differs from clinical information about a user in that a security user is treated as a first class user of the SanteDB system. A clinical user is often linked with a security user, however may not be \(for example, when recording the user responsible for authoring data from an external system\).
* **Devices** - A security device represents the security information related to a physical device which can connect to the SanteDB instance. This is different than a clinical device entity which, while used to represent a security device, may be a non-security device used for recording information related to acquisition of data \(i.e. the model of insulin pump given to a patient\).
* **Applications** - A security application represents an application which has been granted some form of access to SanteDB. Again, a security application can have an application entity related to it, however not all clinical applications are security applications.
* **Roles** - A role represents a particular role a user takes on within a particular security organization. 
* **Policies** - A policy represents either a data policy \(associated to clinical data\) or an functional policy \(associated with an ability to perform a function\)

### Authenticating Organizations / Roles

Starting with SanteDB 1.60, the authentication system supports the selection of UAO \(User Authenticating Organizations\). This functionality allows system administrators to alter policies based on the org unit in which a user is authenticating. 

For example, a clinician may use a particular device in the role of a ED physician on Monday and Wednesday and use the same deployment and application of SanteDB as a GP on Tuesday and Thursday. The UAO functionality allows administrators to define which roles under which UAO have grant or deny access to particular policies.

Additionally, SanteDB supports OBO \(On Behalf Of\) authentication. Under this scheme, users are granted access to policies of the "OBO" user whilst still authenticating as themselves.

