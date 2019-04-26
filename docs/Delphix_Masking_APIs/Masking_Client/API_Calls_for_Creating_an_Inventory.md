# API Calls for Creating an Inventory

Below are examples of requests you might enter and responses you might
receive from the Masking API client. For commands specific to your
masking engine, work with your interactive client at
http://**&lt;myMaskingEngine&gt**/masking/api-client/

!!! warning
    HTTPS (SSL/TLS) is recommended, but for explanatory purposes these examples use insecure HTTP

!!! info
    In all code examples, replace **&lt;myMaskingEngine&gt;** with the hostname or IP address of your virtual machine.

## Fetch Table Names from Database Connector

Object references you will need:

  - The ID of the database connector to fetch tables
for

!!! note
    This database connector ID (1, in this example) is included in the PATH for this operation, NOT the payload.

### **REQUEST**

``` bash
curl -X GET --header 'Accept: application/json' --header 'Authorization:
7c856e3d-5b20-4261-b5fe-cc2ffcee5ae0'
'http://<myMaskingEngine>/masking/api/database-connectors/1/fetch’
```

### **RESPONSE**

``` json
[ "ALL_COLUMNS", "DBVERIFICATION_TABLE"]
```

### **More info**

http://&lt;myMaskingEngine&gt;/masking/api-client/#!/databaseConnector/fetchTableMetadata

### **Example**

See how to use this in the context of a script
[here](../API_Examples/createInventory.md).

## Create Table Metadata

Object references you will need:

  - The name of the table to create the metadata for
  - The ruleset ID

### **REQUEST**

``` bash
curl -X POST --header 'Content-Type: application/json' --header 'Accept:
application/json' --header 'Authorization:
7c856e3d-5b20-4261-b5fe-cc2ffcee5ae0' -d '{ "tableName": "ALL_COLUMNS",
"rulesetId": 2 }'
'http://<myMaskingEngine>/masking/api/table-metadata'
```

### **RESPONSE**

``` json
{ "tableMetadataId": 2, "tableName": "ALL_COLUMNS", "rulesetId": 2
}
```

### **More info**

http://&lt;myMaskingEngine&gt;/masking/api-client/#!/tableMetadata/createTableMetadata

### **Example**

See how to use this in the context of a script
[here](../API_Examples/createInventory.md).

## Get All Column Metadata Belonging to Table Metadata

Object references you will need:

  - The table metadata ID to get the columns
for

!!! tip
    This table metadata ID (2, in this example) is included in the QUERY STRING for this operation, NOT the payload.

### **REQUEST**

``` bash
curl -X GET --header 'Accept: application/json' --header 'Authorization:
7c856e3d-5b20-4261-b5fe-cc2ffcee5ae0'
'http://<myMaskingEngine>/masking/api/column-metadata?table_metadata_id=2'
```

### **RESPONSE**

``` json
[ { "columnMetadataId": 12, "columnName": "schoolnme",
"tableMetadataId": 2, "columnLength": 50, "isMasked": false,
"isPrimaryKey": false, "isIndex": false, "isForeignKey": false }, … ]
```

Note that the above response has been truncated due to its length for
the purposes of this
documentation.

### **More info**

http://&lt;myMaskingEngine&gt;/masking/api-client/#!/columnMetadata/getAllColumnMetadata

### **Example**

See how to use this in the context of a script
[here](../API_Examples/createInventory.md).

## Update Column Metadata with Algorithm Assignment

Object references you will need:

  - Column metadata ID for the column you wish to
update

!!! tip
    This column metadata ID (20, in this example) is included in the PATH for this operation, NOT the payload.

  - Since the names can vary in the API and UI, you should use the names
    obtained through the API (these may not align with the UI).
  - Algorithm name
  - Domain name

### **REQUEST**

``` bash
curl -X PUT --header 'Content-Type: application/json' --header 'Accept:
application/json' --header 'Authorization:
7c856e3d-5b20-4261-b5fe-cc2ffcee5ae0' -d '{ "algorithmName":
"AddrLine2Lookup", "domainName": "ADDRESS_LINE2", "isProfilerWritable": false }'
'http://<myMaskingEngine>/masking/api/column-metadata/20'
```

### **RESPONSE**

``` json
{ "columnMetadataId": 20, "columnName": "l2_address",
"tableMetadataId": 2, "algorithmName": "AddrLine2Lookup", "domainName":
"ADDRESS_LINE2", "columnLength": 512, "isMasked": true, "isProfilerWritable": false, "isPrimaryKey":
false, "isIndex": false, "isForeignKey": false
}
```

### **More info**

http://&lt;myMaskingEngine&gt;/masking/api-client/#!/columnMetadata/updateColumnMetadata

###  **Example**

See how to use this in the context of a script
[here](../API_Examples/createInventory.md).
