# SanteDB Brain Bug

The brain bug tool is named after the infamous "Brain Bug" from the movie Starship Troopers. The tool does exactly what that alien did, it extracts logs, files and databases from the dCDR Android Application. 

The tool was developed to overcome the fact that extracting Android backups is difficult on Microsoft Windows operating systems. To run the brainbug tool you will need the Android SDK installed on your Windows environment.

## Command Line Options

**Tool: `sdb-bb.exe`**

The following command line options are available for the brain bug tool.

<table>
  <thead>
    <tr>
      <th style="text-align:left">Option</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left">Example</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">help</td>
      <td style="text-align:left">Show help for the tool and exit</td>
      <td style="text-align:left"><code>--help</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">pkgid</td>
      <td style="text-align:left">
        <p>Identifies the package of the android application you wish to extract</p>
        <p>logs and files for. The package identifier is the <code>id</code> of your
          solution.</p>
      </td>
      <td style="text-align:left"><code>--pkgid=mm.mpi.app</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">sdk</td>
      <td style="text-align:left">
        <p>If you&apos;ve installed the Android SDK in a different location than
          the</p>
        <p>default for your operating system, this is the path to the
          <br /><code>adb.exe</code> tool.</p>
      </td>
      <td style="text-align:left"><code>--sdk=&quot;C:\android&quot;</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">bkfile</td>
      <td style="text-align:left">
        <p>If you wish to simply extract your application from the android</p>
        <p>device and save it to ship to another developer, specify the</p>
        <p>backup file. Conversely, if you wish to simply extract the contents</p>
        <p>of a backup file, specify the backup file.</p>
      </td>
      <td style="text-align:left"><code>--bkfile=mybackup</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">tar</td>
      <td style="text-align:left">If you wish to extract a TAR file from the <code>.ab</code> file then specify
        <br
        />the tar archive to be saved.</td>
      <td style="text-align:left"><code>--tar=mybackup.tar</code>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">extract</td>
      <td style="text-align:left">
        <p>If you wish to extract the contents of the backup directly to a</p>
        <p>folder on your computer, this is the path to the extract location.</p>
      </td>
      <td style="text-align:left"><code>--extract=C:\issue1</code>
      </td>
    </tr>
  </tbody>
</table>



