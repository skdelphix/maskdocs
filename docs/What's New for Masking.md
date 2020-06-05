# What's New for Masking

## 6.0.1.0 Release

### Extended Connectors

Testing a new change. This is new. Extended Connectors is a new feature that allows you to upload additional JDBC Drivers to the Delphix Masking engine. This enables masking data sources that are not natively supported by Delphix Masking. For more information, please refer to the [Managing Extended Connectors](/Connecting_Data/Managing_Extended_Connectors/) section.

### Sync for Tokenization and Reidentification Jobs

The Sync feature allows you to coordinate the operation of multiple engines. This release adds Sync support for Tokenization and Reidentification Jobs. For more information on the Sync feature, please refer to the [Managing Multiple Engines for Masking](/Managing_Multiple_Engines_for_Masking/Working_with_Multiple_Masking_Engines/) section.

### File Record Type APIs

When masking a delimited or fixed length file, the Masking Engine uses a file format to interpret the file's contents. Each format has one or more record types. In previous releases, these record types could only be created and managed through the graphical user interface. This release adds the ability to also create and manage file record types through the APIs. Specifically, the following APIs were added:

| **Group** | **Endpoints** | **Description** |
|-----------|---------------|-----------------|
| recordType | GET /record-types | Get all record type |
| | POST /record-types | Create record type |
| | DELETE /record-types/{recordTypeId} | Delete record type by ID |
| | GET /record-types/{recordTypeId} | Get record type by ID |
| | PUT /record-types/{recordTypeId} | Update record type |
| recordTypeQualifier | GET /record-type-qualifiers | Get all record type qualifiers |
| | POST /record-type-qualifiers |Create record type qualifier |
| | DELETE /record-type-qualifiers/{recordTypeQualifierId} | Delete record type qualifier by ID |
| | GET /record-type-qualifiers/{recordTypeQualifierId} |Get record type qualifier by ID |
| | PUT /record-type-qualifiers/{recordTypeQualifierId} | Update record type qualifier by ID |

Note that record types are only used for delimited and fixed length file formats. For more information on record types, see the [Adding Record Types for Files](/Connecting_Data/Managing_Inventories/#adding-record-types-for-files) section.

## 6.0.0.0 Release

### Objects Names Requirements
In 6.0 we have added validations for objects names that can be created/renamed manually.
For more information please refer to [Naming Requirements](/Getting_Started/Naming_Requirements/).
Please pay attention to the fact that enforcing these requirements might fail the import, sync, or upgrade from pre-6.0 release.
Please refer to the following [Knowledge Base Article KBA5096](https://support.delphix.com/Delphix_Masking_Engine/Object_Naming_Requirements_\(KBA5096\)) on how to solve those failures.

### Versioning Framework

6.0 marks the release of version 5.1 of the Masking API. For information on how the Masking API is versioned, please refer to the documentation here: [Masking API Versioning Documentation](/Delphix_Masking_APIs/Masking_Client/Backwards_Compatibility_API_Usage/#api-versioning-context)

### New API Endpoints
In 6.0 we have expanded the list of API endpoints to include:


| **Group** | **Endpoints**      | **Description**       |
| ----------- | -----------      | ------------          |
| Application | DELETE /applications/{applicationId} | Delete application by ID |
| Mount Filesystem | GET /mount-filesystem | Get all mounts |
| | POST /mount-filesystem | Create a mount |
| |GET /mount-filesystem/{mountId} | Get a mount by ID |
| |DELETE /mount-filesystem/{mountId} | Delete a mount by ID |
| |PUT /mount-filesystem/{mountId} | Update a mount by ID |
| |PUT /mount-filesystem/{mountId}/connect | Connect a mount by ID |
| |PUT /mount-filesystem/{mountId}/disconnect | Disconnect a mount by ID |
| |PUT /mount-filesystem/{mountId}/remount | Remount a mount by ID |

In addition to the new API endpoints, we have improved existing API endpoints. These improvements include:

- Addition of the applicationId field to the application model
- Replacement of the application field with an applicationId field in the Envirionment model
- Removal of the classification field from the domain model
- Addition of the rulesetType field to the Masking, Profiling, Reidentification and Tokenization job models.
- Addition of mountName in the ConnectionInfo of a file connector and a mainframe dataset connector to use a filesystem mount point.

For more information on Delphix Masking APIs please see the [API documentation](https://maskingdocs.delphix.com/Delphix_Masking_APIs/Masking_Client/Masking_API_Client/).

### NFS and CIFS Mounts

In previous releases, the Masking Engine has supported masking files via FTP or SFTP. In this release, we have added the ability for users to directly mount and mask a file system over NFS and CIFS. This should dramatically simplify the process of file masking. As with other Masking Engine objects, the Sync feature can be used to coordinate mount objects across multiple engines. For more information on the mount feature, please refer to the [Managing Remote Mounts](/Connecting_Data/Managing_Remote_Mounts/) section.

## 5.3 Release

### Synchronizing Masking Jobs and Universal Settings Across Engines
In 5.2 we introduced the ability to synchronize Masking Algorithms between engines to ensure consistent masking, regardless of the engine executing the masking. In 5.3 we are expanding the list of syncable objects to include:

- Masking Jobs
- Connectors
- Rulesets
- Domains
- File Formats

The sync of objects is possible through improvements to several sync API endpoints, including:

- GET /syncable-objects[?object_type=<type>]
- POST /export
- POST /export-async
- POST /import
- POST/import-async

This expansion of syncable objects ensures that users can sync their Masking Jobs and all the objects necessary for that masking job to execute successfully - regardless of the masking engine it lives on, allowing for easier scaling of Delphix Masking across the enterprise. Please see [Managing Multiple Masking Engines](/Managing_Multiple_Engines_for_Masking/Working_with_Multiple_Masking_Engines/)  for more details.

### Support for Kerberized Connections
In 5.2.4 we added support for Kerberos for our Oracle Masking Connector. In 5.3 we have expanded the list of connectors that support Kerberos to:

- SQL Server
- Sybase

To enable Kerberized connectors your engine must be configured properly and you must configure your masking Connectors for Kerberos. Kerberos can be enabled by going to the Advanced mode on Oracle, SQL Server and Sybase. Please see [Managing Connectors](/Connecting_Data/Managing_Connectors/) for more details.

![](./media/create_kerberos.png)

### New API Endpoints
In 5.2 we released an all-new set of API endpoints allowing for the automation of many masking workflows. In 5.3 we have expanded this list of API endpoints around Algorithms, Users, Roles, File Upload, System Information, Login, Rulesets, and Connector. Below are the net new API endpoints:


| **Group** | **Endpoints**      | **Description**       |
| ----------- | -----------      | ------------          |
| Algorithms  | POST /algorithms | Create algorithm      |
|             | DELETE /algorithms/{algorithmName}| Delete algorithm by name   |
|             | GET /algorithms/{algorithmName}        | Get algorithm by name     |
|             | PUT /algorithms/{algorithmName}                 | Update algorithm by name  |
|             | PUT /algorithms/{algorithmName}/randomize-key                 | Randomize key by name      |
| Users | GET /users | Get all users      |
|  | POST /users| Create user   |
|     | DELETE /users/{userId}   | Delete user by ID     |
|     |    GET /users/{userId}         | Get user by ID |
|     | PUT /users/{userId} | Update user by ID|
| Roles  | GET /roles | Get all roles|
| | POST /roles | Create role|
| | DELETE /roles/{roleId}| Delete role by ID|
|  | GET /roles/{roleId}| Get role by ID|
|  | PUT /roles/{roleId} |Update role by ID|
| Rulesets| PUT /database-rulesets/{databaseRulesetId}/bulk-table-update|Update the rule set’s tables|
| | PUT /database-rulesets/{databaseRulesetId}/refresh| Refresh the rule set|
|Connectors|POST /database-connectors/{databaseConnectorId}/test|Test a database connector|
| | POST /database-connectors/test|Test an unsaved database connector|
|  |POST /file-connectors/{fileConnectorId}/test|Test a file connector|
|  | POST /file-connectors/test|Test an unsaved file connector|
|Async Tasks|GET /async-tasks|Get all asyncTasks|
|  |GET /async-tasks/{asyncTaskId}|Get asyncTask by ID|
|  |PUT /async-tasks/{asyncTaskId}/cancel|Cancel asyncTask by ID|
|File Upload/Download|DELETE /file-uploads|Delete all file uploads|
|  | POST /file-uploads | Upload file|
|  | GET /file-downloads/{fileDownloadId}|Download file|
|System Information|GET /system-information | Get version, etc.|
|Login/Logout|PUT /logout | User logout|
|Executions|GET /execution-components | Status for a table, file, or Mainframe data set|
| Tokenization Job  | GET /tokenization-jobs | Get all tokenization jobs|
| | POST /tokenization-jobs | Create tokenization job|
| | DELETE /tokenization-jobs/{tokenizationJobid}| Delete tokenization job by ID|
|  | GET /tokenization-jobs/{tokenizationJobid}| Get tokenization job by ID|
|  | PUT /tokenization-jobs/{tokenizationJobid} |Update tokenization job by ID|
| Re-identification Job  | GET /reidentification-jobs | Get all re-identification jobs|
| | POST /reidentification-jobs | Create re-identification job|
| | DELETE /reidentification-jobs/{reidentificationJobid}| Delete re-identification job by ID|
|  | GET /reidentification-jobs/{reidentificationJobid}| Get re-identification job by ID|
|  | PUT /reidentification-jobs/{reidentificationJobid} |Update re-identification job by ID|
| Database Rulesets  | PUT  | Update Database Ruleset by ID|


In addition to the net new API endpoints, we have improved pre-existing API endpoints. Some of the improvements include:

- Addition of DB2 iSeries and Mainframe to connector endpoints.
- Addition of Kerberos configuration on Oracle, SQL Server and Sybase connectors
- Ability to have ruleset refresh drop tables
- Support for XML file types
- Addition of dataType to column metadata
- Addition of isProfilerWritable field to file-field-metadata endpoints. This is now represented in the API as a new *isProfilerWritable* boolean field in the body of a file-field-metadata. When the isProfilerWritable field is set to true,  the algorithm/domain assignment on a column can be overwritten by the profiler. When the field is false, it may not be overwritten.
- Addition of multipleProfilerCheck field to Profile Job endpoints. This feature is turned on using the boolean field in the body of a profile job. The job profiler normally stops profiling a column as soon as it flags a field as sensitive. If *multipleProfilerCheck* is true, the profiler will continue to scan the column for additional sensitive patterns. In the event that it finds more than one pattern, it will tag all the data domains found and apply 'one' standard algorithm for all those domains. The standard algorithm is ‘Null SL’ as of 5.3.4.0.
This feature was formerly called ‘multi PHI’.


For more information on Delphix Masking APIs please see the [API documentation](https://maskingdocs.delphix.com/Delphix_Masking_APIs/Masking_Client/Masking_API_Client/).  Please note that the previous generation of Masking APIs (commonly referred to as V4) is EOL and no longer supported in this release. All users are encouraged to migrate to the V5 APIs.
