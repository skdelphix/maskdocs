Before masking your data, it is important to prepare the database. This section
explains the required changes, reasons for the change, and instructions to make
the change.

## Logging Archive

**What is Durability Level?** 
Sybase has 3 Durability levels, Full, at_shutdown and no_recovery. Databases
with a durability set to no_recovery or at_shutdown—whether they are in-memory
or disk-resident—are referred to as low-durability databases. Data in low
durability databases survives after a commit (provided you do not restart the
server).

Use create database with durability=durability_level to set a database’s
durability level. Adaptive Server supports full, no_recovery, and at_shutdown
durability levels.

	
**Why is it important to make this change?** 

We recommend using the no_recovery to minimize log size and increase
performance. This should be combined with setting the sp_dboption to ‘trunc log
on chkpt’ to true and to set the sp_dboption to 'select into/bulkcopy/pllsort'
to true. It is also recommended at the table level to use DML_Logging set to
minimal to reduce logging DML statements, such as updates. This is best for
large tables.
