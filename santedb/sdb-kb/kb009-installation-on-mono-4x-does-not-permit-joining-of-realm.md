# KB009 - Installation on Mono 4.x does not permit joining of realm

**Issue:** When you install the Disconnected Client on Linux or MacOS, you are able to launch the setup page, however are unable to join any realm.

**Applies To:**

* OpenIZ Disconnected Client for Linux

**Symptoms:**

* When joining the realm you receive an error which says : "The realm cannot be contacted"

**Cause:**The cause of this is Mono 4.x lacks support for some of the .NET 4.5 features that the disconnected client uses. Namely, the remote certificate validation callback on the Mono 4.x framework throws a Missing Method Exception.

**Solution:**

* You will need to update you version of Mono to 5.x.
* On Ubuntu based systems:

```bash
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
echo "deb http://download.mono-project.com/repo/ubuntu xenial main" | sudo tee /etc/apt/sources.list.d/mono-official.list
sudo apt-get update
sudo apt-get upgrade
```

* On MacOS 
  * Download [http://www.mono-project.com/download/\#download-mac](http://www.mono-project.com/download/#download-mac)

