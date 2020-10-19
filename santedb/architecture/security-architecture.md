# Security Architecture

## Authentication Architecture

The figure below illustrates how a remote client can obtain a token from a federated security token service \(STS\) representing an IPrincipal and pass it to the SanteDB HDS. The creation of a local IPrincipal is controlled by a local IIdentityProviderService implementation. It is imperative that the ACS generate a token format which is suitable for the HDS messaging interface to consume \(i.e. the configurations match\), otherwise the HDS will have no mechanism for verifying tokens.

![](../../.gitbook/assets/image%20%28160%29.png)

Any ACS service can be used with SanteDB, however it is recommended that the ACS being used support the OAuth token service’s password grant and provide client/device authentication via TLS and/or HTTP basic auth.

## Policy / Access Control Architecture

The enforcement of privacy and policies is handled through a series of services within the SanteDB solution. From a high level, three different types of services are involved:

* **Policy Information Provider \(PIP\) -** [**IPolicyInformationService**](../extending-santedb/server-plugins/service-definitions/security-services/policy-services/ipolicyinformationservice.md) – Is responsible for storing information related to the policies. The information point is responsible for maintaining a list of IPolicy objects which contain the name, oid, handler \(C\# class which is executed upon policy decision\), and elevation control.
* **Policy Decision Point \(PDP\)** - [IPolicyDecisionService](../extending-santedb/server-plugins/service-definitions/security-services/policy-services/ipolicydecisionservice.md) – Is responsible for making a decision related to a policy \(or series of policies\) for a given securable. The decision outcome is one of the following options:
  * **Deny** – The principal has no authorization to access the requested securable or policy.
  * **Elevate** – The principal can access the securable or policy however they require additional authentication \(such as 2nd level password, TFA, etc.\)
  * **Grant** – The principal is granted access to the specified securable or policy.
* **Policy Enforcement Point \(PEP\)** - [IPolicyEnforcementService](../extending-santedb/server-plugins/service-definitions/security-services/policy-services/ipolicyenforcementservice.md) – Is responsible for listening to events from the SanteDB system and leveraging the decision and information points to enforce the policy decision. This implementation can vary between jurisdictions however by default involves either the masking \(i.e. there is something here you can’t see\), redaction \(i.e. removal of information\), or partial disclosure of records.

The process for enforcement is illustrated below.

![](../../.gitbook/assets/image%20%28161%29.png)

### Most-Restrictive Policy Enforcement

SanteDB’s default policy decision service provider operates on a basis of most-restrictive with default DENY. In this evaluation scheme policy decisions are created as follows:

* If the principal has no data associated with the policy, the result of the decision is DENY,
* If the principal has one rule associated with the policy via role, device, or application then the result of the decision is the rule’s configuration,
* If the principal has multiple rule instances configured via role, device or application then the result of the decision is the most restrictive option.

For example, if user jsmith is a member of USERS, CLINICAL and is accessing SanteDB from application ReaderApp.

| **Policy** | **From USERS** | **From CLINICAL** | **From ReaderApp** | **Effective Set** |
| :--- | :--- | :--- | :--- | :--- |
| **Access Administrative Function** |  |  |  | **DENY** |
| Change Password |  |  |  | DENY |
| Create Role |  |  |  | DENY |
| Alter Role |  |  |  | DENY |
| Create Identity |  |  |  | DENY |
| Login | GRANT |  | GRANT | GRANT |
| **Unrestricted Clinical Data** |  | **GRANT** |  | **GRANT** |
| Query Clinical Data |  | GRANT \(implied\) |  | GRANT \(implied\) |
| Write Clinical Data |  | GRANT \(implied\) | DENY | DENY |
| Delete Clinical Data |  | GRANT \(implied\) | DENY | DENY |
| Read Clinical Data |  | GRANT \(implied\) |  | GRANT \(implied\) |
| Override Disclosure |  | GRANT | DENY | DENY |

