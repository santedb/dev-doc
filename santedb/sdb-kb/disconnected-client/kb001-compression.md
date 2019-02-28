# KB001 - Improving Download Speeds on Slow Connections

**Issue:** When using the Disconnected Client from a device with a slow internet connection, downloads take a large amount of time.

**Applies To:** 

* OpenIZ Disconnected Client Android Application
* OpenIZ Disconnected Client Windows Application
* OpenIZ Disconnected Client Linux Application

**Symptoms:**

* Frequent timeouts or long waits for downloads
* Inability to login to the connected IMS
* Interrupted downloads on 2g/3g connections.

**Cause:** This issue is caused when the amount of bandwidth being used by the OpenIZ Disconnected Client is too large for the network timeouts. This can often result in the background processes giving up on sending or receiving data.

**Solutions:**

* If you are using OpenIZ Disconnected client &lt; 0.9.7.2 you can try
  * Turning the 2g/3g connection on/off again and attempting a re-synchronization
  * Connecting to a wi-fi network that has a more reliable internet connection 
  * Closing the application and restarting it again
  * Going offline and waiting until a better signal is available
* If you are using OpenIZ Disconnected client &gt; 0.9.7.2, in addition to the above steps, you can enable a higher grade of compression. This is done on initial setup under the network options.
  * Ultra - Will use the LZMA compression algorithm at the highest available level of compressing. This algorithm introduces additional server and tablet resource requirements as compressing LZMA streams is CPU intensive
  * High - Uses the BZip2 compression algorithm at a medium-high level of compression. This algorithm requires less resources than LZMA but usually results in poorer compression \(though better than GZIP\)
  * Medium - Uses the GZIP compression algorithm. This algorithm balances CPU requirements and compression ratios.
  * Fast/Low - Uses the deflate compression algorithm. This algorithm uses very little CPU on the server and tablet \(so is faster\) but has poorer compression quality than GZIP.
  * Off - Does not optimize traffic. This is intended for debugging only or when using a proxy which requires inspecting contents.

![](../.gitbook/assets/kb001-settings.png)

