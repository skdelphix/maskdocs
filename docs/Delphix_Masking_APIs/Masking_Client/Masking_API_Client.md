# Masking API Client

This section describes the API client available on the masking engine.

## Introduction

With the release of API v5 on the Masking Engine, Delphix has opened up
the possibility of scripting and automation against the Masking Engine.
While this is exciting for us internally at Delphix, we are sure that
this will be even more exciting for the consumers of the Masking Engine.
This document is intended to be a high-level overview of what to expect
with API v5 as well as some helpful links to get you started.

### REST

API v5 is a RESTful API. REST stands for REpresentational State
Transfer. A REST API will allow you to access and manipulate a textual
representation of objects and resources using a predefined set of
operations to accomplish various tasks.

### JSON

API v5 uses JSON (JavaScript Object Notation) to ingest and return
representations of the various objects used throughout various
operations. JSON is a standard format and, as such, has many tools
available to help with creating and parsing the request and response
payloads, respectively.

Here are some UNIX tools that can be used to parse JSON -
[<span class="underline">https://stackoverflow.com/questions/1955505/parsing-json-with-unix-tools</span>](https://stackoverflow.com/questions/1955505/parsing-json-with-unix-tools).
That being said, this is only the tip of the iceberg when it comes to
JSON parsing and the reader is encouraged to use their method of choice.

### API Client

The various operations and objects used to interact with API v5 are
defined in a specification document. This allows us to utilize various
tooling to ingest that specification to generate documentation and an
API Client, which can be used to generate cURL commands for all
operations.

To access the API client on your Masking Engine, go to
[<span class="underline">http://myMaskingEngine.myDomain.com/masking/api-client</span>](http://mymaskingengine.mydomain.com/masking/api-client).

To see how to log into the API client and for some starter recipes,
please check out API Cookbook document. Happy programming\!

### Supported Features

API v5 is in active development but does not currently support all
features that are accessible in the GUI. The list of supported features
will expand over the course of subsequent releases.

For a full list of supported APIs, the best place to look is the API
client on your Masking Engine

[<span class="underline">http://myMaskingEngine.com/masking/api-client.</span>](http://mymaskingengine.com/masking/api-client.)High-level
operations that are **not currently supported** via the v5 APIs include,
but are not limited to:

  - Job Scheduler

  - Audit and application logs

  - Copybook formats

  - Tokenization jobs

  - Reidentification jobs

## API Calls for Masking Administration

The Delphix Masking Engine supports the following two types of
administrative APIs:

  - Analytics APIs

    - These APIs are for including Masking performance information in the
    support bundle and do not need to be used unless that information is
    requested.

  - Application Setting APIs

    - Application Setting APIs allow an administrator to change the
    Delphix Masking Engine settings. Presently there are five categories
    of settings: analytics settings, LDAP settings, general settings,
    mask settings and profile settings. Over time, more settings will be
    added to give users direct control over the product's various
    settings. Below are the details of currently supported settings.

### Application Settings APIs

#### General Group Settings

<table>
<tbody>
<tr class="odd">
<td>
<strong>Setting Group</strong>
</td>
<td>
<strong>Setting Name</strong>
</td>
<td>
<strong>Type</strong>
</td>
<td>
<strong>Description</strong>
</td>
<td>
<strong>Default Value</strong>
</td>
</tr>
<tr class="even">
<td>
general
</td>
<td>
EnableMonitorRowCount
</td>
<td>
Boolean
</td>
<td>
Controls whether a job displays the total number of rows that are being masked.
Setting this to false reduces the startup time of all jobs.
</td>
<td>
true
</td>
</tr>
<tr class="odd">
<td></td>
<td>
PasswordTimeSpan
</td>
<td>
Integer
[0, ∞)
</td>
<td>
The number of hours a user is locked out for before they can attempt to log in again.
</td>
<td>
23
</td>
</tr>
<tr class="even">
<td></td>
<td>
PasswordCount
</td>
<td>
Integer
[0, ∞)
</td>
<td>
The number of incorrect password attempts before a user is locked out.
</td>
<td>
3
</td>
</tr>
<tr class="odd">
<td></td>
<td>
AllowPasswordResetRequest
</td>
<td>
Boolean
</td>
<td>
When true, users can request a password reset link be sent to the email associated with their account.
</td>
<td>
true
</td>
</tr>
<tr class="even">
<td></td>
<td>
PasswordResetLinkDuration
</td>
<td>
Integer
[1, ∞)
</td>
<td>
Controls how many minutes the password reset link is valid for.
</td>
<td>
5
</td>
</tr>
</tbody>
</table>

#### Algorithm Group Settings

<table>
<tbody>
<tr class="odd">
<td><strong>Setting Group</strong></td>
<td><strong>Setting Name</strong></td>
<td><strong>Type</strong></td>
<td><strong>Description</strong></td>
<td><strong>Default Value</strong></td>
</tr>
<tr class="even">
<td>algorithm</td>
<td>DefaultNonConformantDataHandling</td>
<td>String
{DONT_MASK, FAIL}</td>
<td>Default algorithm behavior for Handling of NonConformant Data patterns.</td>
<td>DONT_MASK</td>
</tr>
</tbody>
</table>

#### LDAP Group Settings

<table>
<tbody>
<tr class="odd">
<td><strong>Setting Group</strong></td>
<td><strong>Setting Name</strong></td>
<td><strong>Type</strong></td>
<td><strong>Description</strong></td>
<td><strong>Default Value</strong></td>
</tr>
<tr class="even">
<td>ldap</td>
<td>Enable</td>
<td>Boolean</td>
<td>Used to enable and disable LDAP authentication</td>
<td>false</td>
</tr>
<tr class="odd">
<td></td>
<td>LdapHost</td>
<td>String</td>
<td>Host of LDAP server</td>
<td>10.10.10.31</td>
</tr>
<tr class="even">
<td></td>
<td>LdapPort</td>
<td>Integer
[0, ∞)</td>
<td>Port of LDAP server</td>
<td>389</td>
</tr>
<tr class="odd">
<td></td>
<td>LdapBasedn</td>
<td>String</td>
<td>Base DN of LDAP server</td>
<td>DC=tbspune,DC=com</td>
</tr>
<tr class="even">
<td></td>
<td>LdapFilter</td>
<td>String</td>
<td>Filter for LDAP authentication</td>
<td>(&amp;(objectClass=person)(sAMAccountName=?))</td>
</tr>
<tr class="odd">
<td></td>
<td>MsadDomain</td>
<td>String</td>
<td>MSAD Domain for LDAP authentication</td>
<td>AD</td>
</tr>
<tr class="odd">
<td></td>
<td>LdapTlsEnable</td>
<td>Boolean</td>
<td>Enable and disable the use of TLS for LDAP connections.</td>
<td>false</td>
</tr>
</tbody>
</table>

!!! warning
    In the LDAP group, once the "Enable" setting is set to "true", all users logging in will be authenticated via the LDAP server. Local authentication will no longer work. Before setting this to true set all other LDAP settings correctly and create the necessary LDAP users on the masking engine.

#### Mask Group Settings

<table>
<tbody>
<tr class="odd">
<td>
<strong>Setting Group</strong>
</td>
<td>
<strong>Setting Name</strong>
</td>
<td>
<strong>Type</strong>
</td>
<td>
<strong>Description</strong>
</td>
<td>
<strong>Default Value</strong>
</td>
</tr>
<tr class="even">
<td>
mask
</td>
<td>
DatabaseCommitSize
</td>
<td>
Integer
[1, ∞)
</td>
<td>
Controls how many rows are updated (Batch Update) or inserted (Bulk Data) to the database before the transaction is committed.
</td>
<td>
10000
</td>
</tr>
<tr class="odd">
<td></td>
<td>
BulkDataSeparator
</td>
<td>
String
</td>
<td>
Characters used to separate fields in a bulk data masking job.
</td>
<td>
#;#
</td>
</tr>
<tr class="even">
<td></td>
<td>
DefaultStreams
</td>
<td>
Integer
[1, ∞)
</td>
<td>
Default number of streams for a masking job.
</td>
<td>
1
</td>
</tr>
<tr class="odd">
<td></td>
<td>
DefaultUpdateThreads
</td>
<td>
Integer
[1, ∞)
</td>
<td>
Default number of database update threads for a masking job.
</td>
<td>
1
</td>
</tr>
<tr class="even">
<td></td>
<td>
DefaultMaxMemory
</td>
<td>
Integer
[1024, ∞)
</td>
<td>
Default maximum memory for masking jobs (in megabytes).
</td>
<td>
1024
</td>
</tr>
<tr class="odd">
<td></td>
<td>
DefaultMinMemory
</td>
<td>
Integer
[1024, ∞)
</td>
<td>
Default minimum memory for masking jobs (in megabytes).
</td>
<td>
1024
</td>
</tr>
</tbody>
</table>

#### Profile Group Settings

<table>
<tbody>
<tr class="odd">
<td><strong>Setting Group</strong></td>
<td><strong>Setting Name</strong></td>
<td><strong>Type</strong></td>
<td><strong>Description</strong></td>
<td><strong>Default Value</strong></td>
</tr>
<tr class="even">
<td>profile</td>
<td>EnableDataLevelCount</td>
<td>Boolean</td>
<td>When enabled, only profile the number of rows specified by DataLevelRows when running data level profiling jobs.<br /><br />
When disabled, profile all rows when running data level profiling jobs.</td>
<td>false</td>
</tr>
<tr class="odd">
<td></td>
<td>DataLevelRows</td>
<td>Integer
[1, ∞)</td>
<td>The number of rows a data level profiling job samples when profiling a column. This is only used when EnableDataLevelCount is true.</td>
<td>100</td>
</tr>
<tr class="even">
<td></td>
<td>DataLevelPercentage</td>
<td>Double
(0, ∞)</td>
<td>Percentage of rows that must match the data level regex to consider this column a match, and thus sensitive.</td>
<td>80.0</td>
</tr>
<tr class="odd">
<td></td>
<td>IgnoreDatatype</td>
<td>String</td>
<td>Datatypes that a profiling job should ignore. Columns of these types will not be assigned a domain/algorithm pair.</td>
<td>BIT,BOOLEAN,CHAR#1,VARCHAR#1,VARCHAR2#1,NCHAR#1,<br />NVARCHAR#1,NVARCHAR2#1,BINARY,VARBINARY,IMAGE,<br />LOB,LONG,BLOB,CLOB,NCLOB,BFILE,RAW,ENUM,BFILE</td>
</tr>
<tr class="even">
<td></td>
<td>DefaultStreams</td>
<td>Integer
[1, ∞)</td>
<td>Default number of streams for a profiling job.</td>
<td>1</td>
</tr>
<tr class="odd">
<td></td>
<td>DefaultMaxMemory</td>
<td>Integer
[1024, ∞)</td>
<td>Default maximum memory for profiling jobs (in megabytes).</td>
<td>1024</td>
</tr>
<tr class="even">
<td></td>
<td>DefaultMinMemory</td>
<td>Integer
[1024, ∞)</td>
<td>Default minimum memory for profiling jobs (in megabytes).</td>
<td>1024</td>
</tr>
</tbody>
</table>
