# Audit Repository

## Purpose of Audits

Auditing represents official inspection of user accounts. SanteSuite logs **timestamped** **events** that occur when **actors** perform **actions** within the application that may result in various **outcomes**. 

![](../../../.gitbook/assets/purpose_highlight.png)

## Reviewing Audits

Audits can be sorted and filtered by:

* **Action** - can be Execute, Create, Read, Update, Delete depending on an event action.
* **Event** - can be Security Alert, Authentication, Import Data, Export Data, or Query depending on what an actor does in the application that is being logged for auditing.
* **Outcome** - can be Success, Minor/Moderate Fail, Serious Fail, ui.model.audit.outcome.epic

Additional details are provided when viewing an audited event \(by clicking a 'View' button in the 'Actions' column\) with details about the:

1. Event Information
2. Network
3. Users & Computers
4. Data & Objects

![](../../../.gitbook/assets/purpose_highlight2.png)

### Event Information

| Label | Description |
| :--- | :--- |
| EID | Event ID. |
| Action | Operation triggering the event; can be either _execute, create, read, update, delete_. |
| Event | Security code representing the event triggered by an action; can be either _Security Alert, Authentication, Import Data, Export Data,_ _query_. |
| Timestamp | Datetime of the event. |
| Outcome | Result of the action triggering the event; can be either _Success, Minor/Moderate Fail, Serious Fail, ui.model.audit.outcome.epic._ |
| Process | Name of the SanteDB process and corresponding process ID handling the event. |
| Source |  |

### Network

The following network diagrams show how each may differ depending on the event action: 

![Diagram showing direction of data transfer between user and device during an execute action.](../../../.gitbook/assets/network_execute.png)

![Diagram showing direction of data transfer between user and device during a read action.](../../../.gitbook/assets/network_read.png)

| Label | Description |
| :--- | :--- |
| URL |  |

### Users & Computers

| Label | Description |
| :--- | :--- |
| User Name | Name of the user that triggered the event with an action. |
| Machine | Name of the device where the event was triggered from. |
| R |  |
| Roles | Name\(s\) of any roles associated with the User that triggered the event. |

### Data & Objects

| Label | Description |
| :--- | :--- |
| Type |   |
| LC |  |
| Role |  |
| ID |  |

