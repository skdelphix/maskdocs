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

    The executions endpoint only returns status for the most recent job run, this is the expected behavior. Although the Masking Service does not currently retain historical execution results, the API has been designed to allow for historical results to be returned in the future.

### **REQUEST**

``` bash
curl -X GET --header 'Accept: application/json' --header 'Authorization:
8935f7f7-6de6-40ba-80d8-d8956b71248b'
'http://<myMaskingEngine>:8282/masking/api/executions/1'
```

### **RESPONSE**

``` json
{ "executionId": 1, "jobId": 1, "status": "SUCCEEDED"
}
```

### **More info**

http://&lt;myMaskingEngine&gt;:8282/masking/api-client/#!/execution/getExecutionById
