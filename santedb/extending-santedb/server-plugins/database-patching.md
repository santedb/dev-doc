# Database Patching

Some plugins may require special indexing and/or patches to the underlying SanteDB schema. While this is generally not recommended \(you should attempt to use the built-in RIM concepts\), there are occasions where your plugin will need to touch the database.

### Patch SQL Files

Patching is done by including SQL files in your project as an Embedded Resource. The files should end in the extension .SQL and must contain a header with the following format:

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

The SanteDB updater config tool will read these manifests and allow the system administrator an option to install your patches to their database.

The schema is as follows:

<table>
  <thead>
    <tr>
      <th style="text-align:left">Element</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">@scope</td>
      <td style="text-align:left">The scope of the patch. This is typically to the main database (SanteDB.Persistence.Data.ADO)
        however some other SanteDB products (such as SanteGuard) define their own
        scopes.</td>
    </tr>
    <tr>
      <td style="text-align:left">@id</td>
      <td style="text-align:left">A unique identifier for your patch.</td>
    </tr>
    <tr>
      <td style="text-align:left">@name</td>
      <td style="text-align:left">The name of your patch, this appears as the title of the patch in the
        user interface</td>
    </tr>
    <tr>
      <td style="text-align:left">@applyRange</td>
      <td style="text-align:left">The range of database schema on which the patch is designed. SanteDB will
        not apply your patch if the database version is outside of this range.</td>
    </tr>
    <tr>
      <td style="text-align:left">@invariantName</td>
      <td style="text-align:left">
        <p>The name of the database provider the SQL applies to. Allowed values are:</p>
        <p>npgsql = PostgreSQL</p>
        <p>fbsql = FirebirdSQL</p>
        <p>sqlite = SQLite</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">summary</td>
      <td style="text-align:left">A textual summary of your patch.</td>
    </tr>
    <tr>
      <td style="text-align:left">remarks</td>
      <td style="text-align:left">More detailed documentation related to the patch.</td>
    </tr>
    <tr>
      <td style="text-align:left">isInstalled</td>
      <td style="text-align:left">SQL statement that, when evaluated to TRUE indicates that the patch does
        not need to be applied.</td>
    </tr>
  </tbody>
</table>

