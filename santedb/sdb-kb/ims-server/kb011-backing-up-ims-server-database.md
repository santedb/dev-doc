# HS001 - Backing up IMS server database

**Purpose:** You wish to perform a complete backup of the OpenIZ primary data store, or a data store which OpenIZ uses.

**Introduction:** Backing up your database server is a routine procedure and should be performed on an automated schedule. This article will guide system administrators through the backup and restore process.

**Applies To:**

* OpenIZ Immunization Management Server \(running PostgreSQL database\)

**Steps:**

1. Open the **C:\Program Files \(x86\)\Mohawk College\OpenIZ\openiz.exe.config** file in a text edit
2. Navigate to the &lt;connectionStrings&gt; section and note the server, username and password for your primary OpenIZ connection string. For example, the connection below is pointing to _localhost_ with username _postgres_ and password _postgres._

   ```text
       <add name="PSQL_CLIN" 
          connectionString="server=localhost; database=openiz_staging; user id=postgres; password=postgres; " 
          providerName="Npgsql"/>
   ```

3. Open a command prompt and navigate to **C:\Program Files\PostgreSQL\9.4\bin** \(note: if you are using the bundled installation of OpenIZ your directory may be **C:\Program Files \(x86\)\Mohawk College\OpenIZ\PostgreSQL\bin**\)
4. Stop the OpenIZ service by typing : **net stop openiz**
5. Type the following command:

   ```text
   C:\Program Files\PostgreSQL\9.4\bin>pg_dump -h localhost -U postgres -W --dbname=openiz_staging > c:\temp\mybackup.sql
   Password:
   ```

   1. Enter your password when prompted

6. Restart the OpenIZ service by typing : **net start openiz**

If you need to restore a backup use the following instructions:

1. Open a command prompt and navigate to **C:\Program Files\PostgreSQL\9.4\bin** \(note: if you are using the bundled installation of OpenIZ your directory may be **C:\Program Files \(x86\)\Mohawk College\OpenIZ\PostgreSQL\bin**\)
2. Stop the openiz service by executing : **net stop openiz**
3. Run the command **psql -U postgres -W -h localhost**
4. **Optional:** In the SQL command prompt rename the current copy of your database to another name \(this will preserve the database in the server\)

   ```text
   postgres=# alter database openiz_staging rename to openiz_original;
   ALTER DATABASE
   ```

5. Create a new database to which to restore the backup: \(note: lines prefixed with postgres=\# are the inputs\)

   ```text
   postgres=# create database openiz_staging owner postgres;
   CREATE DATABASE
   postgres=# \c openiz_staging
   Password for user postgres:
   WARNING: Console code page (437) differs from Windows code page (1252)
            8-bit characters might not work correctly. See psql reference
            page "Notes for Windows users" for details.
   You are now connected to database "openiz_staging" as user "postgres".
   openiz_staging=#
   ```

6. Restore the database by using the **\i** command

   ```text
   openiz_staging=# \i /temp/mybackup.sql
   ```

   1. You may encounter errors on the first run, this is due to pg\_dump not adhering to foreign key constraints. If you receive an error such as that listed below, simply re-run the above command a second time:
   2. ```text
      psql:/temp/mybackup.sql:435254: ERROR:  new row for relation "act_ptcpt_tbl" violates check constraint "ck_act_ptcpt_rol_cd"
      DETAIL:  Failing row contains (6689a586-3c42-4a2d-bbdc-bec0843856ef, 41b008a6-fcf8-40bc-ab96-7567e94bcf8f, 74baee85-6e99-43d5-95ef-bc70edd0b554, 1, null, null, 99e77288-cb09-4050-a8cf-385513f32f0a, 0).
      CONTEXT:  COPY act_ptcpt_tbl, line 1: "6689a586-3c42-4a2d-bbdc-bec0843856ef     41b008a6-fcf8-40bc-ab96-7567e94bcf8f    74baee85-6e99-43d5-95ef-bc..."
      COPY 0
      ```

7. Start the OpenIZ host process by running **net start openiz**

