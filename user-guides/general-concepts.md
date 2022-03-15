# Common User Interface Elements

All SanteDB administrative interfaces leverage a common user interface framework and design language. These common elements are consistent throughout any administrative or data panel regardless of the solution, plugin, or screen users are viewing.&#x20;

Users should familiarize themselves with these common concepts, as they are not covered in each screen.&#x20;

## Tables & Summary Data

In SanteDB's administrative panel, summary lists are displayed using client-side data tables. These tables have common functions for manipulating, filtering and editing objects displayed.&#x20;

Take, for example, the following list of identity domains.

![](<../.gitbook/assets/image (453) (1) (1).png>)

### Table / Global Actions

Actions which do not impact a specific record will be exposed as buttons at the top of any data table in SanteDB's administrative panel. Common actions which are shown in SanteDB include:

* Create - When present, allows a user to create a new record / entry for the data table being viewed.
* Reload - Forces the data table to re-query the server for new information.
* Show Deleted - When supported, changes the table from displaying active records, to showing records which have been removed.
* Export - When shown allows the user to export data (or data from the backing data source) to a downloadable format.

### Column Controls

Columns are used to display either a discrete field (such as name, OID, URLs, etc.) or a combination of fields (such as demographics, etc.). Fields that can be sorted are those which are primary fields on the object being displayed (i.e. they are not nested fields). This will be indicated by a sort control for columns which support sorting.

### Filtering / Searching

If supported by the resource, a data table may contain a search option above the table header. The field which is searched will depend on the resource being viewed, and is displayed as the placeholder for the search field.

Searches are executed against the server, meaning that each search on the data tables results in a new request to the server. Searches are performed as the user types into the search bar.&#x20;

### Provenance Information

The provenance column is usually shown as a "Created By", "Updated By", or "Deleted By" column. Provenance provides insights to the source of the information or the source of the last update/delete request to the object.&#x20;

Provenance will show:

* The User which executed the action
* The application which was used to execute the action
* The device which was used to execute the action
* During which session the action was executed

### Record Actions

Individual records, depending on their type, will permit actions directly from the summary table. These actions can typically include:

* View - Opens a new page with a detailed view of the object
* Edit - Opens an editor page which can be used to manipulate the object
* Delete - Removes the record from the SanteDB system
* Un-Delete - When supported, restores a previously deleted record into an active state
* Clone - Copies the object, creating a new clone of the object
* Export / Download - Allows for the downloading of the resource in a structured format from the server to the client's machine.

## Panels&#x20;

SanteDB provides a robust user interface extension mechanism which is exposed using [html-widgets.md](../developers/extending-santesuite/extending-santedb/applets/assets/html-widgets.md "mention"). These widgets are provided by plugins in the SanteDB administrative or user interface panels and render as either new tabs or new panels in a detail screen.

![](<../.gitbook/assets/image (439) (1) (1) (1).png>)

The panel may optionally show one or more action buttons (or alternate views):

* Edit Mode - Shown as a pencil button, the edit mode element allows users to switch the panel from view mode (default) into editing mode where data can be manipulated.
* Settings Mode - Shown as a cog, the settings mode allows users to customize what the panel is showing.
* Summary Mode - Shown as a chart icon, this mode allows users to switch between tabular/detail view mode and a summary chart mode.

### Saving Panel Data

When in settings or edit mode, a panel titlebar will show two icons for cancelling the change and submitting the change. Any changes made to the panel contents must be saved via the check button. The check button may be disabled when the form is incomplete or missing data.

![](<../.gitbook/assets/image (438) (1) (1) (1).png>)

## Contextual Help

As part of improving the usability of the SanteDB administrative panel, several screens have an option to display inline help. This function provides additional hints and tips for users while also reducing clutter on the screen.&#x20;

To access contextual help, simply hover the mouse cursor over the `?` icon in the user interface (or tap on a mobile device) and information about that data element, or function will appear.

![](<../.gitbook/assets/image (435) (1) (1) (1) (1).png>)
