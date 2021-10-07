# Entity Data Dictionary

The [Conceptual Entity Data Dictionary](../conceptual-data-model/entities/data-dictionary.md) expressed in ADO.NET tables.  


![](../../../../.gitbook/assets/image%20%28414%29.png)

| **Physical Table** | **Conceptual Entity** | **Description** |
| :--- | :--- | :--- |
| `app_ent_tbl` | [Application Entity](../conceptual-data-model/entities/data-dictionary.md#application-entity) | This table is used to describe the clinical attributes of an application such as vendor, version etc. This differs from the security definition of an application. A security application may exist without a clinical application existing. |
| `dev_ent_tbl` | [Device Entity](../conceptual-data-model/entities/data-dictionary.md#device-entity) | This table is used to describe the clinical attributes of a device. For example an insulin pump. Like an application, a clinical device may not be a security device or vice versa. For example when describing an event in which a device was involved , but that device does not need access to the system. |
| `ent_addr_cmp_tbl` | [Entity Address Component](../conceptual-data-model/entities/data-dictionary.md#entity-address-component) | This table is used to store entity address components. In order to normalize addresses, the values of the addresses themselves are not stored in this table, rather, stored in a unique datatable. |
| `ent_addr_cmp_val_tbl` | N/A | This table stores the unique values of all address components found in the SanteDB system. |
| `ent_addr_tbl` | [Entity Address](../conceptual-data-model/entities/data-dictionary.md#entity-address) | Stores information related to an entity’s physical, mailing or other postal addresses |
| `ent_ext_tbl` | [Entity Extension](../conceptual-data-model/entities/data-dictionary.md#entity-extension) | Stores the data related to entity extensions. Entity extensions are versioned, additional values for a particular entity. |
| `ent_id_tbl` | [Entity Identifier](../conceptual-data-model/entities/data-dictionary.md#entity-identifier) | The entity identifier table is used to store alternate, external identifiers associated with a particular entity |
| `ent_name_cmp_tbl` | [Entity Name Component](../conceptual-data-model/entities/data-dictionary.md#entity-name-component) | The entity name component table is used to store the individual components \(family, given, prefix, suffix\) of an entity’s name. |
| `ent_name_tbl` | [Entity Name](../conceptual-data-model/entities/data-dictionary.md#entity-name) | The entity name table is used to store the names associated with a particular entity. For example, a patient may have a married and maiden name. |
| `ent_note_tbl` | [Entity Notes](../conceptual-data-model/entities/data-dictionary.md#entity-note) | The entity note table is used to store freetext notes about a patient. |
| `ent_rel_tbl` | [Entity Relationship](../conceptual-data-model/entities/data-dictionary.md#entity-relationship) | Entity relationships are relationships between one or more entities with one another. For example, a service delivery location may have one or more employees. |
| `ent_tag_tbl` | [Entity Tags](../conceptual-data-model/entities/data-dictionary.md#entity-tag) | Entity tags are non-versioned extensions of an entity. That is their value can change however changes are not tracked over time. |
| `ent_tbl` | [Entity](../conceptual-data-model/entities/data-dictionary.md#entity) | Represents a non-versioned parts of the core entity such as class, determiner, etc. |
| `ent_tel_tbl` | [Entity Telecom Addresses](../conceptual-data-model/entities/data-dictionary.md#entity-telecom-address) | Stores telecommunications addresses related to the entity and their associated type \(phone, email, etc\) and use \(work, home, mobile, etc.\) |
| `ent_vrsn_tbl` | [Entity Versions](../conceptual-data-model/entities/data-dictionary.md#entity-version) | This table is used to store the data which can change over time for an entity such as status, additional classifier, etc. |
| `mat_tbl` | [Material](../conceptual-data-model/entities/data-dictionary.md#material) | This table is used to store information related to materials. |
| `mmat_tbl` | [Manufactured Materials](../conceptual-data-model/entities/data-dictionary.md#manufactured-material) | This table is used to store information related to manufactured materials. |
| `org_tbl` | [Organization](../conceptual-data-model/entities/data-dictionary.md#organization) | This table is used to store information related to organizations, which are groupings of people, places for administrative purposes. |
| `pat_tbl` | [Patient](../conceptual-data-model/entities/data-dictionary.md#patient) | This table is used to store information related to patients, or those who are receiving care. |
| `plc_svc_tbl` | [Place Services](../conceptual-data-model/entities/data-dictionary.md#place-service) | This table is used to store information related to the services which occur at a particular place. |
| `plc_tbl` | [Place](../conceptual-data-model/entities/data-dictionary.md#place) | This table is used to store information about a physical place. In Open IZ places can represent delivery locations \(hospitals, clinics, etc.\) or administrative units \(states, cities, etc.\) |
| `psn_lng_tbl` | [Person Languages](../conceptual-data-model/entities/data-dictionary.md#person-communication-language) | This table is used to store information related to the languages which a person \(including patients\) speak. |
| `psn_tbl` | [Person](../conceptual-data-model/entities/data-dictionary.md#person) | This table is used to store information related to persons \(including patients and providers\). |
| `pvdr_tbl` | [Provider](../conceptual-data-model/entities/data-dictionary.md#provider) | This table is used to store information related to providers \(persons who deliver care\). |
| `usr_ent_tbl` | [User Entity](../conceptual-data-model/entities/data-dictionary.md#person) | This table is used to link the security subsystem for users to the clinical subsystem of entities \(as entities are the ones who participate in Acts rather than Security Users\). |

