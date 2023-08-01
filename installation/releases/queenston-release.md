# Queenston Release

As part of improving documentation of the SanteDB release documentation, each code named release will have its development versions (odd number minor versions) on a single page with the official versions (even number minor versions).&#x20;

Since this new method of documenting releases has only started with 2.1.170, this page is partial. One should consult the GitHub release schedules for more information.

## Version 2.2.3

Release Assets: [http://santesuite.org/assets/uploads/santedb/community/releases/2.2.3/](http://santesuite.org/assets/uploads/santedb/community/releases/2.2.3/)

* Fixes bug with the deletion of pub-sub subscriptions from the user interface
* Fixes un-delete operation on the pub-sub subscription manager
* Adds persistent job state service
* Adds default implementation of job state service (local XML file - work is being performed on the shared state service).

## Version 2.2.1

Release Assets: [http://santesuite.org/assets/uploads/santedb/community/releases/2.2.1.10/](http://santesuite.org/assets/uploads/santedb/community/releases/2.2.1.10/)

This release of SanteDB builds on the fixes in 2.2.0 and corrects adds the following enhancements:

* Fixes bug with blocking on `metaphone` and `dmetaphone` on PostgreSQL (improper parameter exception)
* Adds better descriptions to the SanteGuard view screens for user activity and audit trail.
* Updates to the audit detail view which uses the registered resource viewer (in order to open more types of data)
* Adds link to the detailed audit entry in the audit trail and activity tabs
* Fixes issue with job scheduling (present in 2.2.0) setting the appropriate type of schedule in the `xcron.xml` file.
* Adds ability to download match configuration source files in XML to port the configuration over to other systems.

## Version 2.2.0 (Official)  / 2.1.180 (CTP)

Release Assets: [http://santesuite.org/assets/uploads/santedb/community/releases/2.2.0/ ](http://santesuite.org/assets/uploads/santedb/community/releases/2.2.0/)

This is the second official stable release of the .NET Standard version of the SanteDB platform and related assets. The products which are included in the 2.2.0 release of SanteDB are:

* SanteDB iCDR Server 2.2.0
* SanteMPI iCDR Server 2.2.0
* SanteDB dCDR Web Access Gateway 2.2.0
* SanteDB dCDR Software Development Kit 2.2.0

This release includes all major upgrades and updates to the SanteDB platform from the 2.1.x Community Technology Preview release streams and is suitable for testing. There will be a normalization period for this release, however, since it is an official release of SanteDB iCDR it will receive an official maintenance branch and will have generally, more stable APIs.

Following the release of the 2.2.0 all future 2.1.x Community Technology Previews will be for the Regina release.&#x20;

### Enhancements

* SanteDB/SanteMPI Core iCDR Enhancements
  * Enhancements to HL7 FHIR interface:
    * Support for FHIR operations (`$operation`)
    * Implementations of `$match`, `$validate`, `$ihe-pix`, `$process-message` operations
    * Support for FHIR messaging bundles and transaction bundles
    * Support for FHIR subscriptions and FHIR push notifications
    * Enhanced support for FHIR resources `Patient`, `RelatedPerson`, `Organization`, `Practitioner`
    * Implementation of IHE PMIR messaging
  * Enhancements to HL7 Version 2 Interface:
    * Enhanced support for HL7 Z-Segments in messages
    * Enhanced processing of HL7 datatypes and handling of errors
  * New MDM Layer
    * Refactored complete MDM layer to support establishment of ROT from determiner codes
    * Improved functions for MDM auto-linking and candidate resolution
    * Support for unlink and re-link operations
    * Implementation of MDM enhanced HDSI operations `$mdm-link`, `$mdm-rematch`, `$mdm-ignore`.
  * Enhancements to HDSI
    * Support for HDSI operations via `$operation` name
    * Support for HDSI deep-linked child records (cleaned up implementation to be pluggable)
    * Enhanced HTTP caching for `If-None-Match`
  * Enhancements to matching engine
    * Implementation of update/save configuration files over HTTP APIs
    * New blocking algorithms for `similarity` and `similartiy_lev`
    * Added new blocking logic to allow for specifying ignore keys on master or sources
    * Added diagnostics / debugging / tracing collectors
  * Enhancements to probes interfaces
    * New probes implemented for CPU, Memory, ADO.ET connection, thread pooling, etc.
  * Enhanced thread pools for REST APIs and core functions which can scale-up or scale-down threads (without polluting the .NET threadpool)
  * Updated documentation of core API classes and interfaces
  * Automatically seed/create and update/patch database schemas
  * Enhanced BIS functions for storing materialized
  * Enhanced `IJob` management, scheduling and control
  * New Configuration Tool which can be used for setting/modifying settings on the iCDR host in Windows or Linux
  * Added classification, strength, and role codes to entity, act relationships and participations.
  * Implementation of MSMQ queue provider
* SanteDB Administrative Interface Enhancements
  * System Administration Screen Additions
    * System Probes manager screen
    * Dispatcher queue management screen
    * Pub/Sub management screen
  * Security Administration Enhancements
    * User, group, device, and application screens now modular (have extension points)
    * Re-envisioned audit viewing screen and audit center
  * MPI Management Screens
    * Enhanced entity relationship diagrams
    * Master Data Management screens for match/merge/unlink
    * SanteMPI matches panel
      * Detailed match overview screen
      * Resolve/Ignore functions on summary view
      * Reports for match details including full match export (< 10k rows)
    * SanteMPI Match Configuration
      * Edit/View match configuration metadata
      * Edit/View match blocking configuration&#x20;
      * Edit/View match scoring with compete algorithm selection for each attribute
      * Edit/View match classification stage for classifying results
      * Test match configuration functions
    * New free-text and advanced (per-field) search
    * New power search function
* SanteDB dCDR Web Access Gateway Enhancements
  * Self-restart of web access gateway after configuration
  * Ability to run in Docker, Linux or Windows service environments
* SanteDB dCDR SDK Enhancements
  * Enhanced pakman.exe manager
    * Supports local package repository resolution for applet debugger
    * Supports publish to remote package repository / server
  * Enhanced applet debugger environment which can load references by name
  * New vocabulary import tool which can import FHIR>Dataset or CSV>Dataset (for reference terms only)
  * New patient importer which can import ONC or FEBRL datasets

## Version 2.1.175 (CTP)

**Release Assets:** [http://santesuite.org/assets/uploads/santedb/community/releases/2.1.175/](http://santesuite.org/assets/uploads/santedb/community/releases/2.1.175/)

This is a minor release which correct small performance and caching issues. Included in this fix are:

* Addresses over-threading of the rest and internal background job thread pool (adds option to use .NET thread pool for all services)
* Addresses under-caching issues where client using `If-None-Match` would not receive a cached version but would hit the database.
* Fixes issues with the new version of NPGSQL related to handing of DateTime and DateTimeOffset
* Adds units of measure to the dCDR Web Access Gateway admin portal on probes
* Fixes issue where scheduled tasks (starting before date of startup) are executed on start rather than waiting until the next execution window
* Adds performance probes for:
  * .NET Thread Pool I/O and Worker Threads
  * ADO.NET Database Connections (active read/write, statements being executed)
* Adds ability to change blocking instructions to operate on MASTER or SOURCE mode
  * Fixes issues with ignored records when blocking is performed in SOURCE mode
* Adds new `date_trunc` filter expression for HDSI queries. This is more efficient than `date_diff` in that it allows date column indexes to be used.
* Increases performance of `levenshtein` filter function on PostgreSQL by changing logic from : `where levenshtein(column_name, ?) < value` to `where column_name % ? and levenshtein(column_name, ?) < value` which allows PostgreSQL to use the GIN indexing to reduce the number of rows passed to levenshtein function.

## Version 2.1.170.1 (CTP)

**Release Assets:** [http://santesuite.org/assets/uploads/santedb/community/releases/2.1.170.1/](http://santesuite.org/assets/uploads/santedb/community/releases/2.1.170.1/)

This version is a patch for the 2.1.170 release. It fixes the following issues found in 2.1.170:

* Fixes logic for timer jobs based on calendar to reduce the "greedyness" of the jobs
* Fixes display caching issue (was an issue with the BulkPurge function) so new data is properly rendered.
* Fixes some threading issues with the .NET ThreadPool on background matching

## Version 2.1.170 (CTP)

Release Assets: [http://santesuite.org/assets/uploads/santedb/community/releases/2.1.170/](http://santesuite.org/assets/uploads/santedb/community/releases/2.1.170/)

### Features / Fixes:

* Added ability to schedule `IJob` jobs within the administrative panel
* Added job descriptions to the job screen
* Added ability to more efficient background matching on the match job
* Added default .NET thread pool as the default implementation of `IThreadPoolService` and changed the way that the probe data is displayed.
* Added `useLowerLayer` attribute to the `<blocking>` instructions in match configuration. This allows for configurations to bypass master synthesization (see notes below)
* Added configuration to the match screens in the administrative panel to allow for selection of absolute scoring or normalized scoring.
* Added ability to customize the free-text algorithm used for translating search terms into `tsquery` results (see:&#x20;
* Fixed matching engine bug where the record's self was not excluded from result.
* Fixed matching `auto-merge` bug (see above fix for cause)

### Known Issues:

* The entity relationship graph on the patient profile screen will show duplicate links
* Caching of some entities shows erroneous data on the relationship graphs. Validation of the state at database reveals this is a caching issue.&#x20;
* Running the background matching task in Linux or Docker can result in CPU use at 100% as the `ThreadPool` and `ConcurrentQueue<T>` implementations in Mono framework appear to be implemented in a slightly, less efficient manner.
* There is a display bug for entities which have been auto-merged using the `$mdm.auto-link` flag where the resulting source record will display multiple relationships (indicating they are active when they are not).&#x20;

### PostgreSQL FreeText Search

The new version of the SanteDB `_any` parameter handling uses the free-text engine. In PostgreSQL this method calls the function `fti_tsquery` function. This function is passed a single text parameter and is expected to return a `tsquery` structure.&#x20;

By default, 2.1.170 uses the `websearch_to_tsquery` method. This search method was introduced in PostgreSQL 11 and converts a search string into a tsquery method. Implementers may wish to change this behavior if:

* They are using PostgreSQL < 11&#x20;
* They wish to use other free-text search configurations (other than English)
* They wish to support other lexeme or advanced functions.

#### Using Plain Free-Text Searches

Implementers can use plain free-text search parsing by altering the function `fti_tsquery` to use `plainto_tsquery` as:

```
CREATE OR REPLACE FUNCTION public.fti_tsquery(search_term_in text)
 RETURNS tsquery
 LANGUAGE plpgsql
 IMMUTABLE
AS $function$
BEGIN
	RETURN PLAINTO_TSQUERY('english', search_term_in);
END;
$function$
;

```

#### Using Full-Featured Searches / PostgreSQL 10

Implementers can allow users to access advanced features supported by the PostgreSQL freetext search engine. The method below illustrates taking a search term and splitting the term by spaces and appending each back to a query.&#x20;

```
CREATE OR REPLACE FUNCTION public.fti_tsquery(search_term_in text)
 RETURNS tsquery
 LANGUAGE plpgsql
 IMMUTABLE
AS $function$
BEGIN
	RETURN TO_TSQUERY('english', ARRAY_TO_STRING(STRING_TO_ARRAY(SEARCH_TERM_IN, ' '), ' & '));
END;
$function$
;

```

The method above would convert `John Smith Lincoln FR-403` to the TSQUERY expression: `John & Smith & Lincoln & FR-403` . This simple implementation permits search by prefix/wildcard: `Joh:* Sm:*` converted to `Joh:* & Sm:*`.&#x20;

Users can implement custom search term parsing/filtering based on their use case and context.

### Matching Job Notes

The SanteDB matching job has been updated to modify the behavior of the job based on the configuration of the environment it is running in. The table below provides a summary of this change:&#x20;

<table><thead><tr><th>OS</th><th width="182.377245508982">CPU</th><th>Matching / Strategy</th></tr></thead><tbody><tr><td>Windows</td><td>&#x3C; 4 Cores</td><td>Multi-Threaded Load (PLINQ)<br>Single Threaded Match</td></tr><tr><td></td><td>4+ Cores</td><td>Multi-Threaded Load (PLINQ)<br>Multi-Threaded Match</td></tr><tr><td>Docker / Mono</td><td>&#x3C; 4 Cores</td><td>Single-Threaded Load<br>Single Threaded Match</td></tr><tr><td></td><td>4+ Cores</td><td>Single-Threaded Load<br>Multi-Threaded Match</td></tr></tbody></table>

When running the background matching job in Docker , users may experience periods of time where the available threads in the thread pool are consumed by the worker tasks. This appears to be the Mono implementation of `ConcurrentQueue` and/or the method in which Mono allocates threads.&#x20;

Users may experiment with the `MONO_THREADS_PER_CPU` environment variable to tune the performance of their deployment.



