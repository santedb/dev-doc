---
description: >-
  SanteGuard is a centralized audit and security repository which is compatible
  with SanteDB products and as well as any product using OAUTH and IHE ATNA.
---

# About SanteGuard

## What is SanteGuard?

SanteGuard is a plugin to SanteDB that integrates a powerful audit trail into the SanteDB system. SanteGuard provides several system interfaces, user interfaces, reports, and an enhanced implementation of the IAuditRepository service. At a high level, SanteGuard:

* Allows SanteDB to receive Audit events from external systems using IETF RFC3881 or NEMA DICOM format audits over SYSLOG \(TCP, UDP, and STCP\).
* Allows SanteDB to receive Audit events over HTTP using the IETF RFC3881 or DICOM audit format \(POX service\)
* \(Future\) Allows SanteDB to receive Audit Events using HL7 FHIR
* Stores additional information about audits not captured in the default SanteDB audit repository such as SIEM attribute son the incoming Syslog message, versioning of audit events, etc.
* Adds several "widgets" to key areas of SanteDB \(the patient summary screen for example\) which allow administrators to quickly identify who has been accessing a particular patient's data.
* \(In-Progress\) An enhanced audit repository dashboard.

## Why do you care about Auditing so much?

The real question is, why should you care about auditing so much? Audits are a foundational piece of any health information system. A robust audit trail allows system administrators, policy compliance officers, and patients to have full insight into who has been accessing what data, at which times, and for what purpose. 

SanteDB heavily audits all traffic and access control decisions it makes. These, of course, can be filtered based on event, outcome, action, etc.

 

