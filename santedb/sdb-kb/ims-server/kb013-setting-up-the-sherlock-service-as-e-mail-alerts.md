# HS002 - Setting up the "sherlock" service

**Purpose:** You wish to capture service reports from the field via e-mail or JIRA.

**Introduction:** The OpenIZ disconnected client allows users to file bug reports complete with log file and diagnostic information attached. This service is provided by the AMI's "sherlock" service. By default, the data submitted to this service is persisted through the IDataPersistenceService&lt;DiagnosticReport&gt; interface. OpenIZ ships with two implementations of this service:

* Atlassian JIRA - A web-based bug tracking and ticketing system
* E-Mail - Which e-mails diagnostic reports via SMTP.

**Applies To:** 

* OpenIZ Immunization Management Server 

**Steps:**

If you wish to setup the Atlassian JIRA target:

1. Open **C:\Program Files \(x86\)\Mohawk College\OpenIZ\openiz.exe.config** in a text editor 
2. Register the JIRA configuration section in the header of the file under **&lt;configSections&gt;**

   `<section name="openiz.persistence.diagnostics.jira" type="OpenIZ.Persistence.Diagnostics.Jira.Configuration.ConfigurationSectionHandler, OpenIZ.Persistence.Diagnostics.Jira, Version=0.6.0.0"/>`

3. Add the **&lt;openiz.persistence.diagnostics.jira&gt;** configuration section to your configuration file:

   ```text
      <openiz.persistence.diagnostics.jira>
      <jira url="url-to-jira" project="project"/>
      <auth username="username" password=""/>
      </openiz.persistence.diagnostics.jira>
   ```

   1. url = The endpoint for the REST services on JIRA \(note: you must enable this on the JIRA server\)
   2. project = The project in the JIRA service where you want new tickets to be created
   3. username = The user under which new tickets should be created
   4. password = The password for the user

4. Add the JIRA service to the **&lt;serviceProviders&gt;** section of the configuration file  

   `<add type="OpenIZ.Persistence.Diagnostics.Jira.DiagnosticReportPersistenceService, OpenIZ.Persistence.Diagnostics.Jira, Version=0.6.0.0"/>`

5. Restart the OpenIZ host process: 
   1. **net stop openiz**
   2. **net start openiz**

If you wish to setup the e-mail target:

1. Open **C:\Program Files \(x86\)\Mohawk College\OpenIZ\openiz.exe.config** in a text editor 
2. Register the JIRA configuration section in the header of the file under **&lt;configSections&gt;**

   `<section name="openiz.persistence.diagnostics.email" type="OpenIZ.Persistence.Diagnostics.Email.Configuration.ConfigurationSectionHandler, OpenIZ.Persistence.Diagnostics.Email, Version=0.6.0.0" />`

3. Add the **&lt;openiz.persistence.diagnostics.jira&gt;** configuration section to your configuration file:

   ```text
      <openiz.persistence.diagnostics.email>
    <smtp server="smtp://mail.domain.com:587" ssl="true" username="XXXXXXX" password="YTYYYYYY" from="fromaddress@domain.com" />
        <recipient>
            <add>user1@domain.com</add>
                       <add>user2@domain.com</add>
        </recipient>
    </openiz.persistence.diagnostics.email>
   ```

   1. server = The SMTP server through which mail should be routed
   2. ssl = Whether the SMTP server requires SSL
   3. username = The username to use when logging into the SMTP server \(or empty if open relay\)
   4. password = The password to use when logging into the SMTP server \(or empty if open relay\)
   5. from = The address which appears in the FROM: header
   6. recipient/add = Adds a recipient to which diagnostic reports should be sent.

4. Add the EMAIL service to the **&lt;serviceProviders&gt;** section of the configuration file  

   `<add type="OpenIZ.Persistence.Diagnostics.Email.DiagnosticReportPersistenceService, OpenIZ.Persistence.Diagnostics.Email, Version=0.6.0.0" />`

5. Restart the OpenIZ host process: 
   1. **net stop openiz**
   2. **net start openiz**

