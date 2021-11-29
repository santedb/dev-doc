# Act Data Dictionary

The [Conceptual Act Data Dictionary](../conceptual-data-model/acts/act-data-dictionary.md) expressed in ADO.NET tables.

![](../../../../.gitbook/assets/image%20%28413%29.png)

| **Physical Table** | **Conceptual Entity** | **Description** |
| :--- | :--- | :--- |
| `act_tbl` | [Act](../conceptual-data-model/acts/act-data-dictionary.md#act-entity) | This table is used to store the non-versioned aspects of an act. These are things that are not supposed to change over the lifespan of an act |
| `act_vrsn_tbl` | [Act \(Versions\)](../conceptual-data-model/acts/act-data-dictionary.md#actversion-entity) | This table is used to store the versioned portions of an act. The version sequence column should be a sequence which increments for each tuple \(at minimum\) or each new version of an object \(best option\) |
| `act_id_tbl` | [Act Identifiers](../conceptual-data-model/acts/act-data-dictionary.md#actidentifier-entity) | This is an associative table which is used to store identifiers by which an act is referenced externally. |
| `act_ext_tbl` | [Act Extensions](../conceptual-data-model/acts/act-data-dictionary.md#actextension-entity) | Extensions table. |
| `act_proto_tbl` | Act Protocols | Act protocol implementation table. |
| `act_ptcpt_tbl` | [Act Participation](../conceptual-data-model/acts/act-data-dictionary.md#actparticipation-entity) | Act participation table \(links acts to entities\) |
| `act_tag` | [Act Tags](../conceptual-data-model/acts/act-data-dictionary.md#acttag-entity) | Act tags table |
| `act_ext_tbl` | [Act Extensions](../conceptual-data-model/acts/act-data-dictionary.md#actextension-entity) | Act extensions table \(value should be a binary array or BLOB\) |
| `act_note_tbl` | [Act Notes](../conceptual-data-model/acts/act-data-dictionary.md#actnote-entity) | Act notes |
| `act_pol_assoc_tbl` | Act Policies | Policies which apply to the act. |
| `act_rel_tbl` | [Act Relationships](../conceptual-data-model/acts/act-data-dictionary.md#actrelationship-entity) | Relationships table. Note that effective/obsolete sequence columns refer to the source act. |
| `sub_adm_tbl` | [Substance Administrations](../conceptual-data-model/acts/act-data-dictionary.md#substanceadministration-entity) | Substance administration child table which is linked directly to the act table. |
| `obs_tbl` | [Observation](../conceptual-data-model/acts/act-data-dictionary.md#observation-entity) | Observation child table which is linked to the act table. |
| `qty_obs_tbl` | [Quantity Observations](../conceptual-data-model/acts/act-data-dictionary.md#quantityobservation-entity) | Quantity Observation table which is linked with the observation table. |
| `txt_obs_tbl` | [Text Observations](../conceptual-data-model/acts/act-data-dictionary.md#textobservation-entity) | Text observations table which is linked with the observation table. |
| `cd_obs_tbl` | [Coded Observations](../conceptual-data-model/acts/act-data-dictionary.md#codedobservation-entity) | Coded observations table which is linked to the observation table. |
| `pat_enc_tbl` | [Patient Encounters](../conceptual-data-model/acts/act-data-dictionary.md#patientencounter-entity) | Patient encounters table which is linked to the act table. |
| `proc_tbl` | [Procedures](../conceptual-data-model/acts/act-data-dictionary.md#procedure-entity) | Procedures tablet which is linked to the act table. |
