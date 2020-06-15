# State Machine

SanteDB Act support attribution of the current status of an act using the state machine illustrated in Figure 2. 

![Figure 2 - Act States](../../../../../.gitbook/assets/image%20%2846%29.png)

The states of an act are:

* **New :** Indicates that the act has yet to be reviewed and//or that business processing rules have yet to be executed.
* **Active :** Indicates that an act is currently occurring or being actioned. This state is used, for example, if an encounter is still occurring however has not completed.
* **Complete :** Indicates that the act has occurred. If the act is of a mood code such as intent, request, etc, the _complete_ status indicates that the request or intent is complete and has been fulfilled.
* **Nullified :** Indicates that the act was created in error, and never occurred.
* **Obsolete :** Indicates that the act did occur, however the information is no longer accurate, or has been amended.

