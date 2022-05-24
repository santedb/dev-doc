# Performance Settings

The performance group in the configuration tool controls the caching of data in SanteDB.

![](<../../../.gitbook/assets/image (422) (1) (1) (1) (1) (1) (1) (1) (1).png>)

The services installed by default on SanteDB are:

* REDIS Based Caching Services: These connect to the REDIS server and store objects in cache there. REDIS caching is useful in a scaled-out deployment where multiple application servers must share cached data between themselves.
* Memory Based Caching Service: These are local in-process caches. This type of caching service is useful for single process or single application servers.

The caching control panel is broken into two sections:

* Configuration Sections: Which are used to control the configuration of each class of caching, and
* &#x20;Services Section: Which is used to set the caching service/strategy used.

## Services Configuration

The services section is used to to control the implementations of the caching infrastructure.&#x20;

| Option               | Description                                                                                                                                                                              | Example |
| -------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------- |
| Data Object Cache    | The data object cache is used to store fully loaded objects from the database. This service reduces load on the database.                                                                |         |
| Ad-Hoc Cache         | The ad-hoc cache is used to  store any value which a plugin needs to store. These are typically used to cache policy decisions, policy information, term lookups, etc.                   |         |
| Stateful Query Cache | The stateful query cache is used to store stateful query results which are paginated on the client. Stateful queries are useful for freezing a result set to those at the time of query. |         |

## Cache Configuration

### REDIS Configuration

| Option             | Description                                                                                                                                                                 | Example                                                                    |
| ------------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| REDIS Server(s)    | The location of the REDIS server (or pool of servers) which should be used for caching.                                                                                     | `127.0.0.0:6729`                                                           |
| REDIS User         | If the REDIS server requires authentication (recommended) the username to use to authenticate with the REDIS server.                                                        |                                                                            |
| Password           | If the REDIS server requires authentication (recommended) the password which matches the username.                                                                          |                                                                            |
| TTL                | The Time To Live of objects stored in REDIS. Default is 15 minutes.                                                                                                         | <p><code>00:15:00</code> 15 Minutes</p><p><code>01:00:00</code> 1 Hour</p> |
| Broadcast Messages | If true, then the SanteDB server will broadcast updates to the REDIS server cache objects so that other SanteDB servers are notified when data in the REDIS server changes. |                                                                            |

### Memory Configuration

| Option              | Description                                                                                                                                                                       | Example       |
| ------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------- |
| Max Cache Size (MB) | The maximum amount of in-process memory to dedicate to caching objects.                                                                                                           | `1000` = 1 GB |
| Max Cache Age (S)   | The maximum length of time in seconds for cached objects to live in the cache before being evicted.                                                                               |               |
| Max Query Age (S)   | The maximum length of time (in seconds) for cached stateful queries to be retained before being evicted (note: callers must complete consumption of the query prior to this time) |               |
