# Preparing Oracle Database for Profiling/Masking

Before masking your data, it is important to prepare your database. This 
section explains the required changes, reasons for the changes, and instructions
on how to make the changes.

## Archive Logging 

**What is Archive Logging?** 

Oracle Database lets you save filled groups of redo log files to one or more
offline destinations, known collectively as the archived redo log, or more
simply the archive log. The process of turning redo log files into archived redo
log files is called archiving. This process is only possible if the database is
running in ARCHIVELOG mode. You can choose automatic or manual archiving.

**Why is it important to make this change?** 

Archive logging will slow down masking processes and absorb CPU resources that
could be used by the masking process.  Furthermore, since masking will change
every row in every table being masked logs are only needed for short term
recovery and transaction backout.  

The choice of whether to enable the archiving of filled groups of redo log files
depends on the availability and reliability requirements of the application
running on the database. If you cannot afford to lose any data in your database
in the event of a disk failure, use ARCHIVELOG mode. The archiving of filled
redo log files can require you to perform extra administrative operations.

**How exactly do I make this change? (exact commands, etc).** 

`ALTER DATABASE NOARCHIVELOG;`

## DB/VDB Memory Allocation

**What is SGA?** 
A system global area (SGA) is a group of shared memory structures that contain
data and control information for one Oracle database instance. If multiple users
are concurrently connected to the same instance, then the data in the instance's
SGA is shared among the users. Consequently, the SGA is sometimes called the
shared global area.

An SGA and Oracle processes constitute an Oracle instance. Oracle automatically
allocates memory for an SGA when you start an instance, and the operating system
reclaims the memory when you shut down the instance. Each instance has its own
SGA.

The SGA is read/write. All users connected to a multiple-process database
instance can read information contained within the instance's SGA, and severa
l processes write to the SGA during execution of Oracle.
When automatic SGA memory management is enabled, the sizes of the different SGA
components are flexible and can adapt to the needs of a workload without
requiring any additional configuration. The database automatically distributes
the available memory among the various components as required, allowing the
system to maximize the use of all available SGA memory. Make sure the DB/VDB
memory allocation is sufficient for the workload. Delphix’s best practices for
sizing a VDB will handle most masking requirements.  If you plan to run many
concurrent masking jobs a small memory allocation will negatively impact
performance of the masking jobs.  

**Why is it important to make this change?**

To assure that masking jobs will perform at an optimum level.  

**How exactly do I make this change? (exact commands, etc).** 
Set automatic SGA memory management to enabled. If not allowed set the SGA based
on the diagnosis from the AWR report generated during a masking job. The DBA is 
best suited to make the appropriate tuning changes to the SGA parameters for the
version of oracle being masked.

## Undo Tablespace Size And Undo Retention Time:

**What is tablespace?** 
Every Oracle Database must have a method of maintaining information that is used
to roll back, or undo, changes to the database. Such information consists of 
records of the actions of transactions, primarily before they are committed. 
These records are collectively referred to as undo.

Undo records are used to:
 - Roll back transactions when a ROLLBACK statement is issued
 - Recover the database
 - Provide read consistency
 - Analyze data as of an earlier point in time by using Oracle Flashback Query
 - Recover from logical corruptions using Oracle Flashback features

When a ROLLBACK statement is issued, undo records are used to undo changes that
were made to the database by the uncommitted transaction. During database
recovery, undo records are used to undo any uncommitted changes applied from the
redo log to the datafiles. Undo records provide read consistency by maintaining
the before image of the data for users who are accessing the data at the same
time that another user is changing it.

**Why is it important to make this change?** 

The masking Engine updates or inserts masked data in batches. In the case of an
insert it only requires the current transaction size for the commit of each table
being masked. The default per table stream is 10k rows. However, with an update
the transaction is not complete until the entire table is masked. So, the more
tables and more rows and the wider (size) each row is in each table, the more
undo space is needed to complete the transaction. Large tables, such as DW
tables or history and Audit tables, most often need an increase to the Undo
space and undo Retention time for updates. If the space or time is exceeded then
the masking job may fail with an ORA-01555, Snapshot too old error.

**How exactly do I make this change? (exact commands, etc).** 

It is highly recommended to increase the Undo space and undo Retention time when
running in-place jobs on large tables. A general rule of thumb is 2 or 3 times
the size of the larges table(s), or if there are multiple tables running at the
same time, then all tables combined. A DBA is best suited to make the necessary
UDNO Space and the UNDO Retention changes.

## Redo Logs Are Optimally Sized 

**What is Redo Logs?** 

The most crucial structure for recovery operations is the redo log, which
consists of two or more preallocated files that store all changes made to the
database as they occur. Every instance of an Oracle Database has an associated
redo log to protect the database in case of an instance failure.

**Why is it important to make this change?** 

The most important reason to make this change is to keep performance optimal.
If redo logs are too small, then the log switching will occur too often, using
up valuable Oracle resource.

**How exactly do I make this change? (exact commands, etc).** 

A DBA is best suited to make these changes appropriately.

## Change PCTFREE to 40-50:

**What is PCTFREE?** 

PCTFREE and PCTUSED are used together, but PCTFREE is critical for updates.
The larger the PCTFREE value the more updates can be done.

**Why is it important to make this change?** 

PCTFREE aids in performance increases for updating Oracle during masking. The
Masking Engine does many updates at the same time in batch mode. The more that 
can be done without DB overhead the faster the masking jobs run.

**How exactly do I make this change? (exact commands, etc).**

A DBA is best suited to make these changes.

## Change Primary Key To ROWID:

**What is ROWID?** 

For each row in the database, the ROWID pseudocolumn returns the address of the
row. Oracle Database rowid values contain information necessary to locate a row.

**Why is it important to make this change?**

This is especially important in masking for performance. IF ROWID is used then
Oracle will manage the updates for the rows it tracks using ROWID. This makes
updates much faster. On occasion there may be a key (PK/FK/UK) or ID column with
an index that is faster, but generally ROWID is the fastest.

**How exactly do I make this change? (exact commands, etc).**

Add ROWID as the logical key on each table in the ruleset using the Masking
Engine GUI. Also, in a script you should drop foreign keys, and if possible
indices and disable triggers and recreate them after the masking job has been
run for any of these types of columns being masked. 


