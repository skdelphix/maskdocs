Before masking your data, it is important to prepare your database. This section
explains the required changes, reasons for the change, and the instructions to
make the change.

## Logging 

**What is Simple Recovery Model?**

SQL Database Simple Recovery model - Automatically reclaims log space to keep
space requirements small, essentially eliminating the need to manage the
transaction log space. Operations that require transaction log backups are not
supported by the simple recovery model. 

**Why is it important to make this change?**

Reducing the overhead of the transaction logging and the size of the files
before checkpoints increases the masking speed significantly.

**How exactly do I make this change?**

Using SQL Server Management Studio open the DB properties dialog box and select
the “simple recovery model” or from a SQL Query tool enter “SET RECOVERY SIMPLE.”
Please see _____ for more details. 


## DB/VDB Memory Allocation 

**What is min/max memory in SQL Server?**

Memory is allocated at the SQL Server level, so all the DBs will share the
entire load. Max memory should be close the maximum available on the server. 

**Why is it important to make this change?**

To assure that masking jobs will perform at an optimum level.  

**How exactly do I make this change?**

Use SQL Server Management Studio and change the max memory allocation for the
server.


## Primary/Foreign/DMS_ROW_ID Keys

**What is a key?**

A key is a unique, non-null value that identifies a row in the database.  

**Why is it important to make this change?**

Using a PK or Foreign key is critical for fast updates. When a table does not
have an identity column with an index or a PK/FK then the masking engine will
alter the table to have an Identity column, DMS_ROW_ID to optimize performance.

**How exactly do I make this change?**

A logical key can be added to a table in the Masking Engine Ruleset for each
table, if there is a specific column that would find the row to update faster
than the current PK/FK.
