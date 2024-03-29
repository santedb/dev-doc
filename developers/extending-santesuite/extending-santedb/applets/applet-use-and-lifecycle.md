# Applet Use and Lifecycle

Applets are designed to be packaged and digitally signed for distribution in a production environment. Any of the iCDR and dCDR implementations use applets as the source of end developer components. The manner in which applets are used depends on the context:

Applets are distributed from the iCDR server to dCDR clients which are connected to it. This is useful since the packaging and digital signature of an applet ensures operators of SanteDB that the packages have not been tampered or changed since receipt from the original developer.

However, since the standard iCDR and dCDR components only load and operate with packaged applets, this makes debugging and developing applets challenging. This is the rationale behind the SanteDB Applet SDK.
