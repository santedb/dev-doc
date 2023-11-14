# Installing Software

SanteDB software packages support many different environments and use cases. The underlying software is attempting to provide a common structure into which data/processes can be realized. Because of this there are two different distributions of SanteDB software, which can be installed in an operational environment.

## iCDR - Integrated CDR

The iCDR is typically installed once per application role in a jurisdiction. (See:[#icdr-server](../../../../santedb/architecture.md#icdr-server "mention")).&#x20;

{% content-ref url="santedb-server/" %}
[santedb-server](santedb-server/)
{% endcontent-ref %}

## dCDR - Disconnected CDR

The dCDR is installed on the client side or in an aggregate setting as a gateway (or mini CDR). The distribution of the dCDR software and its installation is unique to each platform. This wiki covers the configuration of the dCDR to an iCDR instance.

{% content-ref url="disconnected-gateway/" %}
[disconnected-gateway](disconnected-gateway/)
{% endcontent-ref %}

