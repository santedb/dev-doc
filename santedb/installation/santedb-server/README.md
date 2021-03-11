---
description: >-
  This page describes the planning stages and various deployment scenarios which
  SanteDB supports.
---

# SanteDB iCDR Server

## Minimum Requirements

SanteDB Server can be a light process, and requirements for running SanteDB Server will vary depending on your deployment and purpose. At minimum, SanteDB Server requires:

* **Operating System:** Windows Server 2008R2 SP1, Windows 7 SP2, Linux \(varies\), MacOS 10.9+
* **RAM:** 1 GB RAM minimum \(more if using Memory Caching\)
* **CPU:** Any \(multi-core system recommended\)
* **HDD:** 300 MB recommended

### Database Support

SanteDB Server runs on a variety of operating systems and a variety of RDBMS however not all RDBMS modules are available on all platforms.

| OS | PostgreSQL | FirebirdSQL |
| :--- | :--- | :--- |
| Windows | 9.6+, 10 | 3.0+ |
| MacOS | 9.6+, 10 | Not Supported |
| Linux | 9.6+, 10 | Not Supported |

#### PostgreSQL

PostgreSQL 9.6 or 10 are recommended for use with SanteDB, and are the only two versions of PostgreSQL with which SanteDB server is tested. Earlier versions of PostgreSQL may be supported, however some features or unexpected behaviors may occur.

Use PostgreSQL when:

* You are deploying to a training, testing, or production environment
* Your SanteDB server will be accessed by multiple clients
* You require the use of third party reporting, ETL, or query tools
* You need to support or scale out of your application server 

#### **FirebirdSQL**

FirebirdSQL 3.0 is also supported on Microsoft Windows based machines \(it could be supported on Linux with a few modifications\). FirebirdSQL provides a fully ACID compliant RDBMS solution while also being embedded within the SanteDB host process. This allows SanteDB Server to run without requiring setup of a third party database server.

Use FirebirdSQL when:

* You are setting up a development or testing server
* You need to easily wipe/backup/restore test datasets \(you can copy your FDB file and restart the service\)
* You need to setup a demonstration on a lower powered laptop
* You are evaluating a new SanteDB based product and want a quick solution for deployment

### Cache Support

SanteDB supports a caching as a query optimization strategy. The SanteDB cache is used to prevent further retrieval of resources from the database system, which is slower than system memory. In SanteDB there are two solutions for caching.

#### In-Process Memory Cache

The in-process memory cache is the easiest to setup. It requires no additional software services to be running and allows SanteDB Server to store objects in its own memory space. 

Use in-process memory caching when:

* You are setting up a development or testing server
* You don't want to setup a REDIS environment
* You don't need to scale out your application servers.

#### REDIS Cache

SanteDB Server also supports connecting to the NoSQL database REDIS. SanteDB Server uses REDIS as a cache solution which can be persisted or in-memory only.

Use REDIS caching when:

* You may need to scale out your application servers \(i.e. multiple servers accessing the shared REDIS cache\)
* You are setting up a production, training or staging environment and don't want a cold-start of the SanteDB server to result in cache misses.

