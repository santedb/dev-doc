# Concept Dictionary Data Dictionary

The [Conceptual Concept Dictionary](../conceptual-data-model/concept-dictionary/data-dictionary.md) expressed in the physical data model in ADO.NET providers is illustrated below.

![](../../../../.gitbook/assets/image%20%28410%29.png)

| Physical Table | Conceptual Entity | Description |
| :--- | :--- | :--- |
| `cd_tbl` | [Concept](../conceptual-data-model/concept-dictionary/data-dictionary.md#concept) | Non-versioned properties of the concept table. |
| `cd_vrsn_tbl` | [Concept Version](../conceptual-data-model/concept-dictionary/data-dictionary.md#concept-version) | Versioned properties of the concept table. |
| `cd_name_tbl` | [Concept Name](../conceptual-data-model/concept-dictionary/data-dictionary.md#concept-name) | Human readable names of the concept in various languages. |
| `cd_rel_assoc_tbl` | [Concept Relationship](../conceptual-data-model/concept-dictionary/data-dictionary.md#concept-relationship) | Concept relationships table. |
| `cd_rel_typ_cdtbl` | [Concept Relationship Type](../conceptual-data-model/concept-dictionary/data-dictionary.md#concept-relationship-type) | Concept Relationship types reference code table. |
| `cd_set_tbl` | [Concept Set](../conceptual-data-model/concept-dictionary/data-dictionary.md#concept-set) | Concept Set definition table. |
| `cd_set_mem_assoc_tbl` | Concept Set Member | Concept Set &lt;&gt; Concept relationship associative table. |
| `cd_ref_term_assoc_tbl` | [Concept Reference Term](../conceptual-data-model/concept-dictionary/data-dictionary.md#concept-reference-term)  | Concept &lt;&gt; Reference Term associated table. |
| `ref_term_tbl` | [Reference Term](../conceptual-data-model/concept-dictionary/data-dictionary.md#reference-term) | Reference term definition table. |
| `ref_term_name_tbl` | [Reference Term Name](../conceptual-data-model/concept-dictionary/data-dictionary.md#reference-term-display-name) | Preferred display names of the reference term \(when being represented on a standards interface\) |
| `cd_sys_tbl` | [Code System](../conceptual-data-model/concept-dictionary/data-dictionary.md#code-system) | Code system table |

