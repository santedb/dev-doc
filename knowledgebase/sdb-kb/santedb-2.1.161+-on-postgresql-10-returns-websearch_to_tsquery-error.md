# SanteDB 2.1.161+ on PostgreSQL 10 returns "websearch\_to\_tsquery" error

**Issue:** After installing an upgrade for a SanteDB iCDR server to 2.1.161, the service starts however, when attempting to perform a freetext search (with `_any`) the user receives an error that `websearch_to_tsquery` is not a function.

**Applies To:**

* SanteDB iCDR (Version 2.1.161+) on PostgreSQL 10

**Symptoms:**

* When performing a query that uses `_any` the iCDR returns an error that `websearch_to_tsquery` is not available&#x20;

**Solutions:**

1. Open a SQL command prompt to your PostgreSQL 10 server
2. Re-create the `fti_tsquery` stored procedure to use a different algorithm:

```sql
CREATE OR REPLACE FUNCTION websearch_to_tsquery (term_in IN TEXT) 
RETURNS tsquery 
IMMUTABLE 	 AS
$$
BEGIN
	RETURN TO_TSQUERY(ARRAY_TO_STRING(STRING_TO_ARRAY(TERM_IN, ' '), ' & '));
END;q
$$ LANGUAGE plpgsql;
```



