# The Patient Dashboard

The SanteMPI patient dashboard is available for any patient which has been registered in the SanteMPI solution and shows the complete administrative view of the patient.

### Demographics Dashboard

![](../.gitbook/assets/image%20%2844%29.png)

The patient demographics dashboard is first shown when you open a patient's entity information in the SanteMPI platform. This sheet shows the key demographics the patient has, the relationships the patient has with other entities \(people, places, things, etc.\) as well as the Master / Local relationship. 

### Record Type Bar

Depending on the configuration of SanteDB, and the status of the currently viewed record, you will see an information bar appear under the patient header. This header will indicate:

* The record is a synthesized master record which has not been formally reviewed. The data presented represents an amalgamation of the local records.

![](../.gitbook/assets/image%20%2832%29.png)

* The record is a discrete record which was received and processed from a system. The data \(unless edited by a user\) represents the data found in the source system.

![](../.gitbook/assets/image%20%2872%29.png)

* The record is a master record which has been adjudicated by a person. The data you're seeing represents the data from the record of Truth. You can still see the source data by clicking on a local record in the **Master Data Management** tab.

![](../.gitbook/assets/image%20%2842%29.png)

No bar under the patient's summary header indicates that the data you're looking at has not been subjected to data management rules.

### Master Data Management Dashboard

On the MDM dashboard tab of the dashboard will present you with three panels where you can edit key details about the multi-instance storage of information.

![](../.gitbook/assets/image%20%28120%29.png)

### Entity Relationship View

The entity relationship panel allows you to quickly view the relationships between the various entities stored within the SanteDB service for the specified patient. 

![](../.gitbook/assets/image%20%284%29.png)

