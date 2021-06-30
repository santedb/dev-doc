# Security Administration

SanteDB provides a robust security environment. This security environment is maintained either through the web-administration panel, or the santedb administration console \(sdbac\).

### Security Center

The SanteDB security center provides a dashboard of your SanteDB security environment. The dashboard provides several key insights into your SanteDB solution.

![](../../../.gitbook/assets/image%20%28141%29.png)

### SanteDB Administration Console

The santedb administration console can be used to maintain a remote SanteDB server remotely where internet connectivity may be an issue \(too slow for the user interface to load properly\). The SanteDB administration console tool \(sdbac\) provides an interactive console shell which is capable of fetching logs, uploading applets, etc. 

![](../../../.gitbook/assets/image%20%285%29.png)

The sdbac tooling is described in more detail on the [administration console](../host-administration/santedb-icdr-admin-console/) page.

#### Demo Environment

To quickly access the administration console for executing sdbac commands in a [demo environment](../../installation/santedb-server/installing-a-development-demo-environment.md), follow these steps:

1. Download the latest .zip release of sdbac from [https://github.com/santedb/santedb-server/releases](https://github.com/santedb/santedb-server/releases) and unzip the contents into any directory.
2. Open a command prompt instance as an administrator and change the current working directory to where the unzipped contents of sdbac have been stored.
3. Execute the command: 

```text
sdbac -r elbonia.santesuite.net --port=8443 --tls
```

{% hint style="info" %}
Use credentials for the [demo environment](../../installation/santedb-server/installing-a-development-demo-environment.md) \(Administrator/Mohawk123\).
{% endhint %}

