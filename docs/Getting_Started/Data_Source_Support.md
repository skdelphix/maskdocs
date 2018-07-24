# Masking Data Source Support

The Delphix Masking service supports profiling, masking, and tokenizing
a variety of different data sources including distributed databases,
mainframe, PaaS databases, and files. At a high level, Delphix Masking
breaks up support for data sources into two categories:

  - **Dedicated Delphix Connectors:** These are data sources that the
    Delphix Engine can connect directly using built-in connectors
    that have been optimized to perform masking, profiling and
    tokenization.

  - **FEML Sources:** FEML (File Extract Mask and Load) is a method
    used to mask, and tokenize data sources that do not have dedicated
    Delphix Connectors. FEML uses existing APIs from data sources to
    extract the data to a file, masks the file, and then uses APIs to
    load the masked file back into the database.

## Dedicated Delphix Connectors

The Delphix Engine has dedicated masking connectors for the following
data sources:

  - **Distributed Database:** DB2 LUW, Oracle, MS SQL, MySQL, SAP ASE
    (Sybase), PostgreSQL, MariaDB

  - **Mainframe:** DB2 Z/OS, DB2 iSeries, VSAM

  - **PaaS Database:** AWS RDS Oracle

  - **Files:** Excel, Fixed Width, Delimited, XML

For a detailed view of all the versions, features, etc Delphix supports
on each data source - see the sections below. For a higher level matrix
please see our [<span class="underline">Data Source support
matrices</span>](https://docs.delphix.com/display/DOCS525/Support+Matrices).

### DB2 LUW Connector

#### Introduction

DB2 for Linux, UNIX and Windows is a database server product developed
by IBM. Sometimes

called DB2 LUW for brevity, it is part of the DB2 family of database
products. DB2 LUW is the

"Common Server" product member of the DB2 family, designed to run on
most popular

operating systems. By contrast, all other DB2 products are specific to a
single platform.

#### Support Matrix

The Delphix DB2 LUW connector supports the following versions of DB2
LUW:

| **Version** | **Linux** | **Unix**  | **Windows** |
| ----------- | --------- | --------- | ----------- |
| **9.1**     | Supported | Supported | Supported   |
| **9.5**     | Supported | Supported | Supported   |
| **9.7**     | Supported | Supported | Supported   |
| **9.8**     | Supported | Supported | Supported   |
| **10.1**    | Supported | Supported | Supported   |
| **10.5**    | Supported | Supported | Supported   |
| **11.1**    | Supported | Supported | Supported   |

#### Available Features

The DB2 LUW connector supports profiling and masking/tokenization features. Below is a list of which options are & are not available for jobs using the DB2 LUW connector:

|                             | **Feature**             | **Availability** |
| -------------------------   | ---------------------   | ---------------- |
| **In-Place Masking Mode**   | Multi-Tenant            | Available        |
|                             | Streams / Threads       | Available        |
|                             | Bulk Update             | Available        | 
|                             | Batch Update            | Available        | 
|                             | Drop Indexes            | Available        |
|                             | Disable Trigger         | Unavailable      | 
|                             | Disable Constraint      | Unavailable      |
|                             | Identity Column Support | Unavailable      |
| **On-The-Fly Masking Mode** | Restart Ability         | Available        |
|                             | Truncate                | Available        |
|                             | Disable Trigger         | Unavailable      |
|                             | Disable Constraint      | Unavailable      |
|                             | Create Target           | Available        |
| **Profiling**               | Multi-Tenant            | Available        |
|                             | Streams                 | Available        |

### Oracle Connector

#### Introduction

Oracle Database (commonly referred to as Oracle RDBMS or simply as
Oracle) is a multi-model database management system produced and
marketed by Oracle Corporation.

#### Support Matrix

| **Version** | **Linux**     | **Unix**      | **Windows**   |
| ----------- | ------------- | ------------- | ------------- |
| **10g**     | Supported     | Supported     | Supported     |
| **11gR1**   | Supported     | Supported     | Supported     |
| **11gR2**   | Supported     | Supported     | Supported     |
| **12c**     | Supported     | Supported     | Supported     |
| **12cR2**   | Not Supported | Not Supported | Not Supported |

#### Available Features

The Oracle connector supports profiling and masking/tokenization features. Below is a list of which options are and are not available for jobs using the Oracle connector:

|                             | **Feature**             | **Availability** |
| -------------------------   | ---------------------   | ---------------- |
| **In-Place Masking Mode**   | Multi-Tenant            | Available        |
|                             | Streams / Threads       | Available        |
|                             | Bulk Update             | Available        | 
|                             | Batch Update            | Available        | 
|                             | Drop Indexes            | Available        |
|                             | Disable Trigger         | Available        | 
|                             | Disable Constraint      | Available        |
|                             | Identity Column Support | Available        |
| **On-The-Fly Masking Mode** | Restart Ability         | Available        |
|                             | Truncate                | Available        |
|                             | Disable Trigger         | Available        |
|                             | Disable Constraint      | Available        |
|                             | Create Target           | Available        |
| **Profiling**               | Multi-Tenant            | Available        |
|                             | Streams                 | Available        |

### MS SQL Connector

#### Introduction

Microsoft SQL Server is a relational database management system
developed by Microsoft. As a database server, it is a software product
with the primary function of storing and retrieving data as requested by
other software applications—which may run either on the same computer or
on another computer across a network (including the Internet).

#### Support Matrix

| **Version** | **Linux** | **Unix** | **Windows** |
| ----------- | --------- | -------- | ----------- |
| **2005**    | N/A       | N/A      | Supported   |
| **2008**    | N/A       | N/A      | Supported   |
| **2008 R2** | N/A       | N/A      | Supported   |
| **2012**    | N/A       | N/A      | Supported   |
| **2014**    | N/A       | N/A      | Supported   |
| **2016**    | Supported | N/A      | Supported   |

#### Available Features

The MS SQL connector supports profiling and masking/tokenization features. Below is a list of which options are and are not available for jobs using the MS SQL connector.

|                             | **Feature**             | **Availability** |
| -------------------------   | ---------------------   | ---------------- |
| **In-Place Masking Mode**   | Multi-Tenant            | Available        |
|                             | Streams / Threads       | Available        |
|                             | Bulk Update             | Available        | 
|                             | Batch Update            | Available        | 
|                             | Drop Indexes            | Available        |
|                             | Disable Trigger         | Available        | 
|                             | Disable Constraint      | Available        |
|                             | Identity Column Support | Available        |
| **On-The-Fly Masking Mode** | Restart Ability         | Available        |
|                             | Truncate                | Available        |
|                             | Disable Trigger         | Available        |
|                             | Disable Constraint      | Available        |
|                             | Create Target           | Available        |
| **Profiling**               | Multi-Tenant            | Available        |
|                             | Streams                 | Available        |

### PostgreSQL Connector

#### Introduction

PostgreSQL, often simply Postgres, is an object-relational database management system (ORDBMS) with an emphasis on extensibility and standards compliance. PostgreSQL is developed by the PostgreSQL Global Development Group, a diverse group of many companies and individual contributors.[15] It is free and open-source, released under the terms of the PostgreSQL License, a permissive software license.

#### Support Matrix

| **Version** | **Linux** | **Unix** | **Windows** |
| ----------- | --------- | -------- | ----------- |
| **9.2**     | Supported | Supported| Supported   |
| **9.3**     | Supported | Supported| Supported   |
| **9.4**     | Supported | Supported| Supported   |
| **9.5**     | Supported | Supported| Supported   |

#### Available Features

The PostgreSQL connector supports profiling and masking/tokenization features. Below is a list of which options are & are not available for jobs using the PostgreSQL connector:

|                             | **Feature**             | **Availability**
| -------------------------   | ---------------------   | ---------------- |
| **In-Place Masking Mode**   | Multi-Tenant            | Available        |
|                             | Streams / Threads       | Available        |
|                             | Bulk Update             | Available        | 
|                             | Batch Update            | Available        | 
|                             | Drop Indexes            | Unavailable      |
|                             | Disable Trigger         | Unavailable      | 
|                             | Disable Constraint      | Unavailable      |
|                             | Identity Column Support | Available        |
| **On-The-Fly Masking Mode** | Restart Ability         | Unavailable      |
|                             | Truncate                | Available        |
|                             | Disable Trigger         | Available        |
|                             | Disable Constraint      | Available        |
|                             | Create Target           | Available        |
| **Profiling**               | Multi-Tenant            | Available        |
|                             | Streams                 | Unavailable      |

### MySQL Connector

#### Introduction

MySQL is an open-source relational database management system (RDBMS).
MySQL was owned and sponsored by a single for-profit firm, the Swedish
company MySQL AB. MySQL is now owned by Oracle Corporation.

#### Support Matrix

| **Version** | **Linux** | **Unix**  | **Windows** |
| ----------- | --------- | --------- | ----------- |
| **5.5**     | Supported | Supported | Supported   |
| **5.6**     | Supported | Supported | Supported   |
| **5.7**     | Supported | Supported | Supported   |

#### Available Features

The MySQL connector supports profiling and masking/tokenization features. Belwo is a list of which options are and are not available for jobs using the MySQL connector:

|                             | **Feature**             | **Availability** |
| -------------------------   | ---------------------   | ---------------- |
| **In-Place Masking Mode**   | Multi-Tenant            | Available        |
|                             | Streams / Threads       | Available        |
|                             | Bulk Update             | Available        | 
|                             | Batch Update            | Available        | 
|                             | Drop Indexes            | Available        |
|                             | Disable Trigger         | Unavailable      | 
|                             | Disable Constraint      | Unavailable      |
|                             | Identity Column Support | Available        |
| **On-The-Fly Masking Mode** | Restart Ability         | Unavailable      |
|                             | Truncate                | Available        |
|                             | Disable Trigger         | Unavailable      |
|                             | Disable Constraint      | Unavailable      |
|                             | Create Target           | Available        |
| **Profiling**               | Multi-Tenant            | Available        |
|                             | Streams                 | Available        |

### SAP ASE (Sybase) Connector

#### Introduction

SAP ASE (Adaptive Server Enterprise), originally known as Sybase SQL
Server, and also commonly known as Sybase DB or Sybase ASE, is a
relational model database server product for businesses developed by
Sybase Corporation which became part of SAP AG.

#### Support Matrix

| **Version** | **Linux** | **Unix**  | **Windows** |
| ----------- | --------- | --------- | ----------- |
| **12.5**    | Supported | Supported | Supported   |
| **15.03**   | Supported | Supported | Supported   |
| **15.5**    | Supported | Supported | Supported   |
| **15.7**    | Supported | Supported | Supported   |
| **16**      | Supported | Supported | Supported   |

#### Available Features

The SAP ASE (Sybase) connector supports profiling and masking/tokeniztion features. Below is a list of which options are and are not available for jobs using the SAP ASE connector:

|                             | **Feature**             | **Availability** |
| -------------------------   | ---------------------   | ---------------- |
| **In-Place Masking Mode**   | Multi-Tenant            | Available        |
|                             | Streams / Threads       | Available        |
|                             | Bulk Update             | Available        | 
|                             | Batch Update            | Available        | 
|                             | Drop Indexes            | Available        |
|                             | Disable Trigger         | Available        | 
|                             | Disable Constraint      | Available        |
|                             | Identity Column Support | Available        |
| **On-The-Fly Masking Mode** | Restart Ability         | Available        |
|                             | Truncate                | Available        |
|                             | Disable Trigger         | Available        |
|                             | Disable Constraint      | Available        |
|                             | Create Target           | Available        |
| **Profiling**               | Multi-Tenant            | Available        |
|                             | Streams                 | Available        |

### MariaDB Connector

#### Introduction

MariaDB is a community-developed fork of the MySQL relational database
management system intended to remain free under the GNU GPL. Development
is led by some of the original developers of MySQL, who forked it due to
concerns over its acquisition by Oracle Corporation.

#### Support Matrix

| **Version** | **Linux** | **Unix**  | **Windows** |
| ----------- | --------- | --------- | ----------- |
| **10**      | Supported | Supported | Supported   |

#### Available Features

ADD SECTION FOR SETUP / SPECIAL CONSIDERATIONS WHEN MASKING ORACLE.

### DB2 Z/OS and iSeries Connectors

#### Introduction

DB2 for z/OS and iSeries are relational database management systems that run on IBM Z(mainframe) and IBM Power Systems.

#### Support Matrix

| **Version** | **z/OS**  | **i-Series** |
| ----------- | --------- | ------------ |
| **7.1**     | N/A       | Supported    |
| **7.2**     | N/A       | Supported    |
| **7.3**     | N/A       | Supported    |
| **9**       | Supported | N/A          |
| **10**      | Supported | N/A          |
| **11**      | Supported | N/A          |
| **VSAM**    | Supported | N/A          |

#### Available Features

The DB2 for z/OS and iSeries connectors support profilinng and masking/tokenization features. Below is a list of which options are and are not available for jobs using the DB2 and z/OS and iSeries connectors:

|                             | **Feature**             | **Availability** |
| -------------------------   | ---------------------   | ---------------- |
| **In-Place Masking Mode**   | Multi-Tenant            | Available        |
|                             | Streams / Threads       | Available        |
|                             | Bulk Update             | Available        | 
|                             | Batch Update            | Available        | 
|                             | Drop Indexes            | Unavailable      |
|                             | Disable Trigger         | Unavailable      | 
|                             | Disable Constraint      | Unavailable      |
|                             | Identity Column Support | Unavailable      |
| **On-The-Fly Masking Mode** | Restart Ability         | Unavailable      |
|                             | Truncate                | Available        |
|                             | Disable Trigger         | Unavailable      |
|                             | Disable Constraint      | Unavailable      |
|                             | Create Target           | Unavailable      |
| **Profiling**               | Multi-Tenant            | Available        |
|                             | Streams                 | Available        |

### AWS RDS Oracle Connector

#### Introduction

Oracle Database is a relational database management system developed by
Oracle. Amazon RDS makes it easy to set up, operate, and scale Oracle
Database deployments in the cloud. With Amazon RDS, you can deploy
multiple editions of Oracle Database in minutes with cost-efficient and
re-sizable hardware capacity.

#### Support Matrix

| **Version** | **Support Level** |
| ----------- | ----------------- |
| **11.2.04** | Supported         |

#### Available Features
The AWS RDS connector supports profilinng and masking/tokenization features. Below is a list of which options are and are not available for jobs using the AWS RDS connector:

|                             | **Feature**             | **Availability** |
| -------------------------   | ---------------------   | ---------------- |
| **In-Place Masking Mode**   | Multi-Tenant            | Available        |
|                             | Streams / Threads       | Available        |
|                             | Bulk Update             | Available        | 
|                             | Batch Update            | Available        | 
|                             | Drop Indexes            | Available        |
|                             | Disable Trigger         | Available        | 
|                             | Disable Constraint      | Available        |
| **On-The-Fly Masking Mode** | Restart Ability         | Available        |
|                             | Truncate                | Available        |
|                             | Disable Trigger         | Available        |
|                             | Disable Constraint      | Available        |
| **Profiling**               | Multi-Tenant            | Available        |
|                             | Streams                 | Available        |

### Files Connector

#### Introduction

Much of the time data will live outside of databases. The data can be stored in a variety of different formats including Fixed Width, Delimited, etc.

#### Support Matrix

| **File Type/Format**     | **Support Level** |
| ------------------------ | ----------------- |
| **Excel (.xls & .xlsx)** | Supported         |
| **Fixed Width**          | Supported         |
| **Delimited**            | Supported         |
| **XML**                  | Supported         |
| **JSON**                 | Not Supported     |

#### Available Features

ADD SECTION FOR SETUP / SPECIAL CONSIDERATIONS WHEN MASKING ORACLE.

## FEML Sources 

### High Level Process

For more information on how Delphix can help you mask data sources we do
not have dedicated connector for - please
[<span class="underline">contact
us</span>](https://www.delphix.com/company/contact).
