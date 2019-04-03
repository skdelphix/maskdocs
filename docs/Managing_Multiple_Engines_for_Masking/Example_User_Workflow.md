# User Workflow examples
This page provides some examples of some typical user workflows. More information on exactly how each endpoint works is available on the Endpoints page.

## Syncing all Global Objects
The following steps can be used to sync all global objects from Masking Engine A to Masking Engine B. This will sync all algorithms and domains and should be done prior to syncing jobs or rulesets which might depend on them. For more information on the global object, see the **Masking API Call Concepts** section.

*  On Masking Engine A, get the Authorization from the /login API

```
POST http://masking-engine-A:/masking/api/login

HEADER
Content-Type : application/json
Accept: application/json

BODY (raw)
{"username": "user123", "password": "pw123" }
```
Expected Result:
```
{ "Authorization": "dc2cff8b-e20d-4e28-8b7e-5d7c4aad0e2a" }
```


* On Masking Engine A, call GET /syncable-objects to get a list of syncable objects.
```
GET http://masking-engine-A/masking/api/syncable-objects

HEADER
Authorization : dc2cff8b-e20d-4e28-8b7e-5d7c4aad0e2a (whatever you get from login)
Content-Type : application/json
Accept: application/json
```
Expected Result:
```
[
{
"objectIdentifier": {
"keyId": "global"
},
"objectType": "KEY",
"revisionHash": "68eaffef400e426520a5fcbb683419db3be53317"
},
{
"objectIdentifier": {
"id": 4
},
"objectType": "MASKING_JOB",
"revisionHash": "485343f1a68698497946f4f70d1cfdd76d516fd8"
},
{
"objectIdentifier": {
"algorithmName": "AddrLine2Lookup"
},
"objectType": "LOOKUP",
"revisionHash": "f397c46a97bddacf4203e35d7a538fda4bba6b12"
},
{
"objectIdentifier": {
"id": "global"
},
"objectType": "GLOBAL_OBJECT",
"revisionHash": "e230c46a97bddacf4201a35d7a538fda4bca6b14"
}
…
]
```

* On Masking EngineA, call /export-async on GLOBAL_OBJECT.
```
POST http://masking-engine-A/masking/api/export-async

HEADER
Authorization : dc2cff8b-e20d-4e28-8b7e-5d7c4aad0e2a
Content-Type : application/json
Accept: application/json
passphrase (Optional): password to encrypt the export document

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
EXPECTED RESULT
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

* Download the export document with the reference above via the /file-download endpoint.
```
GET http://masking-engine-A/masking/api/file-downloads/EXPORT-ZXhwb3J0X2RvY3VtZW50Xzk0Wjlva3JDLmpzb24=

HEADER
Authorization : dc2cff8b-e20d-4e28-8b7e-5d7c4aad0e2a
Accept: application/octet-stream

EXPECTED RESULT
File - The exported document that would look identical to the response from /export with the same request body and headers
```

An example export document will look like this.
```
{
"exportResponseMetadata": {
"exportHost": "masking-engine-A:8282",
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
"blob":     "RAAAAAokZmZhNWIxNjktODMwMC00N2FlLWJjZmMtNjVhNDUzYWI3OTBjEhgyMDE4LTA2LTE1VDIwOjE2OjIwLjY2MFogBSgBFwIAAAokZmZhNWIxNjktODMwMC00N2FlLWJjZmMtNjVhNDUzYWI3OTBjEu4DCi8IFBIrCiV0eXBlLmdvb2dsZWFwaXMuY29tL0ludGVnZXJJZGVudGlmaWVyEgIIARIvCA4SKwoldHlwZS5nb29nbGVhcGlzLm...",
"signature": "MCwCFAWGf/97wb+oYuSQizj8U12n7jpQAhQKGCaOJ4U8XyDAOEhMUWkzZXHrpw==",
"publicKey": "MIHxMIGoBgcqhkjOOAQBMIGcAkEA/KaCzo4Syrom78z3EQ5SbbB4sF7ey80etKII864WF64B81uRpH5t9jQTxeEu0ImbzRMqzVDZkVG9xD7nN1kuFwIVAJYu3cw2nLqOuyYO5rahJtk0bjjFAkBnhHGyepz0TukaScUUfbGpq.."
}
```

* On Masking Engine B, use the import-async endpoint to import the document downloaded from engine A.
```
POST http://masking-engine-B/masking/api/import-async?force_overwrite=true
HEADER
Authorization : dc2cff8b-e20d-4e28-8b7e-5d7c4aad0e2a
Accept: application/octet-stream

EXPECTED RESULT
File - The import status document that would look identical to the response from /import with the same export document

HEADER
Authorization : dc2cff8b-e20d-4e28-8b7e-5d7c4aad0e2a
Content-Type: multipart/form-data

Accept: application/json
passphrase (Optional): password to encrypt the export document

PARAMETER
force_overwrite and environment_id. See the discussion in /import for more detail.

BODY
File - The downloaded export document
```
Expected Result:
```
EXPECTED RESULT
{
"asyncTaskId": 3,
"operation": "IMPORT",
"reference": "IMPORT-AWhwb3J0X2Ru2VtZW50Xzk0Wjlva3JDLmpzb24=",
"status": "RUNNING",
"startTime": "2018-06-16T20:38:31.483+0000",
"cancellable": false
}
```

* On Masking Engine B, retrieve the completed import status using the reference from the returned Async Task response with /file-downloads
```
GET http://masking-engine-A/masking/api/file-downloads/IMPORT-AWhwb3J0X2Ru2VtZW50Xzk0Wjlva3JDLmpzb24=

HEADER
Authorization : dc2cff8b-e20d-4e28-8b7e-5d7c4aad0e2a
Accept: application/octet-stream
```

Expected Result:
File - The import status document that would look identical to the response from /import with the same export document


## Syncing a Masking Job

The following steps provide an example of how to export a Masking Job from Masking Engine A to Masking Engine B using the synchronous endpoints of /export and /import. This presumes that all of the global objects such as algorithms and domains that the masking job relies on have already been synced. This can also be done via the asynchronous endpoint with the same workflow as above.


* On Masking Engine A, export the MASKING_JOB using the /export endpoint.
```
POST http://masking-engine-A/masking/api/export

HEADER
Authorization : dc2cff8b-e20d-4e28-8b7e-5d7c4aad0e2a (whatever you get from login)
Content-Type : application/json
Accept: application/json
passphrase (Optional): password to encrypt the export document

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
!!!note
    To sync a profile job, swap out the objectType for "PROFILE_JOB" and provide the id of the profile job to sync. Profile jobs are syncable starting in version 5.3.2.0.

Expected Result:
```
{
"exportResponseMetadata": {
"exportHost": "masking-engine-A:8282",
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
"blob":     "RAAAAAokZmZhNWIxNjktODMwMC00N2FlLWJjZmMtNjVhNDUzYWI3OTBjEhgyMDE4LTA2LTE1VDIwOjE2OjIwLjY2MFogBSgBFwIAAAokZmZhNWIxNjktODMwMC00N2FlLWJjZmMtNjVhNDUzYWI3OTBjEu4DCi8IFBIrCiV0eXBlLmdvb2dsZWFwaXMuY29tL0ludGVnZXJJZGVudGlmaWVyEgIIARIvCA4SKwoldHlwZS5nb29nbGVhcGlzLm...",
"signature": "MCwCFAWGf/97wb+oYuSQizj8U12n7jpQAhQKGCaOJ4U8XyDAOEhMUWkzZXHrpw==",
"publicKey": "MIHxMIGoBgcqhkjOOAQBMIGcAkEA/KaCzo4Syrom78z3EQ5SbbB4sF7ey80etKII864WF64B81uRpH5t9jQTxeEu0ImbzRMqzVDZkVG9xD7nN1kuFwIVAJYu3cw2nLqOuyYO5rahJtk0bjjFAkBnhHGyepz0TukaScUUfbGpq.."
}
```

!!!note
    The requestedObjectList returns the list of objects you’ve requested in the export, and the exportedObjectList returns a list of all objects that were exported. This will include both the requested ones and their dependencies.


* On Masking Engine B, import the masking job. You will need to provide an environment for it to import into.
```
POST http://masking-engine-B/masking/api/import?force_overwrite=false&environment_id=1

HEADER
(same as export)

PARAMETER
force_overwrite and environment_id. See the details in the Masking API Call Concepts section for more details .

BODY
(Whatever gets returned from export)
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
