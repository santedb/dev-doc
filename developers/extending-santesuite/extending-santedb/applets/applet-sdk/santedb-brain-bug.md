# SanteDB Brain Bug

The brain bug tool is named after the infamous "Brain Bug" from the movie Starship Troopers. The tool does exactly what that alien did, it extracts logs, files and databases from the dCDR Android Application.&#x20;

The tool was developed to overcome the fact that extracting Android backups is difficult on Microsoft Windows operating systems. To run the brainbug tool you will need the Android SDK installed on your Windows environment.

## Command Line Options

**Tool: `sdb-bb.exe`**

The following command line options are available for the brain bug tool.

| Option  | Description                                                                                                                                                                                                                                                           | Example               |
| ------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------- |
| help    | Show help for the tool and exit                                                                                                                                                                                                                                       | `--help`              |
| pkgid   | <p>Identifies the package of the android application you wish to extract</p><p>logs and files for. The package identifier is the <code>id</code> of your solution.</p>                                                                                                | `--pkgid=mm.mpi.app`  |
| sdk     | <p>If you've installed the Android SDK in a different location than the</p><p>default for your operating system, this is the path to the <br><code>adb.exe</code> tool.</p>                                                                                           | `--sdk="C:\android"`  |
| bkfile  | <p>If you wish to simply extract your application from the android</p><p>device and save it to ship to another developer, specify the </p><p>backup file. Conversely, if you wish to simply extract the contents</p><p>of a backup file, specify the backup file.</p> | `--bkfile=mybackup`   |
| tar     | <p>If you wish to extract a TAR file from the <code>.ab</code> file then specify<br>the tar archive to be saved. </p>                                                                                                                                                 | `--tar=mybackup.tar`  |
| extract | <p>If you wish to extract the contents of the backup directly to a</p><p>folder on your computer, this is the path to the extract location.</p>                                                                                                                       | `--extract=C:\issue1` |

