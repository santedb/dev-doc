# MPI/CR Test Cases for HL7v2

These test cases are based on the OpenHIE CR tests for HL7v2 transactions, and contain specific hints for SanteMPI.

## Security Configuration

All tests for HL7v2 should ensure they are using either:

* [Node authentication ](../../../../../operations-1/standard-operating-procedures/santedb-hl7v2-implementation/hl7-authentication.md#node-authentication-using-x-509-certificates)- Meaning that an X.509 certificate environment has been configured on the MPI. Note that all device configurations should map the certificate to the credential for the device.
* [Msh8 Authentication](../../../../../operations-1/standard-operating-procedures/santedb-hl7v2-implementation/hl7-authentication.md#msh-8-authentication) - Meaning that `MSH-8` should carry necessary authentication information to authenticate the sending node.

For more information on how HL7v2 messages are authenticated in SanteDB, please consult the [HL7 Authentication](../../../../../operations-1/standard-operating-procedures/santedb-hl7v2-implementation/hl7-authentication.md) wiki article.

