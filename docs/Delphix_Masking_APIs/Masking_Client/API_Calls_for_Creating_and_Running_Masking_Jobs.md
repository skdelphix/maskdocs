# API Calls for Creating and Running Masking Jobs

Below are examples of requests you might enter and responses you might
receive from the Masking API client. For commands specific to your
masking engine, work with your interactive client at
http://**&lt;myMaskingEngine&gt;**:8282/masking/api-client/

!!! note
    In all code examples, replace **&lt;myMaskingEngine&gt;** with the hostname or IP address of your virtual machine.

!!! warning
    HTTPS (SSL/TLS) is recommended, but for explanatory purposes these examples use insecure HTTP.

## Creating a Masking Job

Object references you will need:

  - The ID of the ruleset for which you wish to create the masking job

**REQUEST**

``` bash
curl -X POST --header 'Content-Type: application/json' --header 'Accept:
application/json' --header 'Authorization:
e23bad24-8760-4091-a131-34f235d9b2d6' -d '{ "jobName":
"some_masking_job", "rulesetId": 7, "jobDescription": "This example
illustrates a MaskingJob with just a handful of the possible fields set.
It is meant to exemplify a simple JSON body that can be passed to the
endpoint to create a MaskingJob.", "feedbackSize": 100000,
"onTheFlyMasking": false }'
'http://<myMaskingEngine>:8282/masking/api/masking-jobs'
```

### **RESPONSE**

``` json
{ "jobId": 1, "jobName": "some_masking_job", "rulesetId": 7,
"createdBy": "Axistech", "createdTime": "2017-07-04T00:31:00.952+0000",
"environmentId": 2, "feedbackSize": 100000, "jobDescription": "This
example illustrates a MaskingJob with just a handful of the possible
fields set. It is meant to exemplify a simple JSON body that can be
passed to the endpoint to create a MaskingJob.", "maxMemory": 1024,
"minMemory": 1024, "multiTenant": false, "numInputStreams": 1,
"onTheFlyMasking": false }
```

!!! note
    The response includes the ID of the newly created job (“jobId”).

### **More info**

http://&lt;myMaskingEngine&gt;:8282/masking/api-client/#!/job/createMaskingJob

## Running a Masking Job

Create a new execution of a masking job.

Object references you will need:

  - The ID of the job you want to run

### **REQUEST**

``` bash
curl -X POST --header 'Content-Type: application/json' --header 'Accept:
application/json' --header 'Authorization:
e23bad24-8760-4091-a131-34f235d9b2d6' -d '{ "jobId": 1 }'
'http://<myMaskingEngine>:8282/masking/api/executions'
```

### **RESPONSE**

``` json
{ "executionId": 1, "jobId": 1, "status": "RUNNING"
}
```

### **More info**

http://&lt;myMaskingEngine&gt;:8282/masking/api-client/#!/execution/createExecution

## Checking the Status of a Masking Job

Object references you will need:

  - The ID of the execution you want to check (IN THE PATH)

!!! note
    This execution id (1, in this example) is included in the PATH for this operation, NOT the payload.

### **REQUEST**

``` bash
curl -X GET --header 'Accept: application/json' --header 'Authorization:
8935f7f7-6de6-40ba-80d8-d8956b71248b'
'http://<myMaskingEngine>:8282/masking/api/executions/1'
```

### **RESPONSE**

``` json
{
  "executionId": 1,
  "jobId": 1,
  "status": "SUCCEEDED",
  "rowsMasked": 1000,
  "rowsTotal": 1000,
  "startTime": "2019-02-14T21:51:13.253+0000",
  "endTime": "2019-02-14T21:51:54.956+0000"
}
```

### **More info**

http://&lt;myMaskingEngine&gt;:8282/masking/api-client/#!/execution/getExecutionById

## Retrieving Execution Events related to a Masking Job

Object references you will need:

  - The ID of the execution you want to check (as a URL parameter).

!!! note
    This execution id (1, in this example) is specified as a URL parameter for this operation.

    The execution-events endpoint returns execution events for a specified job execution. These execution events report failures or warnings associated with the masking job execution. NOT specifying the execution in the URL parameter will retrieve all execution events for all masking jobs.

### **REQUEST**

``` bash
curl -X GET --header 'Accept: application/json' --header 'Authorization:
8935f7f7-6de6-40ba-80d8-d8956b71248b'
'http://<myMaskingEngine>:8282/masking/api/execution-events?execution_id=1&page_number=1'
```

### **RESPONSE**

``` json
{
  "_pageInfo": {
    "numberOnPage": 1,
    "total": 1
  },
  "responseList": [
    {
      "executionEventId": 1,
      "executionId": 1,
      "eventType": "UNMASKED_DATA",
      "severity": "WARNING",
      "cause": "PATTERN_MATCH_FAILURE",
      "count": 1000,
      "timeStamp": "2019-02-14T21:51:51.790+0000",
      "executionComponentId": 1,
      "maskedObjectName": "RCHARS64_T1_0",
      "algorithmName": "DateShiftVariable"
    }
  ]
}
```

### **More info**

http://&lt;myMaskingEngine&gt;:8282/masking/api-client/#!/execution-events/getAllExecutionEvents

## Retrieving Nonconformant Data Samples associated with an Execution Event

Object references you will need:

  - The ID(s) of the execution event(s) you want to check (as one or more URL parameters). 

!!! note
    This execution event id (1, in this example) is specified as a URL parameter for this operation.

    The non-conformant-data-sample endpoint returns nonconformant data samples for a specified job execution event. These nonconformant data samples will report the data patterns that caused the nonconforming data execution event to help identify why data is not getting masked. NOT specifying an execution event in the URL parameter will retrieve all nonconformant data samples events for all masking jobs.


### **REQUEST**

``` bash
curl -X GET --header 'Accept: application/json' --header 'Authorization:
8935f7f7-6de6-40ba-80d8-d8956b71248b'
'http://<myMaskingEngine>:8282/masking/api/non-conformant-data-sample?execution_event_id=1&page_number=1'
```

### **RESPONSE**

``` json
{
  "_pageInfo": {
    "numberOnPage": 7,
    "total": 7
  },
  "responseList": [
    {
      "dataSampleId": 1,
      "executionEventId": 1,
      "dataSample": "LLLLL",
      "count": 200
    },
    {
      "dataSampleId": 2,
      "executionEventId": 1,
      "dataSample": "LLLLLL",
      "count": 400
    },
    {
      "dataSampleId": 3,
      "executionEventId": 1,
      "dataSample": "LLLL",
      "count": 80
    },
    {
      "dataSampleId": 4,
      "executionEventId": 1,
      "dataSample": "LLLLLLL",
      "count": 100
    },
    {
      "dataSampleId": 5,
      "executionEventId": 1,
      "dataSample": "LLLLLLLLLLL",
      "count": 50
    },
    {
      "dataSampleId": 6,
      "executionEventId": 1,
      "dataSample": "LLLLLLLLL",
      "count": 10
    },
    {
      "dataSampleId": 7,
      "executionEventId": 1,
      "dataSample": "LLLLLLLL",
      "count": 40
    }
  ]
}
```

### **More info**

http://&lt;myMaskingEngine&gt;:8282/masking/api-client/#!/non-conformant-data-sample/getAllNon-conformantDataSamples
