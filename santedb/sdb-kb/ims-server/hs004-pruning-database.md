# HS004 - Pruning and Cleaning the Database

**Purpose:** You wish to reduce the size of your OpenIZ instance by removing obsolete versions of data from the data store and/or increase performance of the database.

**Introduction:** OpenIZ's database provides a versioned history of all edits made to concepts, acts, and entities. While this function is useful for tracing the lifetime of an object, it can cause additional data usage on your server. It is a good practice to occasionally check on the database to ensure it is running at peak performance. This help and support article will show you how to use some basic commands to clean up and prune your OpenIZ database.

**Applies To:**

* OpenIZ Immunization Management Server \(running PostgreSQL database\)

**Steps:**

1. Connect to your PostgreSQL instance using **psql** or **PgAdmin**.
2. Get the time that tables were last vacuumed & analyzed

   ```text
   select relname, last_analyze, last_autovacuum, last_vacuum from pg_stat_all_tables
   ```

   * If you notice that last\_analyze has not occurred run the **ANALYZE** command 
   * If you notice that last\_vacuum has not occurred in a long time run **VACUUM FULL** command
   * If you notice that last\_autovacuum has not occurred in a long time, ensure that your configuration is correct and auto-vacuum is setup by running **SHOW ALL**

3. Get the size of the database per patient: 

   ```text
    select pg_size_pretty(pg_database_size(current_database()) / (select count(*) from pat_tbl));
   ```

   * If the database size seems large for your patient population \(about 50 kb per patient\) you may want to reduce size by squashing the database. \(**NOTE:** Only base your decision on the size reported after running **VACUUM FULL**\)
   * **SQUASHING:** - Just as in GIT the act of squashing the database results in removing all the version history for patients and acts such that only the current version is kept. To squash the database:
   * **!!WARNING!!**: Ensure that you take a backup of your database before squashing it.      

     ```text
      BEGIN TRANSACTION;
      SELECT squash_db();
      COMMIT;
     ```

     * The database server should report its progress:

       ```text
       INFO:    O O   \ /
       INFO:     X     X
       INFO:    / \   O O
       INFO:  PRUNING DATABASE STARTED - THIS WILL REMOVE ALL OBSOLETE DATA FROM DATABASE
       INFO:  DEPENDING ON THE SIZE OF YOUR DATASET THIS MAY TAKE UP TO 30 MINUTES
       INFO:  CURRENT DB SIZE: 5433 MB
       INFO:  PRUNING ADDRESSES
       INFO:  PRUNING NAMES
       ```

