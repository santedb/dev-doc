# Database Patching

Some plugins may require special indexing and/or patches to the underlying SanteDB schema. While this is generally not recommended (you should attempt to use the built-in RIM concepts), there are occasions where your plugin will need to touch the database.

### Patch SQL Files

Patching is done by including SQL files in your project as an [Embedded Resource](https://ikriv.com/blog/?p=1530#:\~:text=Embedded%20Resources%20Embedded%20resources%20are%20the%20same%20as,output%20will%20have%20a%20manifest%20resource%20named%20MyProject.Texts.Guide.txt.). The files should end in the extension .SQL and must contain a header with the following format:

```sql
/** 
 * <feature scope="SanteDB.Persistence.Data.ADO" 
 *     id="YOUR_PATCH_ID" 
 *     name="Update:20170725-01" 
 *     applyRange="0.2.0.0-0.9.0.1"  
 *     invariantName="npgsql">
 *	<summary></summary>
 *	<remarks></remarks>
 *	<isInstalled>select ck_patch('YOUR_PATCH_ID')</isInstalled>
 * </feature>
 */

 BEGIN TRANSACTION ;

-- DO YOUR WORK HERE

SELECT REG_PATCH('YOUR_PATCH_ID');

COMMIT;
```

{% hint style="info" %}
When writing FirebirdSQL patches you should add FROM RDB$DATABASE to the ck_patch and reg patch functions such as `SELECT REG_PATCH('MYPATCH') FROM RDB$DATABASE;`
{% endhint %}

The SanteDB updater config tool will read these manifests and allow the system administrator an option to install your patches to their database.

The schema is as follows:

| Element        | Description                                                                                                                                                                     |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| @scope         | The scope of the patch. This is typically to the main database (SanteDB.Persistence.Data.ADO) however some other SanteDB products (such as SanteGuard) define their own scopes. |
| @id            | A unique identifier for your patch.                                                                                                                                             |
| @name          | The name of your patch, this appears as the title of the patch in the user interface                                                                                            |
| @applyRange    | The range of database schema on which the patch is designed. SanteDB will not apply your patch if the database version is outside of this range.                                |
| @invariantName | <p>The name of the database provider the SQL applies to. Allowed values are:</p><p>npgsql = PostgreSQL</p><p>fbsql = FirebirdSQL</p><p>sqlite = SQLite</p>                      |
| summary        | A textual summary of your patch.                                                                                                                                                |
| remarks        | More detailed documentation related to the patch.                                                                                                                               |
| isInstalled    | SQL statement that, when evaluated to TRUE indicates that the patch does not need to be applied.                                                                                |

### Auto-Deploy of Patches

You should set your SQL file's compile action to `EmbeddedResource `in your plugin. Upon service start (on Windows, Linux, Android, or Docker) your SQL patch file will be executed and the database migrated.
