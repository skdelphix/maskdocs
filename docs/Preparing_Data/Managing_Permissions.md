# Database User Permissions for executing Masking and Profiling Jobs

## Introduction

This section provides the recommended list of permissions required for executing Masking and Profiling jobs on the Delphix Masking Engine. This page provides general permission recommendations. The subsequent pages in this section provide detailed recommendations for specific databases.

Recommend creating a separate Database user (i.e. named *Masking User*) to be created across all the databases with the appropriate permissions on the schemas to be masked. If needed create multiple users. The appropriate permissions for the database *Masking User* are listed below.

The benefits of having a separate DB *Masking User*:

 - Replicating the new user (and privileges) are easier
 - Access Audits are much easier
 - Can be created as central AD user and used at many places simultaneously

## List of Database Entitlements Required to Run Masking Jobs

 - Read data from Tables
 - Write data to Tables
 - Update data in tables
 - Create indexes
 - Drop indexes
 - Create triggers
 - Drop triggers
 - Disable triggers
 - Enable triggers
 - Alter tables add column
 - Alter table delete column
 - Create constraints
 - Delete constraints
 - Disable constraints
 - Enable constraints

## List of Database Entitlements Required to Run Profiling Jobs

 - View Definition (Schema)
 - Read Data from Tables
