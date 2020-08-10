# When sending a National Scoped ID in PID-19 \(SSN\) you receive "AuthorityUuid" missing error

**Issue:** When using the SanteDB dCDR via the HL7 ADT feed, new patients are not registered, rather you receive a NACK indicating a missing argument/parameter for AuthorityUUID

**Applies To:**

* SanteDB dCDR Gateway Kelowna \(Version 2.0.22+\)
* SanteDB iCDR + SanteMPI \(Version 2.0.22+\)

**Symptoms:**

* Upon sending a registration using PID-19, you receive a NACK as illustrated below

```text
MSH|^~\&|SENDER|LOCAL|MPI_SERVER|NATIONAL_DC|20200806100518|XXXXX|ADT^A04^ADT_A01|117631e6-8866-4d67-be10-4ed64e55b52b|P|2.3.1|||AL
EVN||202008061005+0630
PID|||XXXYYY^^^AUTHORITY^PT||SMITH^JOHN^^^^^U||1978|M|||||||||||403-304-302
NK1|1|^U Hla Shwe|FTH
PV1||I

MSH|^~\&|MPI_SERVER|NATIONAL_DC|SENDER|LOCAL|20200806100051||ACK^A04^ACK|cc103f57-4602-4590-83c8-741c9c834ee9||2.3.1
MSA|AE|117631e6-8866-4d67-be10-4ed64e55b52b|General Error|||207^Insert SanteDB.Core.Model.Collection.Bundle
ERR|^^^&Insert SanteDB.Core.Model.Collection.Bundle||207|E
ERR|^^^&Exception has been thrown by the target of an invocation.||207|E
ERR|^^^&Requires a value\X000d\Parameter name: AuthorityUuid||207|E
```

**Cause:** This rejection is caused because the ssnAuthority has not been configured for the dCDR or iCDR. 

**Solutions:**

If correcting the iCDR:

1. Open the file C:\Program Files\SanteSuite\SanteDB\Server\SanteDB.config.xml
2. Locate the section HL7Configuration
3. Add the &lt;ssnAuthority&gt; element \(below\) with the appropriate configuration of what identifier is being carried in the PID-19 field.
4. Save the file
5. Restart the SanteDB Host Process

If correcting the dCDR:

1. Open the file C:\WINDOWS\SYSWOW64\config\systemprofile\AppData\roaming\santedb\dcg-default\santedb.config
2. Locate the section HL7Configuration
3. Add the &lt;ssnAuthority&gt; element \(below\) with the appropriate configuration of what identifier is being carried in the PID-19 field.
4. Save the file
5. Restart the SanteDB Host Process

An appropriate ssnAuthority configuration is illustrated below:

```text
<ssnAuthority>
      <domainName xmlns="http://santedb.org/model">SOME_AUTHORITY_NAME</domainName>
</ssnAuthority>
```

