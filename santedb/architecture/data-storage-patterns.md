---
description: Exploring SanteDB's patterns of data storage
---

# Data Storage Patterns

SanteDB's iCDR and dCDR platforms are designed to operate like any regular CDR. By default, when you install SanteDB's CDR software, the solution will permit the storage and retrieval of the data. This method of operation is sufficient for deployments where SanteDB is servicing a single purpose, for example: a national immunization registry, where only SanteDB is contributing data to / from the central server. 

However, when you want to run SanteDB as an integrator of data \(for example, as an MPI or a Shared Health Record \(SHR\)\) this mode of operation is no longer optimal. In the field you will have multiple data sources contributing a variety of information. 

SanteDB ships with a matching engine that operates in either deterministic or probabilistic modes, these functions are described in the Matching engine documentation. However, once a match is detected, one of two storage patterns can be used.

### Single-Instance Mode

When SanteDB's SIM data storage pattern service is enabled, the SIM service will handle the matching and merging of records. In single instance mode, SanteDB's storage engine will flag duplicates \(or merge them, depending on your configuration\) however will only ever keep one copy of a known good record.

This means, for example, if one system reports a Facility Registration for a facility name "Good Health Hospital", and another reports a facility "Good Health Hospital" that is determined to be a duplicate, SanteDB will flag the two records as duplicates. Once merged, one record is subsumed into the other, the subsumed record is nullified and no longer appears in searches. 

### Multi-Instance Mode 

When SanteDB's MIM data storage pattern service is enabled, the behavior of the software is quite different. In MIM mode, SanteDB will store all records as a "local" record and tag them as mdm.type=L. The solution then searches for other records which might be duplicated in its data store.

If SanteDB determines no other records match the local record created, it will generate a new master record and tag it as mdm.type=M. Master records aren't really records, rather they are pointers \(or an anchor point\) where local records are attached. 

If the matching system determines that there are potential matches, depending on configuration, it will either link the newly inserted local record to the existing master record which matches, or it will simply mark the record as a candidate local \(for later merging\).

The sending system has complete authority to update its local records however it wants, it may change names, dates of birth, etc. When an update occurs on a local, the MIM pattern service will re-run the matching rules to determine if the local is still, indeed a match with the master, or if the record could be linked to another master.

When in MIM mode, and a query is run, the MIM persistence service will query for local records which match the specified criteria, and will synthesize a master based on the data elements the requesting system has appropriate access permission for.

Multi-instance mode is very useful for central registries like MPI, MFR, and MPR. It has several benefits over SIM:

* Merged records can subsequently be un-merged
* It is possible to flag / compartmentalize local records based on their access policies \(for example, you can prevent an immunization registry from seeing an HIV programme information\)
* It allows complete versioning and tracking of updates made to the local record.

#### Records of Truth

When running in MIM mode, it is possible to assign attributes of the various local records into a record of truth. For example, if you collect patient information from several hospitals about a particular patient \(say: William Butler in hospital A, Bill Butler from hospital B\), it is possible to designate an official record of truth for that patient. A record of truth will always be returned to callers, and prevents the synthesizing of master data records \(or rather, it overrides the local fields which have been promoted to record of truth status\).

Records of truth cannot be edited by local systems, records of truth can only be edited by the iCDR in which the record resides.

