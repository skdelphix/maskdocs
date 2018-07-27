Before masking your data, it is important to prepare the database. This section
explains the required changes, reasons for the change, and instructions to make
the change.

## Logging Archive

**What is Durability Level?** 
Sybase has 3 Durability levels, Full, at_shutdown and no_recovery. Databases
with a durability set to **no_recovery** or **at_shutdown**—whether they are in-memory
or disk-resident—are referred to as low-durability databases. Data in low
durability databases survives after a commit (provided you do not restart the
server).

Use **create database with durability=durability_level** to set a database’s
durability level. Adaptive Server supports **full**, **no_recovery**, and
**at_shutdown** durability levels.

	
**Why is it important to make this change?** 

We recommend using the no_recovery to minimize log size and increase
performance. This should be combined with setting the sp_dboption to ‘trunc log
on chkpt’ to true and to set the sp_dboption to 'select into/bulkcopy/pllsort'
to true. It is also recommended at the table level to use DML_Logging set to
minimal to reduce logging DML statements, such as updates. This is best for
large tables.

**How exactly do I make this change? (exact commands, etc).**

Use create database with **durability=durability_level** to set a database’s
durability level. Adaptive Server supports **full**, **no_recovery**, and
**at_shutdown** durability levels.


`create database database`

	`on data_device = 'size of device'`
	
	`log on log_device = 'size of device'`
	
	`with durability = no_recovery;`

`sp_dboption database, 'trunc log on chkpt', true;`

`sp_dboption database, 'select into/bulkcopy/pllsort', true;`

`ALTER TABLE tablename SET dml_logging = minimal;`

##  What is min/max memory in SQL Server? 

### Determining the Amount of Memory SAP ASE Needs

The total memory SAP ASE requires to start is the sum of all memory
configuration parameters plus the size of the procedure cache plus the size of
the buffer cache, where the size of the procedure cache and the size of the
buffer cache are expressed in round numbers rather than in percentages.
The procedure cache size and buffer cache size do not depend on the total
memory you configure. You can configure the procedure cache size and buffer
cache size independently. Use **sp_cacheconfig** to obtain information such as the
total size of each cache, the number of pools for each cache, the size of each
pool, and so on.

Use **sp_configure** to determine the total amount of memory SAP ASE is using at a
given moment:

`1> sp_configure "total logical memory"`

|**Parameter Name**|**Default**|**Memory Used**|**Config Value**|**Run Value**|**Unit**|**Type**|
|---|---|---|---|---|---|---|---|
|total logical memory|33792|127550|63775|63775|memory pages(2k)|read-only|

The value for the Memory Used column is represented in kilobytes, while the
value for the Config Value column is represented in 2K pages.

The Config Value column indicates the total logical memory SAP ASE uses while it
is running. The Run Value column shows the total logical memory being consumed
by the current SAP ASE configuration. Your output differs when you run this
command, because no two SAP ASEs are configured exactly the same.

### Determine the SAP ASE Memory Configuration

The total memory allocated during system start-up is the sum of memory required
for all the configuration needs of SAP ASE. You can obtain this value from the 
read-only configuration parameter **total logical memory**
.
This value is calculated by SAP ASE. The configuration parameter **max memory** must
be greater than or equal to **total logical memory**. **Max memory** indicates
the amount of memory you will allow for SAP ASE needs.

During server start-up, by default, SAP ASE allocates memory based on the value
of **total logical memory**. However, if the configuration parameter **allocate
max shared memory** has been set, then the memory allocated will be based on 
the value of **max memory**. The configuration parameter **allocate max shared 
memory** enables a system administrator to allocate the maximum memory that is
allowed to be used by SAP ASE, during server start-up.

The key points for memory configuration are:

 - The system administrator should determine the size of shared memory available
   to SAP ASE and set **max memory** to this value.

 - The configuration parameter **allocate max shared memory** can be turned on 
   during start-up and runtime to allocate all the shared memory up to **max
   memory** with the least number of shared memory segments. A large number of
   shared memory segments has the disadvantage of some performance degradation
   on certain platforms. Check your operating system documentation to determine
   the optimal number of shared memory segments. Once a shared memory segment is
   allocated, it cannot be released until the server is restarted.

 - The difference between **max memory** and **total logical** memory determines the
   amount of memory available for the procedure and statement caches, data
   caches, or other configuration parameters.

 - The amount of memory SAP ASE allocates during start-up is determined by
   either **total logical memory** or **max memory**. If you set **alloc max**
   **shared memory**  to 1, SAP ASE uses the value for **max memory**.

 - If either **total logical memory** or **max memory** is too high:
    - SAP ASE may not start if the physical resources on your machine are not
      sufficient.
    - If it does start, the operating system page fault rates may rise
      significantly and the operating system may need to be reconfigured to
      compensate.

**Why is it important to make this change?**

To assure that masking jobs will perform at an optimum level.  

## Primary/Foreign/DMS_ROW_ID keys to for masking Sybase:

**What is a key?**

A key is a unique, non-null value that identifies a row in the database.  

**Why is it important to make this change?** 

Using a PK or Foreign key is critical for fast updates. When a table does not
have an identity column with an index or a PK/FK then the masking engine will
alter the table to have an Identity column, DMS_ROW_ID to optimize performance.

**How exactly do I make this change? (exact commands, etc)**. 

A logical key can be added to a table in the Masking Engine Ruleset for each
table, if there is a specific column that would find the row to update faster
than the current PK/FK.

Note Sybase ASE will create unavoidable log entries when a table is altered 
and will increase the log size significantly. If needed, run the masking jobs
using the On-The-Fly method to avoid log file increases.

## Creating a Masking User and Privileges:

It is highly recommended to create a database user, and possibly a role, to
mask. This user should not be created in production but should be created in
non-Production. The following permissions are needed:

Syntax to add user and give privileges:

`sp_adduser mask_user;` 

`CREATE user NEWUSER;`

`CREATE LOGIN mask_user WITH PASSWORD Delphix_123; --THIS MUST BE DONE IN MASTER`

`CREATE USER mask_user IDENTIFIED BY Delphix_123;`

`GRANT SELECT ON PII_V2 TO mask_user;`
`GRANT INSERT ON PII_V2 TO mask_user;`
`GRANT DELETE ON PII_V2 TO mask_user;`
`GRANT ALTER ON PII_V2 TO mask_user;`
`GRANT UPDATE ON PII_V2 TO mask_user;`

`GRANT ALTER ANY TABLE TO mask_user;`

Adaptive Server requires a two-step process to add a user: sp_addlogin followed
by sp_adduser.

----------------------------------------------------------

`CREATE LOGIN MASK_SUPER_USER WITH PASSWORD Delphix_123;`

`sp_addlogin MASK_SUPER_USER, Delphix_123;`

`GRANT ROLE sa_role TO MASK_SUPER_USER;`


