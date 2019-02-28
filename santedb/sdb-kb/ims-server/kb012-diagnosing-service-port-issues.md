# KB012 - Diagnosing service port issues

**Issue:** When starting up the OpenIZ immunization management service, the service interfaces appear to be unavailable.

**Applies To:**

* OpenIZ Immunization Management Service

**Symptoms:**

* OpenIZ Host Process does not start with one of the following errors:
  * Port reservation for [http://+:8080/](http://+:8080/) failed
  * WCF Exception - Port is in use
* OpenIZ Host Process starts when configured for HTTPS however the service is not accessible.

**Cause:** Typically these symptoms are caused by improper security settings on the server environment or from a server port conflict. Usually OpenIZ hosts will run on port 8080 when not secured and 8443 when secured by SSL.

**Solution:**

If you encounter the issue regarding conflicting port numbers, try changing the port:

1. Open **C:\Program Files \(x86\)\Mohawk College\OpenIZ\openiz.exe.config** in a text editor
2. Navigate to the **&lt;system.serviceModel&gt;** section and locate the **&lt;service&gt;** entry which is causing the issue, change the **baseAddress** and **address** attributes to a different port number.

   ```text
   <service name="OpenIZ.Authentication.OAuth2" behaviorConfiguration="oauth2_behavior">
     <host>
       <baseAddresses>
         <add baseAddress="http://0.0.0.0:8080/auth"/>
       </baseAddresses>
     </host>
     <endpoint address="http://0.0.0.0:8080/auth" binding="webHttpBinding" name="OpenIZ.Authentication.OAuth2" contract="OpenIZ.Authentication.OAuth2" bindingConfiguration="oauth2_binding"/>
   </service>
   ```

3. Restart the OpenIZ host process with 
   * **net stop openiz**
   * **net start openiz**

If you encounter an error indicating port reservation failed, reserve the port for the service user which OpenIZ host process is running on:

1. Open a command prompt as a Windows Administrative user.
2. Type the following command substituting **user** with the user under which the OpenIZ host process operates and the **url** parameter with the URL reservation from the error code.

   ```text
   netsh http add urlacl url=http://+:8080/imsi user=myser
   ```

3. Attempt to start the OpenIZ Host process again with
   * **net start openiz**

If the OpenIZ host process starts successfully, however you cannot access the service and are using HTTPS, enable your registered SSL certificate for the endpoint.

1. Open **C:\Program Files \(x86\)\Mohawk College\OpenIZ\openiz.exe.config** in a text editor
2. Navigate to the **&lt;system.serviceModel&gt;** section and locate the **&lt;service&gt;** entry which is causing the issue, note the port on which the service is running and the **behaviorConfiguration** attribute.
3. Navigate to the **&lt;behaviors&gt;** section and locate the behavior entry noted in the **behaviorConfiguration** and copy the **findValue** attribute.

   ```text
   <behavior name="ami_behavior">
    <serviceCredentials>
       <serviceCertificate storeLocation="LocalMachine" storeName="My" x509FindType="FindByThumbprint" findValue="certificate thumbprint"/>
       </serviceCredentials>
   ```

4. Open a command prompt as a Windows Administrative user.
5. Generate a random UUID for your registry entry \(you can use [https://www.uuidgenerator.net/](https://www.uuidgenerator.net/)\)
6. Run the following command to reserve the SSL certificate substituting **ipport** with the public IP of the machine \(or 0.0.0.0 for all IP addresses\) and port the service is listening on, substituting **certhash** with the copied **findValue** from step \#3.

   ```text
   netsh http add sslcert ipport=0.0.0.0:8443 certhash=certificate_thumbprint appid={uuid}
   ```

7. Restart the OpenIZ host process with 
   * **net stop openiz**
   * **net start openiz**

