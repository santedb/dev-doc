# SanteDB Object Identifiers (OIDs)

SanteDB uses object identifiers (OIDs) in one of two registered IANA Private Enterprise Number (PEN) namespaces. The use of these PEN roots depends on the timeframe when the feature was designed:

* Features from OpenIZ (SanteDB v1) and SanteDB v2 reside in the PEN for Mohawk College of Applied Arts and Technology / Applied Research: `1.3.6.1.4.1.33349.3.1.5.9`
* Features from SanteDB v2 and v3 reside in the Fyfe Software Inc. PEN: `1.3.6.1.4.1.52820.5`

The root of SanteDB OIDs from  the OpenIZ root `1.3.6.1.4.1.33349.3.1.5.9`

## OID Namespaces



| Root                      | Child |                                 |
| ------------------------- | ----- | ------------------------------- |
| 1.3.6.1.4.1.33349.3.1.5.9 | 0     | Services                        |
| 1.3.6.1.4.1.33349.3.1.5.9 | 2     | Privacy & Security              |
| 1.3.6.1.4.1.33349.3.1.5.9 | 3     | Concepts & Vocabulary           |
| 1.3.6.1.4.1.52820.5       | 1     | Deployments                     |
| 1.3.6.1.4.1.52820.5       | 2     | Clinical Templates              |
| 1.3.6.1.4.1.52820.5       | 3     | Clinical Protocols & CDSS Rules |
| 1.3.6.1.4.1.52820.5       | 4     | Identity Domains                |

## Privacy & Security OIDs

Privacy and security OIDs assigned in the `1.3.6.1.4.1.33349.3.1.5.9.2` namespace represent policies. These policies are expressed in OIDs as they are hierarchical in nature. The default OIDs in this namespace are:

| OID                                   | Policy                                                          |
| ------------------------------------- | --------------------------------------------------------------- |
| 1.3.6.1.4.1.33349.3.1.5.9.2           | Unrestricted All                                                |
| 1.3.6.1.4.1.33349.3.1.5.9.2.0         | Unrestricted Administrative Function                            |
| 1.3.6.1.4.1.33349.3.1.5.9.2.0.1       | Change Password                                                 |
| 1.3.6.1.4.1.33349.3.1.5.9.2.0.10      | Administer Data Warehouse                                       |
| 1.3.6.1.4.1.33349.3.1.5.9.2.0.11      | Access Audit Log                                                |
| 1.3.6.1.4.1.33349.3.1.5.9.2.0.12      | Administer Applets                                              |
| 1.3.6.1.4.1.33349.3.1.5.9.2.0.13      | Assign Policy                                                   |
| 1.3.6.1.4.1.33349.3.1.5.9.2.0.14      | Unrestricted PubSub Administration                              |
| 1.3.6.1.4.1.33349.3.1.5.9.2.0.14.1    | Create/Alter PubSub Subscriptions                               |
| 1.3.6.1.4.1.33349.3.1.5.9.2.0.14.2    | Disable/Enable PubSub Subscriptions                             |
| 1.3.6.1.4.1.33349.3.1.5.9.2.0.14.3    | Delete PubSub Subscriptions                                     |
| 1.3.6.1.4.1.33349.3.1.5.9.2.0.14.4    | Read PubSub Subscriptions                                       |
| 1.3.6.1.4.1.33349.3.1.5.9.2.0.15      | Alter System Configuration                                      |
| 1.3.6.1.4.1.33349.3.1.5.9.2.0.15.1    | Unrestricted Match Configuration                                |
| 1.3.6.1.4.1.33349.3.1.5.9.2.0.15.1.1  | Alter Match Configurations                                      |
| 1.3.6.1.4.1.33349.3.1.5.9.2.0.15.1.2  | Disable/Enable Match Configurations                             |
| 1.3.6.1.4.1.33349.3.1.5.9.2.0.15.2    | Unrestricted Clinical Protocol Configuration                    |
| 1.3.6.1.4.1.33349.3.1.5.9.2.0.15.2.0  | Create Clinical Protocol                                        |
| 1.3.6.1.4.1.33349.3.1.5.9.2.0.15.2.1  | Alter Clinical Protocol                                         |
| 1.3.6.1.4.1.33349.3.1.5.9.2.0.15.2.2  | Delete Clinical Protocol                                        |
| 1.3.6.1.4.1.33349.3.1.5.9.2.0.15.3    | Alter Clinical Data Templates                                   |
| 1.3.6.1.4.1.33349.3.1.5.9.2.0.16      | Unrestricted Dispatcher Queue                                   |
| 1.3.6.1.4.1.33349.3.1.5.9.2.0.17      | Administer Internal Mail / Messages                             |
| 1.3.6.1.4.1.33349.3.1.5.9.2.0.18      | Manage System Backups                                           |
| 1.3.6.1.4.1.33349.3.1.5.9.2.0.18.1    | Create System Backup on (Private or Public)                     |
| 1.3.6.1.4.1.33349.3.1.5.9.2.0.18.1.1  | Create Private System Backup                                    |
| 1.3.6.1.4.1.33349.3.1.5.9.2.0.19      | Unrestricted Security Certificate Management                    |
| 1.3.6.1.4.1.33349.3.1.5.9.2.0.19.1    | Issue New Certificates                                          |
| 1.3.6.1.4.1.33349.3.1.5.9.2.0.19.2    | Revoke Certificates                                             |
| 1.3.6.1.4.1.33349.3.1.5.9.2.0.19.3    | Assign Certificate to Security Identity                         |
| 1.3.6.1.4.1.33349.3.1.5.9.2.0.2       | Create Role                                                     |
| 1.3.6.1.4.1.33349.3.1.5.9.2.0.20      | Manage Foreign Data                                             |
| 1.3.6.1.4.1.33349.3.1.5.9.2.0.21      | Unrestricted Access to Service Logs                             |
| 1.3.6.1.4.1.33349.3.1.5.9.2.0.21.1    | Read Service Logs                                               |
| 1.3.6.1.4.1.33349.3.1.5.9.2.0.21.2    | Delete Service Logs                                             |
| 1.3.6.1.4.1.33349.3.1.5.9.2.0.22      | Unrestricted Job Management                                     |
| 1.3.6.1.4.1.33349.3.1.5.9.2.0.22.0    | Read System Jobs                                                |
| 1.3.6.1.4.1.33349.3.1.5.9.2.0.22.1    | Start/Run System Job                                            |
| 1.3.6.1.4.1.33349.3.1.5.9.2.0.22.2    | Alter System Job Schedule                                       |
| 1.3.6.1.4.1.33349.3.1.5.9.2.0.22.3    | Register New System Job                                         |
| 1.3.6.1.4.1.33349.3.1.5.9.2.0.3       | Alter Role                                                      |
| 1.3.6.1.4.1.33349.3.1.5.9.2.0.4       | Create Identity                                                 |
| 1.3.6.1.4.1.33349.3.1.5.9.2.0.4.1     | Create Local Users                                              |
| 1.3.6.1.4.1.33349.3.1.5.9.2.0.5       | Create Device                                                   |
| 1.3.6.1.4.1.33349.3.1.5.9.2.0.6       | Create Application                                              |
| 1.3.6.1.4.1.33349.3.1.5.9.2.0.7       | Administer Concept Dictionary                                   |
| 1.3.6.1.4.1.33349.3.1.5.9.2.0.8       | Alter Identity                                                  |
| 1.3.6.1.4.1.33349.3.1.5.9.2.0.8.1     | Alter Local Users                                               |
| 1.3.6.1.4.1.33349.3.1.5.9.2.0.9       | Alter Policy                                                    |
| 1.3.6.1.4.1.33349.3.1.5.9.2.1         | Login                                                           |
| 1.3.6.1.4.1.33349.3.1.5.9.2.1.0       | Login as a Service                                              |
| 1.3.6.1.4.1.33349.3.1.5.9.2.1.0.0     | OAUTH Login                                                     |
| 1.3.6.1.4.1.33349.3.1.5.9.2.1.0.0.1   | OAUTH client\_credentials flow permission                       |
| 1.3.6.1.4.1.33349.3.1.5.9.2.1.0.0.1.0 | OAUTH client\_credentials flow permission no device cred        |
| 1.3.6.1.4.1.33349.3.1.5.9.2.1.0.0.2   | OAUTH password flow permission                                  |
| 1.3.6.1.4.1.33349.3.1.5.9.2.1.0.0.2.0 | OAUTH password flow permission no device cred                   |
| 1.3.6.1.4.1.33349.3.1.5.9.2.1.0.0.3   | OAUTH authoization code grant flow permission                   |
| 1.3.6.1.4.1.33349.3.1.5.9.2.1.0.0.3.0 | OAUTH authoization code grant flow permission no device cred    |
| 1.3.6.1.4.1.33349.3.1.5.9.2.1.0.0.4   | OAUTH Password Reset grant (extended permission)                |
| 1.3.6.1.4.1.33349.3.1.5.9.2.1.0.0.4.0 | OAUTH Password Reset grant (extended permission) no device cred |
| 1.3.6.1.4.1.33349.3.1.5.9.2.1.0.1     | Login for Password Reassignment                                 |
| 1.3.6.1.4.1.33349.3.1.5.9.2.1.0.2     | Allow Impersonation of Application                              |
| 1.3.6.1.4.1.33349.3.1.5.9.2.10        | Access Client Administrative Function                           |
| 1.3.6.1.4.1.33349.3.1.5.9.2.100       | Access All SanteDB Tools                                        |
| 1.3.6.1.4.1.33349.3.1.5.9.2.100.1     | Access SanteDB Administrator Panel                              |
| 1.3.6.1.4.1.33349.3.1.5.9.2.100.2     | Access SanteEMR Clinical Interface                              |
| 1.3.6.1.4.1.33349.3.1.5.9.2.2         | Unrestricted Clinical Data                                      |
| 1.3.6.1.4.1.33349.3.1.5.9.2.2.0       | Query Clinical Data                                             |
| 1.3.6.1.4.1.33349.3.1.5.9.2.2.1       | Write Clinical Data                                             |
| 1.3.6.1.4.1.33349.3.1.5.9.2.2.2       | Delete Clinical Data                                            |
| 1.3.6.1.4.1.33349.3.1.5.9.2.2.3       | Read Clinical Data                                              |
| 1.3.6.1.4.1.33349.3.1.5.9.2.2.4       | Export Clinical Data (PHI)                                      |
| 1.3.6.1.4.1.33349.3.1.5.9.2.2.5       | Elevate Clinical Data                                           |
| 1.3.6.1.4.1.33349.3.1.5.9.2.2.6       | Unrestricted Non-PHI CDR Acts                                   |
| 1.3.6.1.4.1.33349.3.1.5.9.2.2.6.1     | Write Non-PHI CDR Acts                                          |
| 1.3.6.1.4.1.33349.3.1.5.9.2.2.6.2     | Read Non-PHI CDR Acts                                           |
| 1.3.6.1.4.1.33349.3.1.5.9.2.200       | Unrestricted EMR Functions                                      |
| 1.3.6.1.4.1.33349.3.1.5.9.2.200.1     | Clinic Reporting                                                |
| 1.3.6.1.4.1.33349.3.1.5.9.2.300       | Unrestricted IMS Functions                                      |
| 1.3.6.1.4.1.33349.3.1.5.9.2.300.1     | Unrestricted Stock Management                                   |
| 1.3.6.1.4.1.33349.3.1.5.9.2.300.1.0   | View Clinic Stock Information                                   |
| 1.3.6.1.4.1.33349.3.1.5.9.2.300.1.1   | Alter Clinic Stock Stores                                       |
| 1.3.6.1.4.1.33349.3.1.5.9.2.300.1.2   | Perform Stock Count                                             |
| 1.3.6.1.4.1.33349.3.1.5.9.2.300.1.3   | Manage Clinic Vaccination Sessions                              |
| 1.3.6.1.4.1.33349.3.1.5.9.2.300.1.4   | Perform Stock Adjustment                                        |
| 1.3.6.1.4.1.33349.3.1.5.9.2.300.1.5   | Perform Stock Store Temperature Monitoring                      |
| 1.3.6.1.4.1.33349.3.1.5.9.2.300.2     | Unrestricted Order Management                                   |
| 1.3.6.1.4.1.33349.3.1.5.9.2.300.2.1   | Create or Cancel Order Request                                  |
| 1.3.6.1.4.1.33349.3.1.5.9.2.300.2.2   | Accept and Despatch Order Requests                              |
| 1.3.6.1.4.1.33349.3.1.5.9.2.300.2.3   | Accept Order Despatch                                           |
| 1.3.6.1.4.1.33349.3.1.5.9.2.4         | Unrestricted Metadata                                           |
| 1.3.6.1.4.1.33349.3.1.5.9.2.4.0       | Read Metadata                                                   |
| 1.3.6.1.4.1.33349.3.1.5.9.2.4.0.1.2   | Read Materials                                                  |
| 1.3.6.1.4.1.33349.3.1.5.9.2.4.0.1.3   | Query Materials                                                 |
| 1.3.6.1.4.1.33349.3.1.5.9.2.4.0.2.2   | Read Places & Orgs                                              |
| 1.3.6.1.4.1.33349.3.1.5.9.2.4.0.2.3   | Query Places & Orgs                                             |
| 1.3.6.1.4.1.33349.3.1.5.9.2.4.1.0     | Write Materials                                                 |
| 1.3.6.1.4.1.33349.3.1.5.9.2.4.1.1     | Delete Materials                                                |
| 1.3.6.1.4.1.33349.3.1.5.9.2.4.2.0     | Write Places & Orgs                                             |
| 1.3.6.1.4.1.33349.3.1.5.9.2.4.2.1     | Delete Places & Orgs                                            |
| 1.3.6.1.4.1.33349.3.1.5.9.2.5         | Unrestricted Data Warehouse                                     |
| 1.3.6.1.4.1.33349.3.1.5.9.2.5.0       | Write Warehouse Data                                            |
| 1.3.6.1.4.1.33349.3.1.5.9.2.5.1       | Delete Warehouse Data                                           |
| 1.3.6.1.4.1.33349.3.1.5.9.2.5.2       | Read Warehouse Data                                             |
| 1.3.6.1.4.1.33349.3.1.5.9.2.5.3       | Query Warehouse Data                                            |
| 1.3.6.1.4.1.33349.3.1.5.9.2.500       | Export CDR Metadata                                             |
| 1.3.6.1.4.1.33349.3.1.5.9.2.6         | Unrestricted MDM                                                |
| 1.3.6.1.4.1.33349.3.1.5.9.2.6.1       | Write MDM Master                                                |
| 1.3.6.1.4.1.33349.3.1.5.9.2.6.2       | Read MDM Locals                                                 |
| 1.3.6.1.4.1.33349.3.1.5.9.2.6.3       | Merge MDM Master                                                |
| 1.3.6.1.4.1.33349.3.1.5.9.2.6.4       | Establish MDM Record of Truth                                   |
| 1.3.6.1.4.1.33349.3.1.5.9.2.6.4.1     | Edit Existing MDM Record of Truth                               |
| 1.3.6.1.4.1.33349.3.1.5.9.2.600       | Special Security Elevation                                      |
| 1.3.6.1.4.1.33349.3.1.5.9.2.600.1     | Change Security Challenge Question                              |
| 1.3.6.1.4.1.33349.3.1.5.9.2.900       | Login Any Facility                                              |
| 1.3.6.1.4.1.33349.3.1.5.9.2.999       | Override Disclosure                                             |
| 1.3.6.1.4.1.33349.3.1.5.9.3           | Restricted Information / Confidential                           |

## Concept & Vocabulary OIDs

Concept sets and code systems which are specific to SanteDB existing in the root `1.3.6.1.4.1.33349.3.1.5.9.3` these concept sets are:

| OID                               | Concept Set                              |
| --------------------------------- | ---------------------------------------- |
| 1.3.6.1.4.1.33349.3.1.5.9.3.0     | Concept Status                           |
| 1.3.6.1.4.1.33349.3.1.5.9.3.1     | Act Class                                |
| 1.3.6.1.4.1.33349.3.1.5.9.3.10    | Address Component Type                   |
| 1.3.6.1.4.1.33349.3.1.5.9.3.103   | Patient Status Observation Types         |
| 1.3.6.1.4.1.33349.3.1.5.9.3.104   | Condition Indication Concepts            |
| 1.3.6.1.4.1.33349.3.1.5.9.3.104.1 | Condition Negation Indicator Concepts    |
| 1.3.6.1.4.1.33349.3.1.5.9.3.105   | Equipment Functional Status              |
| 1.3.6.1.4.1.33349.3.1.5.9.3.106   | Unit of Measure (Temperatures)           |
| 1.3.6.1.4.1.33349.3.1.5.9.3.107   | Equipment Failure Reason                 |
| 1.3.6.1.4.1.33349.3.1.5.9.3.108   | Pregnancy Complications                  |
| 1.3.6.1.4.1.33349.3.1.5.9.3.109   | EMR Encounter Tags                       |
| 1.3.6.1.4.1.33349.3.1.5.9.3.11    | Name Use                                 |
| 1.3.6.1.4.1.33349.3.1.5.9.3.111   | Tetanus Immunity Status Codes            |
| 1.3.6.1.4.1.33349.3.1.5.9.3.115   | Narrative Note Types                     |
| 1.3.6.1.4.1.33349.3.1.5.9.3.12    | Telecom Address Use                      |
| 1.3.6.1.4.1.33349.3.1.5.9.3.120   | Patient Condition Trigger Codes          |
| 1.3.6.1.4.1.33349.3.1.5.9.3.120.1 | Patient Multi-Condition Codes            |
| 1.3.6.1.4.1.33349.3.1.5.9.3.124   | Pediatric Developmental Disorders        |
| 1.3.6.1.4.1.33349.3.1.5.9.3.13    | Telecom Address Type                     |
| 1.3.6.1.4.1.33349.3.1.5.9.3.13.1  | Human Telecom Address Type               |
| 1.3.6.1.4.1.33349.3.1.5.9.3.14    | Service Code                             |
| 1.3.6.1.4.1.33349.3.1.5.9.3.149   | Vaccine Support Materials                |
| 1.3.6.1.4.1.33349.3.1.5.9.3.15    | Industry Code                            |
| 1.3.6.1.4.1.33349.3.1.5.9.3.16    | Administrative Genders                   |
| 1.3.6.1.4.1.33349.3.1.5.9.3.165   | Confidential Observation Types           |
| 1.3.6.1.4.1.33349.3.1.5.9.3.17    | Role Status                              |
| 1.3.6.1.4.1.33349.3.1.5.9.3.18    | Name Component Type                      |
| 1.3.6.1.4.1.33349.3.1.5.9.3.19    | Reason Codes                             |
| 1.3.6.1.4.1.33349.3.1.5.9.3.2     | Act Mood                                 |
| 1.3.6.1.4.1.33349.3.1.5.9.3.23    | Family members of children               |
| 1.3.6.1.4.1.33349.3.1.5.9.3.24    | Spousal Family Members                   |
| 1.3.6.1.4.1.33349.3.1.5.9.3.25    | Vaccines                                 |
| 1.3.6.1.4.1.33349.3.1.5.9.3.26    | Administration Act Type Codes            |
| 1.3.6.1.4.1.33349.3.1.5.9.3.27    | Container Type                           |
| 1.3.6.1.4.1.33349.3.1.5.9.3.27.1  | Cold Storage Containers                  |
| 1.3.6.1.4.1.33349.3.1.5.9.3.28    | AdministrableDrugForm                    |
| 1.3.6.1.4.1.33349.3.1.5.9.3.29    | Route of administration                  |
| 1.3.6.1.4.1.33349.3.1.5.9.3.3     | Act Status                               |
| 1.3.6.1.4.1.33349.3.1.5.9.3.30    | Subset of Discharge Disposition (HL7)    |
| 1.3.6.1.4.1.33349.3.1.5.9.3.31    | Drug Administration Units                |
| 1.3.6.1.4.1.33349.3.1.5.9.3.32    | AdministrationSite                       |
| 1.3.6.1.4.1.33349.3.1.5.9.3.33    | Drug Administration Units                |
| 1.3.6.1.4.1.33349.3.1.5.9.3.34    | Vital Signs                              |
| 1.3.6.1.4.1.33349.3.1.5.9.3.35    | Units of Measure                         |
| 1.3.6.1.4.1.33349.3.1.5.9.3.36    | Units of Measure for Weight              |
| 1.3.6.1.4.1.33349.3.1.5.9.3.37    | Protocol Violation Reason                |
| 1.3.6.1.4.1.33349.3.1.5.9.3.38    | Stock Adjustment Reasons                 |
| 1.3.6.1.4.1.33349.3.1.5.9.3.38.0  | Stock Act Reasons - Decrease             |
| 1.3.6.1.4.1.33349.3.1.5.9.3.38.1  | Stock Act Reason Codes - Increase        |
| 1.3.6.1.4.1.33349.3.1.5.9.3.38.2  | Vaccination Session Adjustment Reasons   |
| 1.3.6.1.4.1.33349.3.1.5.9.3.39    | Allergies and Intolerance Types          |
| 1.3.6.1.4.1.33349.3.1.5.9.3.4     | Act Relationship Type                    |
| 1.3.6.1.4.1.33349.3.1.5.9.3.40    | SupplementCodes                          |
| 1.3.6.1.4.1.33349.3.1.5.9.3.41    | Act Types                                |
| 1.3.6.1.4.1.33349.3.1.5.9.3.42    | Null Reason                              |
| 1.3.6.1.4.1.33349.3.1.5.9.3.43    | Severity Observation Values              |
| 1.3.6.1.4.1.33349.3.1.5.9.3.44    | Causes of Death                          |
| 1.3.6.1.4.1.33349.3.1.5.9.3.45    | Observation Act Types                    |
| 1.3.6.1.4.1.33349.3.1.5.9.3.46    | Reaction Observations                    |
| 1.3.6.1.4.1.33349.3.1.5.9.3.47    | Subset of Disposition (HL7)              |
| 1.3.6.1.4.1.33349.3.1.5.9.3.48    | Security Audit Codes                     |
| 1.3.6.1.4.1.33349.3.1.5.9.3.49    | Material Type Codes                      |
| 1.3.6.1.4.1.33349.3.1.5.9.3.5     | Act Interpretation                       |
| 1.3.6.1.4.1.33349.3.1.5.9.3.50    | Protocol Violation - Don't Reschedule    |
| 1.3.6.1.4.1.33349.3.1.5.9.3.51    | Diagnosis Codes                          |
| 1.3.6.1.4.1.33349.3.1.5.9.3.52    | Problem or Concern Observation Types     |
| 1.3.6.1.4.1.33349.3.1.5.9.3.53    | Adverse Event Types                      |
| 1.3.6.1.4.1.33349.3.1.5.9.3.54    | Place Type Concepts (Sub-Classes)        |
| 1.3.6.1.4.1.33349.3.1.5.9.3.54.1  | Facility Type Concepts (Sub-Classes)     |
| 1.3.6.1.4.1.33349.3.1.5.9.3.55    | Organization Type Concept                |
| 1.3.6.1.4.1.33349.3.1.5.9.3.55.1  | Educational Organization Types           |
| 1.3.6.1.4.1.33349.3.1.5.9.3.56    | Place Entity Class Code Concepts         |
| 1.3.6.1.4.1.33349.3.1.5.9.3.59    | Language Codes                           |
| 1.3.6.1.4.1.33349.3.1.5.9.3.6     | Entity Class                             |
| 1.3.6.1.4.1.33349.3.1.5.9.3.60    | Living Arrangement                       |
| 1.3.6.1.4.1.33349.3.1.5.9.3.61    | Marital Status                           |
| 1.3.6.1.4.1.33349.3.1.5.9.3.62    | Ethnicities                              |
| 1.3.6.1.4.1.33349.3.1.5.9.3.63    | Religions                                |
| 1.3.6.1.4.1.33349.3.1.5.9.3.64    | Education Levels                         |
| 1.3.6.1.4.1.33349.3.1.5.9.3.65    | Master Data Model Relationship Types     |
| 1.3.6.1.4.1.33349.3.1.5.9.3.66    | Place Classifications                    |
| 1.3.6.1.4.1.33349.3.1.5.9.3.67    | Name Prefix                              |
| 1.3.6.1.4.1.33349.3.1.5.9.3.68    | Name Suffix                              |
| 1.3.6.1.4.1.33349.3.1.5.9.3.69    | Purposes of Use                          |
| 1.3.6.1.4.1.33349.3.1.5.9.3.7     | Entity Status                            |
| 1.3.6.1.4.1.33349.3.1.5.9.3.70    | Encounter Type Codes                     |
| 1.3.6.1.4.1.33349.3.1.5.9.3.71    | Registration Event Type Codes            |
| 1.3.6.1.4.1.33349.3.1.5.9.3.72    | Delivery Outcome Codes                   |
| 1.3.6.1.4.1.33349.3.1.5.9.3.73    | Delivery Method Codes                    |
| 1.3.6.1.4.1.33349.3.1.5.9.3.74    | Delivery Location Codes                  |
| 1.3.6.1.4.1.33349.3.1.5.9.3.75    | Units of Measure for Height              |
| 1.3.6.1.4.1.33349.3.1.5.9.3.76    | Verification Status                      |
| 1.3.6.1.4.1.33349.3.1.5.9.3.77    | Occupation Types                         |
| 1.3.6.1.4.1.33349.3.1.5.9.3.78    | VIP Status Codes                         |
| 1.3.6.1.4.1.33349.3.1.5.9.3.79    | Relationship Classification              |
| 1.3.6.1.4.1.33349.3.1.5.9.3.8     | Entity Relationship Type                 |
| 1.3.6.1.4.1.33349.3.1.5.9.3.80    | Identifier Type Codes                    |
| 1.3.6.1.4.1.33349.3.1.5.9.3.82    | Pregnancy Outcomes                       |
| 1.3.6.1.4.1.33349.3.1.5.9.3.84    | Country Codes                            |
| 1.3.6.1.4.1.33349.3.1.5.9.3.85    | Nationality Codes                        |
| 1.3.6.1.4.1.33349.3.1.5.9.3.86    | Detected Issue Type                      |
| 1.3.6.1.4.1.33349.3.1.5.9.3.87    | Procedure Technique Codes                |
| 1.3.6.1.4.1.33349.3.1.5.9.3.88    | Body Site Codes                          |
| 1.3.6.1.4.1.33349.3.1.5.9.3.9     | Address Use                              |
| 1.3.6.1.4.1.33349.3.1.5.9.3.90    | Provider Types for Individuals           |
| 1.3.6.1.4.1.33349.3.1.5.9.3.91    | HIV Status Codes                         |
| 1.3.6.1.4.1.33349.3.1.5.9.3.92    | Syphilis Diagnosis Codes                 |
| 1.3.6.1.4.1.33349.3.1.5.9.3.94    | Herpes Simplex Virus                     |
| 1.3.6.1.4.1.33349.3.1.5.9.3.95    | Sexually Transmitted Infectious Diseases |
| 1.3.6.1.4.1.33349.3.1.5.9.3.99    | Contact Role                             |

## Community Deployments

Community deployments undertaken by SanteSuite Inc. or SanteSuite partners typically will require OIDs for custom policies, templates, CDSS rules, etc. These OIDs are assigned off the root branch for the deployment in the `1.3.6.1.4.1.52820.5.1` namespace and are.



<table><thead><tr><th>OID</th><th width="146">Jurisdiction</th><th>Uses</th></tr></thead><tbody><tr><td>1.3.6.1.4.1.52820.5.1.0</td><td>ELB</td><td>Elbonia MPI</td></tr><tr><td>1.3.6.1.4.1.52820.5.1.1</td><td>MY</td><td>Myanmar National MPI<br>Myanmar OpenMRS Identifiers</td></tr><tr><td>1.3.6.1.4.1.52820.5.1.2</td><td>SB</td><td>Solomon MPI &#x26; IIS</td></tr><tr><td>1.3.6.1.4.1.52820.5.1.3</td><td>FJ</td><td>Fiji MPI &#x26; IIS</td></tr><tr><td>1.3.6.1.4.1.52820.5.1.4</td><td>KI</td><td>Kiribati MPI &#x26; IIS</td></tr><tr><td>1.3.6.1.4.1.52820.5.1.5</td><td>DL</td><td>Demoland (new Demonstration Jurisdiction)</td></tr></tbody></table>

## Clinical Templates

Clinical templates are structures which dictate the format, entry, and display of clinical data primarily from SanteEMR derivatives (such as SanteIMS). These templates are assigned OIDs from the `1.3.6.1.4.1.52820.5.2` namespace which has five children:

* `1.3.6.1.4.1.52820.5.2.0` - Templates for `Patients`
* `1.3.6.1.4.1.52820.5.2.1` - Templates for `Observations`
* `1.3.6.1.4.1.52820.5.2.2` - Templates for `Act`&#x20;
* `1.3.6.1.4.1.52820.5.2.3` - Templates for `SubstanceAdminsitration`&#x20;
* `1.3.6.1.4.1.52820.5.2.4` - Templates for `Procedure`
* `1.3.6.1.4.1.52820.5.2.5` - Templates for `PatientEncounter`
* `1.3.6.1.4.1.52820.5.2.6` - Templates for stock related data

The clinical templates defined by SanteDB community implementations are:

<table><thead><tr><th width="257">OID</th><th width="259">Mnemonic</th><th width="335">Name</th></tr></thead><tbody><tr><td>1.3.6.1.4.1.52820.5.2.0.1</td><td>org.santedb.emr.patient</td><td>Patient Registration</td></tr><tr><td>1.3.6.1.4.1.52820.5.2.0.2</td><td>org.santedb.emr.patient.baby</td><td>Newborn Information</td></tr><tr><td>1.3.6.1.4.1.52820.5.2.1.0</td><td>org.santedb.emr.observation.verification</td><td>Observation Verification State</td></tr><tr><td>1.3.6.1.4.1.52820.5.2.1.1</td><td>org.santedb.emr.observation.cod</td><td>Cause Of Death</td></tr><tr><td>1.3.6.1.4.1.52820.5.2.1.10</td><td>org.santedb.emr.observation.weight</td><td>Weight Entry</td></tr><tr><td>1.3.6.1.4.1.52820.5.2.1.11</td><td>org.santedb.ims.problem.aefi</td><td>Adverse Event Following Immunization (AEFI)</td></tr><tr><td>1.3.6.1.4.1.52820.5.2.1.12</td><td>org.santedb.emr.hiv.status</td><td>HIV Status</td></tr><tr><td>1.3.6.1.4.1.52820.5.2.1.13</td><td>org.santedb.emr.pregnancy.status</td><td>Pregnancy Status</td></tr><tr><td>1.3.6.1.4.1.52820.5.2.1.13.1</td><td>org.santedb.emr.pregnancy.lmp</td><td>Last Menstrual Period</td></tr><tr><td>1.3.6.1.4.1.52820.5.2.1.13.2</td><td>org.santedb.emr.pregnancy.edd</td><td>Estimated Delivery Date</td></tr><tr><td>1.3.6.1.4.1.52820.5.2.1.13.3</td><td>org.santedb.emr.pregnancy.aof</td><td>Estimated Age of Fetus</td></tr><tr><td>1.3.6.1.4.1.52820.5.2.1.13.4</td><td>org.santedb.emr.pregnancy.confirm</td><td>Confirmation of Pregnancy</td></tr><tr><td>1.3.6.1.4.1.52820.5.2.1.13.5</td><td>org.santedb.emr.pregnancy.complication</td><td>Pregnancy Complication(s)</td></tr><tr><td>1.3.6.1.4.1.52820.5.2.1.14</td><td>org.santedb.emr.pregnancy.history</td><td>Pregnancy History</td></tr><tr><td>1.3.6.1.4.1.52820.5.2.1.15</td><td>org.santedb.emr.infant.feeding</td><td>Breast Feeding Status</td></tr><tr><td>1.3.6.1.4.1.52820.5.2.1.16</td><td>org.santedb.emr.hiv.mothersStatus</td><td>Mother's HIV Status</td></tr><tr><td>1.3.6.1.4.1.52820.5.2.1.17</td><td>org.santedb.emr.observation.headCircumference</td><td>Head Circumference</td></tr><tr><td>1.3.6.1.4.1.52820.5.2.1.18</td><td>org.santedb.emr.observation.vitalSigns</td><td>Vital Signs</td></tr><tr><td>1.3.6.1.4.1.52820.5.2.1.18.1</td><td>org.santedb.emr.observation.heartRate</td><td>Heart Rate</td></tr><tr><td>1.3.6.1.4.1.52820.5.2.1.18.2</td><td>org.santedb.emr.observation.respirationRate</td><td>Respiration Rate</td></tr><tr><td>1.3.6.1.4.1.52820.5.2.1.19</td><td>org.santedb.emr.observation.temperature</td><td>Body Temperature</td></tr><tr><td>1.3.6.1.4.1.52820.5.2.1.20</td><td>org.santedb.emr.observation.bloodPressure</td><td>Blood Pressure Reading</td></tr><tr><td>1.3.6.1.4.1.52820.5.2.1.21</td><td>org.santedb.emr.condition.allergy</td><td>Allergy / Intolerance Entry</td></tr><tr><td>1.3.6.1.4.1.52820.5.2.1.30</td><td>org.santedb.emr.pregnancy.conclude</td><td>Pregnancy Completion/Termination</td></tr><tr><td>1.3.6.1.4.1.52820.5.2.1.40</td><td>org.santedb.emr.organizer.sti.panel</td><td>Sexually Transmitted Diseases (Current &#x26; Historical)</td></tr><tr><td>1.3.6.1.4.1.52820.5.2.1.40.1</td><td>org.santedb.emr.act.sti.infection</td><td>Sexually Transmited Infectious Disease</td></tr><tr><td>1.3.6.1.4.1.52820.5.2.1.6</td><td>org.santedb.emr.observation.height</td><td>Height Entry</td></tr><tr><td>1.3.6.1.4.1.52820.5.2.1.60</td><td>org.santedb.emr.observation.pediatric.developmentDisability</td><td>Developmental Disability</td></tr><tr><td>1.3.6.1.4.1.52820.5.2.1.8</td><td>org.santedb.emr.observation.death</td><td>Death Report</td></tr><tr><td>1.3.6.1.4.1.52820.5.2.1.8.1</td><td>org.santedb.emr.observation.timeofdeath</td><td>Time of Death</td></tr><tr><td>1.3.6.1.4.1.52820.5.2.2.1</td><td>org.santedb.emr.act.registration.birth</td><td>Birth Registration</td></tr><tr><td>1.3.6.1.4.1.52820.5.2.2.1.1</td><td>org.santedb.emr.observation.birthWeight</td><td>Birth Weight Entry</td></tr><tr><td>1.3.6.1.4.1.52820.5.2.2.1.2</td><td>org.santedb.emr.observation.birthSex</td><td>Birth Sex</td></tr><tr><td>1.3.6.1.4.1.52820.5.2.2.1.3</td><td>org.santedb.emr.observation.birthDeliveryLocation</td><td>Birth Delivery Location</td></tr><tr><td>1.3.6.1.4.1.52820.5.2.2.1.4</td><td>org.santedb.emr.observation.birthDeliveryMethod</td><td>Birth Delivery Method</td></tr><tr><td>1.3.6.1.4.1.52820.5.2.2.1.5</td><td>org.santedb.emr.observation.birthDeliveryOutcome</td><td>APGAR Panel</td></tr><tr><td>1.3.6.1.4.1.52820.5.2.2.1.6</td><td>org.santedb.emr.observation.deliveryDateAndTime</td><td>Birth Date &#x26; Time</td></tr><tr><td>1.3.6.1.4.1.52820.5.2.2.1.7</td><td>org.santedb.emr.observation.gestationalAgeAtBirth</td><td>Gestational Age at Birth</td></tr><tr><td>1.3.6.1.4.1.52820.5.2.2.1.8</td><td>org.santedb.emr.observation.apgarScore.panel</td><td>APGAR Scores</td></tr><tr><td>1.3.6.1.4.1.52820.5.2.2.1.8.1</td><td>org.santedb.emr.observation.apgarScore.1Minute</td><td>1 Minute APGAR Score</td></tr><tr><td>1.3.6.1.4.1.52820.5.2.2.1.8.10</td><td>org.santedb.emr.observation.apgarScore.10Minute</td><td>10 Minute APGAR Score</td></tr><tr><td>1.3.6.1.4.1.52820.5.2.2.1.8.5</td><td>org.santedb.emr.observation.apgarScore.5Minute</td><td>5 Minute APGAR Score</td></tr><tr><td>1.3.6.1.4.1.52820.5.2.2.1.9</td><td>org.santedb.emr.observation.birthLength</td><td>Birth Length Entry</td></tr><tr><td>1.3.6.1.4.1.52820.5.2.2.2</td><td>org.santedb.emr.act.registration.death</td><td>Death Registration</td></tr><tr><td>1.3.5.1.4.1.52820.5.2.3.1</td><td>org.santedb.emr.sbadm.supplement</td><td>Supplements</td></tr><tr><td>1.3.5.1.4.1.52820.5.2.3.2</td><td>org.santedb.emr.sbadm.immunization</td><td>Scheduled / Routine Immunization</td></tr><tr><td>1.3.5.1.4.1.52820.5.2.3.2.1</td><td>org.santedb.emr.sbadm.immunization.booster</td><td>Immunization (Booster/AdHoc)</td></tr><tr><td>1.3.5.1.4.1.52820.5.2.3.2.2</td><td>org.santedb.emr.sbadm.immunization.embedded</td><td>Immunization Inline</td></tr><tr><td>1.3.6.1.4.1.52820.5.2.5.1</td><td>org.santedb.emr.act.visit.lds</td><td>Labour &#x26; Delivery Visit</td></tr><tr><td>1.3.6.1.4.1.52820.5.2.5.2</td><td>org.santedb.emr.act.visit.anc</td><td>ANC Visit</td></tr><tr><td>1.3.6.1.4.1.52820.5.2.5.3</td><td>org.santedb.emr.act.visit.general</td><td>General / Primary Care Visit</td></tr><tr><td>1.3.6.1.4.1.52820.5.2.5.6</td><td>org.santedb.emr.act.visit.neonatal</td><td>Neonatal Visit</td></tr><tr><td>1.3.6.1.4.1.52820.5.2.5.8</td><td>org.santedb.ims.pediatric.routineVacc</td><td>Routine Vaccination (Pediatric)</td></tr><tr><td>1.3.6.1.4.1.52820.5.2.6.1</td><td>org.santedb.ims.container.functionalStatus</td><td>Functional Status</td></tr><tr><td>1.3.6.1.4.1.52820.5.2.6.2</td><td>org.santedb.ims.container.temperature</td><td>Temperature Reading</td></tr><tr><td>1.3.6.1.4.1.52820.5.2.6.3</td><td>org.santedb.ims.container.monitoring</td><td>Routine Monitoring of Cold Storage</td></tr><tr><td>1.3.6.1.4.1.52820.5.2.6.4</td><td>org.santedb.ims.container.count</td><td>Stock count &#x26; assignment</td></tr><tr><td>1.3.6.1.4.1.52820.5.2.6.5</td><td>org.santedb.ims.container.adjust</td><td>Stock adjustment</td></tr><tr><td>1.3.6.1.4.1.52820.5.2.6.6</td><td>org.santedb.ims.container.transfer</td><td>Stock transfer</td></tr><tr><td>1.3.6.1.4.1.52820.5.2.6.7.1</td><td>org.santedb.ims.session.start</td><td>Start Vaccination Session</td></tr><tr><td>1.3.6.1.4.1.52820.5.2.6.7.2</td><td>org.santedb.ims.session.issue</td><td>Issue More Stock to Vaccination Session</td></tr><tr><td>1.3.6.1.4.1.52820.5.2.6.7.3</td><td>org.santedb.ims.session.return</td><td>Return Stock from Vaccination Session</td></tr><tr><td>1.3.6.1.4.1.52820.5.2.6.7.4</td><td>org.santedb.ims.session.end</td><td>End Vaccination Session</td></tr><tr><td>1.3.6.1.4.1.52820.5.2.6.7.5</td><td>org.santedb.ims.session.openVialWaste</td><td>Session Open Vial Wastage</td></tr><tr><td>1.3.6.1.4.1.52820.5.2.6.8</td><td>org.santedb.ims.stock.vvm</td><td>Vaccine Vial Monitoring</td></tr><tr><td>1.3.6.1.4.1.52820.5.2.999</td><td>org.santedb.core.masked</td><td>Confidential / Restricted Entry</td></tr></tbody></table>

## Clinical Protocol OIDs

Clinical protocols and libraries exist in the `1.3.5.1.4.1.52820.5.3` namespace, with the following child namespaces:

* `1.3.5.1.4.1.52820.5.3.1` - Childhood Nutrition, Care & Immunization Decision Support (typically applied only to patients under the age of 5)
* `1.3.5.1.4.1.52820.5.3.2` - Antenatal Care Decision Support



| OID                           | Type              | Name                                                                                                                                                                                                      |
| ----------------------------- | ----------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1.3.5.1.4.1.52820.5.3.1.1     | Clinical Protocol | Collect weight of children under 5 years of age at minimum, once per month.                                                                                                                               |
| 1.3.5.1.4.1.52820.5.3.1.2     | Clinical Protocol | Collect height and/or length of children under 5 years of age at minimum, once per month.                                                                                                                 |
| 1.3.5.1.4.1.52820.5.3.1.3     | Clinical Protocol | Administration of routine Vitamin A supplements.                                                                                                                                                          |
| 1.3.5.1.4.1.52820.5.3.1.4     | Clinical Protocol | Administration of routine mabendazole treatment.                                                                                                                                                          |
| 1.3.5.1.4.1.52820.5.3.2.1     | Clinical Protocol | Administer Bacillus Calmette-Guerin Vaccine to children within 2 days of birth.                                                                                                                           |
| 1.3.5.1.4.1.52820.5.3.2.2     | Clinical Protocol | Administer DTP-Hib-HepB trivalent to children three times. First dose occurring 42 days after birth (recommended between 42-49 days), second and third doses administered 28-35 days after previous dose. |
| 1.3.5.1.4.1.52820.5.3.2.3     | Clinical Protocol | When child is under 18 months of age, administer MR1 dose at 274 days after birth, with second dose on or after 18th birthday                                                                             |
| 1.3.5.1.4.1.52820.5.2.3.2.3.1 | Clinical Protocol | Accelerated MR Schedule: When child is older than 18 months and has not received MR1, administer MR1 immediately and administer MR2 1 months after first dose.                                            |
| 1.3.5.1.4.1.52820.5.2.3.2.4   | Clinical Protocol | Regular PCV13 vaccination schedule for children under 5 years old.                                                                                                                                        |
| 1.3.5.1.4.1.52820.5.2.3.2.5   | Clinical Protocol | Regular Oral Polio Vaccination Computation Schedule                                                                                                                                                       |
| 1.3.5.1.4.1.52820.5.2.3.2.6   | Clinical Protocol | Oral Polio Vaccine Birth Dose Computation Protocol                                                                                                                                                        |
| 1.3.5.1.4.1.52820.5.2.3.2.7   | Clinical Protocol | Administration of Human Papilloma Virus (HPV) vaccine after 9 years of age                                                                                                                                |
| 1.3.5.1.4.1.52820.5.2.3.2.8   | Clinical Protocol | Administration of Inactivated Polio Virus Vaccine (IPV)                                                                                                                                                   |



## Identity Domain OIDs

Identity domain oids reside in the root `1.3.6.1.4.1.52820.5.4` and are further subdivided into:

* `.1` - Patient domains
* `.2` - Organization domains
* `.3` - Material Identity&#x20;
* `.4` - Place Identity&#x20;
* `.5` - Act Identity

| OID                       | Domain             | Name                                        |
| ------------------------- | ------------------ | ------------------------------------------- |
| 1.3.6.1.4.1.52820.5.4.2.1 | SIMS\_MANUFACTURER | SanteIMS Manufacturer Code                  |
| 1.3.6.1.4.1.52820.5.4.4.1 | PDH\_FAC\_UNIT\_ID | Pacific Data Hub Facility Import Identifier |
|                           |                    |                                             |
