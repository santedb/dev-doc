# Instant OpenHIE

{% hint style="info" %}
This page is a draft, the software is currently evolving to support the Instant OpenHIE initiative.
{% endhint %}

## Summary

The Instant OpenHIE initiative seeks to provide rapid deployment of OpenHIE use cases using containerization and orchestration to allow users to establish demonstrative environments for particular use cases in OpenHIE. 

In the scope of SanteDB / SanteMPI, our Instant OpenHIE use cases are based on four fundamental principles:

* Miniaturize / Componentize the components in our Open Virtual Appliance \(OVA\) Template to Docker/Kubernetes containers
* Provide plugins to the configuration services \(via a custom [IConfigurationManager](../extending-santedb/server-plugins/service-definitions/iconfigurationmanager.md)\) which allow for overriding default configurations with custom ones
* Provide pre-packaged sample data, allowing spin-up of a demo environment within an OpenHIE environment.
* Document API interfaces that can be used by other Instant OpenHIE components to configure the SanteDB instance \(such as assigning authorities, policies, etc.\)

## Components

SanteDB solutions such as SanteMPI are based on the SanteDB iCDR, as such there are several containers that scheduled for development:

* santempi-core : A container which contains the Core CDR, data initialization scripts for a sample jurisdiction \(Elbonia\)
* santempi-cache : An optional container which contains a configured version of REDIS for caching data from the SanteMPI core container
* santedb-portal : An optional container which contains a configured version of the SanteDB web portal for graphical management



