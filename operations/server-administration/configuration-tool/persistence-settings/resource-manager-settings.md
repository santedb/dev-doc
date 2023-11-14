# Resource Manager Settings

The resource manager settings panel is used to specify the control of automatic linking, merging and governance of resource edits in the system. The resource manager specifies the persistence strategy used (either MDM, SIM, or none which is the default mode of operation).

![](<../../../../.gitbook/assets/image (511).png>)

You can specify the resource manager you'd like to control resources in your deployment of the iCDR.

* MIDM Data Repository => Indicates that the storage, linking, and de-duplication of objects should be controlled by the Master Data Management service.
  * Multiple copies of resources are kept representing the source system's view of that data
  * Merge and un-merge are non-destructive links within the database
* SIM Data Repository => Indicates that the storage, linking, and de-duplication of objects should be controlled by the single instance mode service.&#x20;
  * A single "golden" copy of a record is maintained by the iCDR - source systems are performing updates on the golden copy.
  * Merge is destructive action and un-merge is not possible

You can specify the resources which you'd like to be managed using the strategy by checking their resource registration in the **Resources** property editor.
