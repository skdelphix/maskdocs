# Endpoints

## GET /syncable-objects\[?object\_type=\<type\>\]

This endpoint lists all objects in an engine that are syncable and can
be exported. Any object which can be exported, can be imported into
another engine. The endpoint takes an optional parameter to filter by a
specific object type. Each object is listed with its revision\_hash.
Note that if a syncable object depends on a non-syncable object (i.e.
DOMAIN using a mapping algorithm), it will say so in the “revisionHash”
attribute, and will not be exportable.

Example CURL command:

``` ssh
curl -X GET
--header 'Accept: application/json'
--header 'Authorization: 21c45f0e-82f4-4b04-9072-b49072986231'
'http://masking-engine.com/masking/api/syncable-objects?page_number=1'
```

## POST /export

This endpoint allows you to export one or more objects in batch fashion.
The result of the export is an export document and a set of metadata
that describes what was exported. You are expected to specify which
objects to export by copying their object identifiers from the
/syncable-objects endpoint.

The endpoint has a single optional header, *passphrase*. If you provide
the passphrase, the export document will be encrypted using it.

Example CURL command:

``` ssh
curl -X POST
--header 'Content-Type: application/json'
--header 'Accept: application/json'
--header 'Authorization: 21c45f0e-82f4-4b04-9072-b49072986231'
-d '[
{  
"objectIdentifier": {“id”: 1},  
"objectType": "MASKING_JOB",  
"revisionHash": "asdfjkl12jijfdsaklfj21ojasdk"  
}  
]'
'http://masking-engine.com/masking/api/export'
```

## POST /export-async

This endpoint does exactly the same thing as /export, but the execution
is done asynchronously. The response returns an async task in the form
of this:

``` json
{  
"asyncTaskId": 66,  
"operation": "EXPORT",  
"reference": "EXPORT-ZXhwb3J0X2RvY3VtZW50XzJjcm1EV09yLmpzb24=",  
"status": "RUNNING",  
"startTime": "2018-04-13T17:49:55.354+0000",  
"cancellable": false  
}
```

Example CURL command:

``` ssh
curl -s -X POST
--header 'Content-Type: application/json'
--header 'Accept: application/json'
--header 'Authorization: 21c45f0e-82f4-4b04-9072-b49072986231'
-d "[  
{  
"objectIdentifier": {“id”: 1},  
"objectType": "MASKING_JOB",  
"revisionHash": "asdfjkl12jijfdsaklfj21ojasdk"  
}  
]"
"http://masking-engine.com/masking/api/export-async"
```

The *reference* is used to retrieve the export document of completed
async export tasks from the /file-downloads endpoint. The downloaded
file from this reference should look exactly the same as the response
from /export.

Example CURL command:

``` ssh
curl -s -X GET
--header 'Accept: application/octet-stream'
--header 'Authorization: 21c45f0e-82f4-4b04-9072-b49072986231'
-o "<OUTPUT_FILE_PATH>" "http://masking-engine.com/masking/api/file-downloads/EXPORT-ZXhwb3J0X2RvY3VtZW50XzJjcm1EV09yLmpzb24="
```

### Error handling

If an error occurs while exporting one or more elements in the export
document, the entire export will
abort.

## POST /import

```
POST /import?force_overwrite=<true|false>[&environment_id=<id>][&source_environment_id=<id>]
```

This endpoint allows you to import a document exported from another
engine. The response returns a list of objects that were imported and
whether the import was successful.

The endpoint has one required parameter, *force\_overwrite*, two
optional parameters *environment\_id* and *source\_environment\_id*, and
an optional HTTP header, *passphrase*, which if provided, will cause the
engine to attempt to decrypt the document using the specified
passphrase. The required *force\_overwrite* parameter dictates how to
deal with conflicting objects. *environment\_id* is necessary for all
non-global objects that need to belong in an environment.
*source\_environment\_id* is used for On-The-Fly masking jobs.

Example CURL command:

``` ssh
curl -X POST
--header 'Content-Type: application/json'
--header 'Accept: application/json'
--header 'Authorization: 21c45f0e-82f4-4b04-9072-b49072986231'
-d '{  
"exportResponseMetadata": {  
"exportHost": "masking-engine.com:8282",  
"exportDate": "Mon Aug 13 16:29:30 UTC 2018",  
"exportedObjectList": [  
{  
"objectIdentifier": {  
"algorithmName": "lookup_alg"  
},  
"objectType": "LOOKUP",  
"revisionHash": "cf84d82c21f0e9d4105d37ae7979c0848486d861"  
},  
{  
"objectIdentifier": {  
"keyId": "global"  
},  
"objectType": "KEY",  
"revisionHash": "1d8e9bc552d3ca1dcd218f9e197ea3955ccc29be"  
}  
]  
},
"blob": "<OMITTED>",
"signature": "<OMITTED>", \
"publicKey": "<OMITTED>" \  
}'
'http://masking-engine.com/masking/api/import?force_overwrite=true'
```

## POST /import-async

```
POST /import-async?force_overwrite=<true|false>[&environment_id=<id>][&source_environment_id=<id>]
```

This endpoint does exactly the same thing as /import, but the execution
is done asynchronously and the body is taken in as a file. The response
returns an async task in the form of this:

``` json
{  
"asyncTaskId": 67,  
"operation": "IMPORT",  
"reference": "IMPORT-ZXhwb3J0X2RvY3VtZW50XzJjcm1EV09yLmpzb24=",  
"status": "RUNNING",  
"startTime": "2018-04-13T17:49:55.354+0000",  
"cancellable": false  
}
```

The *reference* is used to retrieve the import status of completed async
import tasks from the /file-downloads endpoint. The downloaded file from
this reference should look exactly the same as the response from
/import.

Example CURL command:

``` ssh
curl -s -X POST
--header 'Content-Type: multipart/form-data'
--header 'Accept: application/json'
--header 'Authorization: 21c45f0e-82f4-4b04-9072-b49072986231'
-F "file=@<DOWNLOADED_FILE_PATH>"
"http://masking-engine.com/masking/api/import-async?force_overwrite=true"
```
