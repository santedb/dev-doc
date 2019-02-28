# HS005 - Installing the OpenIZ Disconnected Server

**Purpose:**  You wish to run an area hospital, or group of computers with a Local Area Network in disconnected mode. In this scenario, all the machines within the hospital are connected 24/7 via LAN however internet connectivity is limited.

**Introduction:**  In some cases, there may be scenarios where deployments that wish to run OpenIZ in an environment whereby several machines connect to the central IMS, however those machines are not always connected to the internet \(though are connected to each other via LAN\). This can be common for large clinics, hospitals, or rural service centres.

Such a deployment leverages the OpenIZ Disconnected Server.

**Applies To:**

* OpenIZ Disconnected Server

**Steps \(Linux\):**

1. On a Linux or Windows virtual machine install the following prerequisites:
   * Mono Framework 5 or higher \(Linux\)
   * NginX

     ```bash
     sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys    3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF
     echo "deb http://download.mono-project.com/repo/ubuntu xenial main" | sudo tee /etc/apt/sources.list.d/mono-official.list
     sudo apt-get update
     sudo apt-get upgrade
     sudo apt-get install nginx mono-complete
     ```
2. Download the OpenIZ disconnected server \(openiz-ds\) from the Mohawk MEDIC repository \(NB: This will download 1.0.1.0\)

   ```text
    wget https://github.com/MohawkMEDIC/openizdc/releases/download/v1.0.1.0/openiz-ds-1.0.1.0.tar.gz
    tar -xzvf openiz-ds-1.0.1.0.tar.gz
   ```

3. Start the Disconnected Server in console mode for configuration:

   ```text
    cd openiz-ds-1.0.1.0/
    mono DisconnectedServer.exe --console
   ```

4. Configure the service by navigating to [http://127.0.0.1:9200](http://127.0.0.1:9200)
5. Configure your Disconnected Server just like the normal Disconnected Client. When you are done you will see a notice that your server needs to be restarted. Press \[ENTER\] in the terminal running the Disconnected Server.
6. Re-start the server in console mode by running:

   ```text
    mono DisconnectedServer.exe --console
   ```

7. Edit the NGINX default site to forward requests on external port 8080 to local port 9200

   ```text
    sudo vi /etc/nginx/sites-available/default
   ```

   and provide this configuration detail:

   ```text
    location / {
        proxy_pass http://127.0.0.1:9200/;
        proxy_cookie_domain 127.0.0.1 $host;
    }
   ```

8. You should now be able to visit the Disconnected Server on a LAN on port 8080.

   **Note:** It is recommended that you configure TLS on NginX so that communications between the computers on the LAN and the server are encrypted.

