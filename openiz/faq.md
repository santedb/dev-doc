---
description: Frequently Asked Questions Regarding OpenIZ and SanteSuite
---

# FAQ

## How does OpenIZ relate to SanteDB?

OpenIZ was the precursor technology for SanteDB. OpenIZ contains a clinical data repository and disconnected clients which formed the basis of SanteDB's iCDR and dCDR products. The SanteDB project was created because, during deployment, several enhancements were identified for OpenIZ which require a significant expansion of the technology which OpenIZ could not support.

Also, SanteDB more accurately expresses the generic nature of the CDR technology, where OpenIZ "sounds" like it is only an EIR platform.

## Why do SanteSuite and MEDIC both have forks of OpenIZ?

The SanteSuite community has forked several of the products being ported to SanteDB in order to better service the community. The SanteSuite community forks of OpenIZ and MEDIC CR are the forks which will most continue to receive updates to the software from SanteSuite community members. 

## Are SanteDB and OpenIZ compatible?

You can upgrade your OpenIZ database to SanteDB \(there are automated scripts to do this\), however any plugins and software will need to be rewritten. There are several factors which necessitate this:

1. The XML namespaces in http://openiz.org have been moved to http://santedb.org
2. The code namespaces have changed from OpenIZ.\* to SanteDB.\*
3. Because we dropped support for Android 4.x,any JavaScript APIs need to be rewritten to use the new Promise architecture.
4. Because the server components have been updated to run on Linux, MacOS and Windows, the API bindings need to be changed.

## Does that mean OpenIZ isn't supported anymore?

No, OpenIZ will continue to be supported until at least 2021 and several features from SanteDB have been requested to be back-ported to OpenIZ which will result in a new minor version of OpenIZ. 



