# Queenston Releases (2.1.150 - 2.1.180)

## Version 2.1.170

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

| OS            | CPU       | Matching / Strategy                                         |
| ------------- | --------- | ----------------------------------------------------------- |
| Windows       | < 4 Cores | <p>Multi-Threaded Load (PLINQ)<br>Single Threaded Match</p> |
|               | 4+ Cores  | <p>Multi-Threaded Load (PLINQ)<br>Multi-Threaded Match</p>  |
| Docker / Mono | < 4 Cores | <p>Single-Threaded Load<br>Single Threaded Match</p>        |
|               | 4+ Cores  | <p>Single-Threaded Load<br>Multi-Threaded Match</p>         |

When running the background matching job in Docker , users may experience periods of time where the available threads in the thread pool are consumed by the worker tasks. This appears to be the Mono implementation of `ConcurrentQueue` and/or the method in which Mono allocates threads.&#x20;

Users may experiment with the `MONO_THREADS_PER_CPU` environment variable to tune the performance of their deployment.

## Version 2.1.170.1

This version is a patch for the 2.1.170 release. It fixes the following issues found in 2.1.170:

* Fixes logic for timer jobs based on calendar to reduce the "greedyness" of the jobs
* Fixes display caching issue (was an issue with the BulkPurge function) so new data is properly rendered.
* Fixes some threading issues with the .NET ThreadPool on background matching

