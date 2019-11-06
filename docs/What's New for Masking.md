# What's New for Masking
## Synchronizing Masking Jobs and Universal Settings Across Engines
In 5.2 we introduced the ability to synchronize Masking Algorithms between engines to ensure consistent masking, regardless of the engine executing the masking. In 5.3 are expanding the list of syncable objects to include:

- Masking Jobs
- Connectors
- Rulesets
- Domains
- File Formats
- Mount Information

The sync of objects is possible through improvements to several sync API endpoints, including:

- GET /syncable-objects[?object_type=<type>]
- POST /export
- POST /export-async
- POST /import
- POST/import-async

This expansion of syncable objects ensures that users can sync their Masking Jobs and all the objects necessary for that masking job to execute successfully - regardless of the masking engine it lives on, allowing for easier scaling of Delphix Masking across the enterprise. Please see [Managing Multiple Masking Engines](/Managing_Multiple_Engines_for_Masking/Working_with_Multiple_Masking_Engines/)  for more details.

## Support for Kerberized Connections
In 5.2.4 we added support for Kerberos for our Oracle Masking Connector. In 5.3 we have expanded the list of connectors that support Kerberos to:

- SQL Server
- Sybase

To enable Kerberized connectors your engine must be configured properly and you must configure your masking Connectors for Kerberos. Kerberos can be enabled by going to the Advanced mode on Oracle, SQL Server and Sybase. Please see [Managing Connectors](/Connecting_Data/Managing_Connectors/) for more details.

![](./media/create_kerberos.png)

## Versioning Framework

6.0 marks the release of version 5.1 of the Masking API. For information on how the Masking API is versioned, please refer to the documentation here: [Masking API Versioning Documentation](/Delphix_Masking_APIs/Masking_Client/Backwards_Compatibility_API_Usage/#api-versioning-context/)

## New API Endpoints
In 6.0 we have expanded the list of API endpoints to include:


| **Group** | **Endpoints**      | **Description**       |
| ----------- | -----------      | ------------          |
| Application | DELETE /applications/{applicationId} | Delete application by ID |


## Other Improvements and Adjustments

In addition to the new API endpoints, we have improved existing API endpoints. These improvements include:

- Addition of the applicationId field to the application model
- Replacement of the application field with an applicationId field in the Envirionment model
- Removal of the classification field from the domain model
- Addition of the rulesetType field to the Masking, Profiling, Reidentification and Tokenization job models.
- Addition of mountName in the ConnectionInfo of a file connector and a mainframe dataset connector to use a filesystem mount point.
For more information please on Delphix Masking APIs please see [API documentation](https://maskingdocs.delphix.com/Delphix_Masking_APIs/Masking_Client/Masking_API_Client/).  Please note that the previous generation of Masking APIs (commonly referred to as V4) is EOL and no longer supported in this release. All users are encouraged to migrate to the V5 APIs.
