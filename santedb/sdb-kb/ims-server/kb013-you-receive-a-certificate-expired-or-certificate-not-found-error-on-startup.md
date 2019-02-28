# KB013 - You receive a certificate expired or certificate not found error on startup

**Issue:** When starting up the IMS service the HTTPS services stop working or provide a certificate expired error.

**Applies To:**

* OpenIZ Immunization Management Server

**Symptoms:**

* When starting up the IMS you see a log file which lists a certificate not found or certificate is invalid error
* When navigating directly to the IMSI or AMI services \(or any other service secured with a certificate\) you notice a red address bar in the browser.

**Cause:** The primary cause of this error is either the certificate installed is not complete \(does not have the private key\), is expired \(expiry time has passed\), is not a valid SSL certificate for HTTP traffic \(i.e. is a code signing certificate\), or is not installed on the server.

**Solution:**

1. Verify the certificate is installed on the machine and has a private key:  
   1. Launch a new Microsoft Management Console by pressing **Windows + R** and typing **mmc**  
   2. Select **File &gt; Add / Remove Snap-In**

   ![](../.gitbook/assets/kb013-snapin.png) 3. Select the **Certificates** snap-in

   ![](../.gitbook/assets/kb013-certificatesnap.png) 4. Select **Computer Account** and press **Next**

   ![](../.gitbook/assets/kb013-computeraccount.png) 5. Select **Local Computer** and \*\*Finish

   ![](../.gitbook/assets/kb013-finishwizard.png) 6. Expand the **Certificates &gt; Personal &gt; Certificates** tree and verify that the certificate is installed on the local machine. The certificate is installed with a private key if it appears in the list with a key icon.

   ![](../.gitbook/assets/kb013-verifyinstalledwithkey.png)

2. If the certificate is not installed, you can import it. 1. Ensure that you acquire a PFX file from your certification authority. 2. Right click on the **Personal** folder in the administration console and select **All Tasks &gt; Import**

   ![](../.gitbook/assets/kb013-importmenu.png) 3. Select the PFX file that was provided by your certificate authority and enter the password, completing the import process.

   ![](../.gitbook/assets/kb013-certificatepassword.png)

3. Register the certificate in the configuration file 1. In the MMC panel \(if you have not opened it see above\) locate the certificate you want to secure your service with. Double click on the certificate and select the details tab. Locate the **serial number** attribute and copy the value.

   ![](../.gitbook/assets/kb013-copyserialnumber.png) 2. Open **C:\Program Files \(x86\)\Mohawk College\OpenIZ\openiz.exe.config** in a text editor 3. Locate the **&lt;system.serviceModel&gt;** section and find the **&lt;service&gt;** to which you want to apply the certificate. Change the **baseAddress** and **address** attributes' scheme to HTTPS and change the port to 8443 \(or other port that is open\). Take note of the **behaviorConfiguration** attribute:

   ```text
      <service name="RISI" behaviorConfiguration="risi_behavior">
        <host>
          <baseAddresses>
            <add baseAddress="https://0.0.0.0:8443/risi" />
          </baseAddresses>
        </host>
        <endpoint address="https://0.0.0.0:8443/risi" binding="webHttpBinding" name="RISI" contract="RISI_1.0" bindingConfiguration="risi_binding" />
      </service>
      </services>
   ```

   1. Locate the appropriate **&lt;behavior&gt;** element. If necessary add the **&lt;serviceCredentials&gt;** element \(if it is present do no add another entry, simply update the existing\). Paste the copied serial number to the **findValue** attribute ensuring to remove any hidden characters or spacing between digits:

      ```text
      <behavior name="risi_behavior">
          <serviceCredentials>
            <serviceCertificate storeLocation="LocalMachine" storeName="My" x509FindType="FindByThumbprint" findValue="68aaae85346680a1458d71271b940438"/>
          </serviceCredentials>
      ```

   2. Open a command prompt as a Windows Administrative user.
   3. Generate a random UUID for your registry entry \(you can use [https://www.uuidgenerator.net/](https://www.uuidgenerator.net/)\)
   4. Run the following command to reserve the SSL certificate substituting **ipport** with the public IP of the machine \(or 0.0.0.0 for all IP addresses\) and port the service is listening on, substituting **certhash** with the copied **findValue** from step \#3.

      ```text
      netsh http add sslcert ipport=0.0.0.0:8443 certhash=68aaae85346680a1458d71271b940438 appid={b751f248-8cf6-4d2b-b8bf-0302d5a52226}
      ```

   5. Restart the OpenIZ host process with 
      * **net stop openiz**
      * **net start openiz**

