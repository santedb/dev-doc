# Deleted Records

SanteDB **never** deletes records from its underlying database. It always adds or updates flags to indicate records are deleted. There are several states of "deleted" in the SanteDB service:

1. **Obsolete -** Indicates that the record did exist, the object had a useful purpose for a period of time which has passed.
2. **Nullified -** Indicates that the record was created in error and should not be considered historical.

When you delete a record in any SanteDB administrative screen, it is placed in the **Obsoleted** state. You can show obsoleted records by selecting **Show Deleted** option. Here you can un-delete a record, which essentially removes the obsoleted flag from the record.

