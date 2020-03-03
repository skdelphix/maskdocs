# User Workflow examples
This page provides some examples of some typical user workflows. More information on exactly how each endpoint works is available on the [Sync Endpoints Section](Endpoints).

## Syncing all Global Objects
The following steps can be used to sync all global objects from Masking Engine A to Masking Engine B. This will sync all algorithms and domains and should be done prior to syncing jobs or rulesets which might depend on them. For more information on the global object, see the [Sync Concepts Section](Masking_API_Call_Concepts).

### Source Masking Engine Steps

#### 1. Login
Login on the source Masking Engine to obtain an Authorization token value.

```
POST https://a.example.com/masking/api/login

HEADER
Content-Type: application/json
Accept: application/json

BODY
{
  "username": "user123",
  "password": "pw123"
}
```

curl example:
```
curl -X POST --cacert /path/to/cert --header 'Content-Type: application/json' --header 'Accept: application/json' -d '{ "username": "user123", "password": "pw123" }' 'https://a.example.com/masking/api/login'
```

Expected Result:
```
{
  "Authorization": "dc2cff8b-e20d-4e28-8b7e-5d7c4aad0e2a"
}
```

#### 2. Get the identifier
Call GET /syncable-objects to obtain the GLOBAL_OBJECT's information.

```
GET https://a.example.com/masking/api/syncable-objects?object_type=GLOBAL_OBJECT

HEADER
Authorization: dc2cff8b-e20d-4e28-8b7e-5d7c4aad0e2a (value from the /login response)
Accept: application/json
```

curl example:
```
curl -X GET --cacert /path/to/cert --header 'Accept: application/json' --header 'Authorization: dc2cff8b-e20d-4e28-8b7e-5d7c4aad0e2a' 'https://a.example.com/masking/api/syncable-objects?object_type=GLOBAL_OBJECT'
```

Expected Result:
```
{
  "_pageInfo": {
    "numberOnPage": 1,
    "total": 1
  },
  "responseList": [
    {
      "objectIdentifier": {
        "id": "global"
      },
      "objectType": "GLOBAL_OBJECT",
      "revisionHash": "8d5236bb029c2176aa568b930786b63253e4f9e4"
    }
  ]
}
```

#### 3. Export the object

Call POST /export-async to asynchronously export the GLOBAL_OBJECT and use the passphrase header to encrypt the export.

!!! note

    The optional passphrase header cannot be specified using the interactive
    [API Client tool](/Delphix_Masking_APIs/Masking_Client/Masking_API_Client/#api-client).
    An example of how to specify this header using a cURL command is shown below.


```
POST https://a.example.com/masking/api/export-async

HEADER
Authorization: dc2cff8b-e20d-4e28-8b7e-5d7c4aad0e2a
Content-Type: application/json
Accept: application/json
passphrase: my example passphrase

BODY
[
  {
    "objectIdentifier": {
      "id": "global"
    },
    "objectType": "GLOBAL_OBJECT"
  }
]
```

```
curl -X POST --cacert /path/to/cert --header 'Content-Type: application/json' --header 'Accept: application/json' --header 'Authorization: dc2cff8b-e20d-4e28-8b7e-5d7c4aad0e2a' --header 'passphrase: my example passphrase' -d '[{"objectIdentifier":{"id":"global"},"objectType":"GLOBAL_OBJECT"}]' 'https://a.example.com/masking/api/export-async'
```

Expected Result:
```
{
  "asyncTaskId": 2,
  "operation": "EXPORT",
  "reference": "EXPORT-ZXhwb3J0X2RvY3VtZW50Xzk0Wjlva3JDLmpzb24=",
  "status": "RUNNING",
  "startTime": "2018-06-15T20:36:35.483+0000",
  "cancellable": false
}
```

#### 4. Download the export document

Use the reference above to download the export document via the /file-download endpoint.

```
GET https://a.example.com/masking/api/file-downloads/EXPORT-ZXhwb3J0X2RvY3VtZW50Xzk0Wjlva3JDLmpzb24=

HEADER
Authorization: dc2cff8b-e20d-4e28-8b7e-5d7c4aad0e2a
Accept: application/octet-stream
```

curl example:
```
curl -X GET --cacert /path/to/cert --header 'Accept: application/json' --header 'Authorization: dc2cff8b-e20d-4e28-8b7e-5d7c4aad0e2a' 'https://a.example.com/masking/api/file-downloads/EXPORT-ZXhwb3J0X2RvY3VtZW50Xzk0Wjlva3JDLmpzb24='
```

Expected Result:
An export document that will look like this.

```
{
  "exportResponseMetadata": {
    "exportHost": "a.example.com",
    "exportDate": "Fri Jun 15 20:16:20 UTC 2018",
    "requestedObjectList": [
      {
        "objectIdentifier": {
          "id": "global"
        },
        "objectType": "GLOBAL_OBJECT",
        "revisionHash": "579850b1c88baf74cee6bad61d81e2aa3dcc206c"
      }
    ],
    "exportedObjectList": [
      {
        "objectIdentifier": {
          "id": "DRIVING_LC"
        },
        "objectType": "DOMAIN",
        "revisionHash": "9ee90782488d14d369f9595dad7f593c961e785f"
      },
      {
        "objectIdentifier": {
          "algorithmName": "DrivingLicenseNoLookup"
        },
        "objectType": "LOOKUP",
        "revisionHash": "e08ac9bfd4ed9f64d486cb47cdc07deb30ccc20f"
      },
      ...
    ]
  },
  "blob": "RAAAAAokZmZhNWIxNjktODMwMC00N2FlLWJjZmMtNjVhNDUzYWI3OTBjEhgyMDE4LTA2LTE1VDIwOjE2OjIwLjY2MFogBSgBFwIAAAokZmZhNWIxNjktODMwMC00N2FlLWJjZmMtNjVhNDUzYWI3OTBjEu4DCi8IFBIrCiV0eXBlLmdvb2dsZWFwaXMuY29tL0ludGVnZXJJZGVudGlmaWVyEgIIARIvCA4SKwoldHlwZS5nb29nbGVhcGlzLm...",
  "signature": "MCwCFAWGf/97wb+oYuSQizj8U12n7jpQAhQKGCaOJ4U8XyDAOEhMUWkzZXHrpw==",
  "publicKey": "MIHxMIGoBgcqhkjOOAQBMIGcAkEA/KaCzo4Syrom78z3EQ5SbbB4sF7ey80etKII864WF64B81uRpH5t9jQTxeEu0ImbzRMqzVDZkVG9xD7nN1kuFwIVAJYu3cw2nLqOuyYO5rahJtk0bjjFAkBnhHGyepz0TukaScUUfbGpq.."
}
```

#### 5. Cleanup

When the export document is no longer needed, use the /export-async endpoint to cleanup the exported documents.

```
DELETE https://a.example.com/masking/api/export-async

HEADER
Authorization: dc2cff8b-e20d-4e28-8b7e-5d7c4aad0e2a
Accept: application/json
```

curl example:
```
curl -X DELETE --header 'Accept: application/json' --header 'Authorization: dc2cff8b-e20d-4e28-8b7e-5d7c4aad0e2a' 'https://a.example.com/masking/api/export-async'
```

Expected Result: no content

### Destination Masking Engine Steps

#### 1. Login
Login on the destination Masking Engine to obtain an Authorization token value (see example above).


#### 2. Import the object

On Masking Engine B, use the import-async endpoint to import the document downloaded from engine A.

```
POST https://b.example.com/masking/api/import-async?force_overwrite=true

HEADER
Authorization: dc2cff8b-e20d-4e28-8b7e-5d7c4aad0e2a
Content-Type: multipart/form-data
Accept: application/json
passphrase: my example passphrase
```

curl example:
```
curl -X POST --cacert /path/to/cert --header 'Content-Type: multipart/form-data' --header 'Accept: application/json' --header 'Authorization: dc2cff8b-e20d-4e28-8b7e-5d7c4aad0e2a' --header 'passphrase: my example passphrase' -F file=@export.json 'https://b.example.com/masking/api/import-async?force_overwrite=true'
```

Expected Result:
```
{
  "asyncTaskId": 1,
  "operation": "IMPORT",
  "reference": "IMPORT-aW1wb3J0X2RvY3VtZW50X2lZQVFKWEFsLmpzb24=",
  "status": "WAITING",
  "cancellable": false
}
```

#### 3. Verify status

On Masking Engine B, call the /file-downloads endpoint using the reference from the returned Async Task response to retrieve the completed import status.

```
GET https://b.example.com/masking/api/file-downloads/IMPORT-aW1wb3J0X2RvY3VtZW50X2lZQVFKWEFsLmpzb24=

HEADER
Authorization: dc2cff8b-e20d-4e28-8b7e-5d7c4aad0e2a
Accept: application/octet-stream
```

curl example:
```
curl -X GET --cacert /path/to/cert --header 'Accept: application/octet-stream' --header 'Authorization: dc2cff8b-e20d-4e28-8b7e-5d7c4aad0e2a' 'https://b.example.com/masking/api/file-downloads/IMPORT-aW1wb3J0X2RvY3VtZW50X2lZQVFKWEFsLmpzb24='
```

Expected Result: 

An import status document that reports the success or failure of each object imported.

```
[
  {
    "objectIdentifier": {
      "id": 7
    },
    "importedObjectIdentifier": {
      "id": 7
    },
    "objectType": "PROFILE_EXPRESSION",
    "importStatus": "SUCCESS"
  },
  {
    "objectIdentifier": {
      "id": "CERTIFICATE_NO"
    },
    "importedObjectIdentifier": {
      "id": "CERTIFICATE_NO"
    },
    "objectType": "DOMAIN",
    "importStatus": "SUCCESS"
  },
  ...
]
```

#### 4. Cleanup

Once the status is no longer needed, use the /import-async endpoint to cleanup the exported documents.

```
DELETE https://b.example.com/masking/api/import-async

HEADER
Authorization: dc2cff8b-e20d-4e28-8b7e-5d7c4aad0e2a
Accept: application/json
```

curl example:
```
curl -X DELETE --cacert /path/to/cert --header 'Accept: application/json' --header 'Authorization: dc2cff8b-e20d-4e28-8b7e-5d7c4aad0e2a' 'https://b.example.com/masking/api/import-async'
```

Expected Result: no content

## Syncing a Masking Job

The following steps provide an example of how to export a Masking Job from Masking Engine A to Masking Engine B using the synchronous endpoints of /export and /import. This presumes that all of the global objects such as algorithms and domains that the masking job relies on have already been synced. This can also be done via the asynchronous endpoint with the same workflow as above.


### 1. Export the job

Before this step, the /login and /syncable-objects endpoints should have been called to obtain the authorization token and job identifier respectively. Then use the /export endpoint to obtain an export document with the desired MASKING_JOB. In this example, the optional passphrase is used to encrypt the export document.

!!!note
    To sync a profile job, swap out the objectType for "PROFILE_JOB" and provide the id of the profile job to sync. Profile jobs are syncable starting in version 5.3.2.0.

```
POST http://a.example.com/masking/api/export

HEADER
Authorization: dc2cff8b-e20d-4e28-8b7e-5d7c4aad0e2a
Content-Type: application/json
Accept: application/json
passphrase: password to encrypt the export document

BODY
[
  {
    "objectIdentifier": {
      "id": 4
    },
    "objectType": "MASKING_JOB"
  }
]
```

curl example:
```
curl -X POST --cacert /path/to/cert --header 'Content-Type: application/json' --header 'Accept: application/json' --header 'Authorization: dc2cff8b-e20d-4e28-8b7e-5d7c4aad0e2a' --header 'passphrase: my example passphrase' -d '[ { "objectIdentifier": { "id": 4 }, "objectType": "MASKING_JOB" } ]' 'https://a.example.com/masking/api/export'
```

Expected Result:
```
{
  "exportResponseMetadata": {
    "exportHost": "a.example.com",
    "exportDate": "Fri Jun 15 20:16:20 UTC 2018",
    "requestedObjectList": [
      {
        "objectIdentifier": {
          "id": 1
        },
        "objectType": "MASKING_JOB",
        "revisionHash": "579850b1c88baf74cee6bad61d81e2aa3dcc206c"
      }
    ],
    "exportedObjectList": [
      {
        "objectIdentifier": {
          "id": 1
        },
        "objectType": "DATABASE_RULESET",
        "revisionHash": "bf63b401129cbc84f90eeb708281e98121f5a829"
      },
      {
        "objectIdentifier": {
          "id": "FIRST_NAME"
        },
        "objectType": "DOMAIN_REFERENCE",
        "revisionHash": "e6a52079843afd2625f20237fd50f56254c7e630"
      },
      {
        "objectIdentifier": {
          "id": 1
        },
        "objectType": "MASKING_JOB",
        "revisionHash": "579850b1c88baf74cee6bad61d81e2aa3dcc206c"
      },
      {
        "objectIdentifier": {
          "id": 1
        },
        "objectType": "DATABASE_CONNECTOR",
        "revisionHash": "6455f39dfa354a54bdf4ef69d6511a6c2bb19db3"
      },
      {
        "objectIdentifier": {
          "algorithmName": "FirstNameLookup"
        },
        "objectType": "ALGORITHM_REFERENCE",
        "revisionHash": "13b0a51a7e3904f52526c442419c54b39033dca3"
      }
    ]
  },
  "blob": "RAAAAAokZmZhNWIxNjktODMwMC00N2FlLWJjZmMtNjVhNDUzYWI3OTBjEhgyMDE4LTA2LTE1VDIwOjE2OjIwLjY2MFogBSgBFwIAAAokZmZhNWIxNjktODMwMC00N2FlLWJjZmMtNjVhNDUzYWI3OTBjEu4DCi8IFBIrCiV0eXBlLmdvb2dsZWFwaXMuY29tL0ludGVnZXJJZGVudGlmaWVyEgIIARIvCA4SKwoldHlwZS5nb29nbGVhcGlzLm...",
  "signature": "MCwCFAWGf/97wb+oYuSQizj8U12n7jpQAhQKGCaOJ4U8XyDAOEhMUWkzZXHrpw==",
  "publicKey": "MIHxMIGoBgcqhkjOOAQBMIGcAkEA/KaCzo4Syrom78z3EQ5SbbB4sF7ey80etKII864WF64B81uRpH5t9jQTxeEu0ImbzRMqzVDZkVG9xD7nN1kuFwIVAJYu3cw2nLqOuyYO5rahJtk0bjjFAkBnhHGyepz0TukaScUUfbGpq.."
}
```

!!!note
    The requestedObjectList returns the list of objects you’ve requested in the export, and the exportedObjectList returns a list of all objects that were exported. This will include both the requested ones and their dependencies.

### 2. Import the job

On Masking Engine B, import the masking job. You will need to provide an environment for it to import into.

```
POST http://b.example.com/masking/api/import?force_overwrite=false&environment_id=1

HEADER
Authorization: dc2cff8b-e20d-4e28-8b7e-5d7c4aad0e2a
Content-Type: application/json
Accept: application/json
passphrase: password to encrypt the export document

PARAMETER
force_overwrite and environment_id. See the details in the Masking API Call Concepts section for more details .

BODY
(Whatever gets returned from export)
```

curl example:
```
curl -X POST --cacert /path/to/cert --header 'Content-Type: application/json' --header 'Accept: application/json' --header 'Authorization: dc2cff8b-e20d-4e28-8b7e-5d7c4aad0e2a' --header 'passphrase: my example passphrase' -d @/path/to/export.json 'https://b.example.com/masking/api/import?force_overwrite=false&environment_id=1'
```

Expected Result:
```
[
  {
    "objectIdentifier": {
      "id": 3033
    },
    "importedObjectIdentifier": {
      "id": 1
    },
    "objectType": "DATABASE_CONNECTOR",
    "importStatus": "SUCCESS"
  },
  {
    "objectIdentifier": {
      "id": 5421
    },
    "importedObjectIdentifier": {
      "id": 1
    },
    "objectType": "DATABASE_RULESET",
    "importStatus": "SUCCESS"
  }
  ...
]
```
