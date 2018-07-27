# API Calls Involving File Upload

API calls involving file upload are noteworthy because the generated
curl from the Masking API client will be **missing the parameter
referencing the file**; as such, those commands from the Masking API
client **will not work**.

Instead, below are examples of working requests and responses for API
calls involving file upload.

For commands specific to your masking engine, work with your interactive
client at
http://**&lt;myMaskingEngine&gt;**:8282/masking/api-client/

!!! warning
    HTTPS (SSL/TLS) is recommended, but for explanatory purposes these examples use insecure HTTP.

!!! note
    In all code examples, replace **\<myMaskingEngine\>** with the hostname or IP address of your virtual machine.

## Creating a File Format

### **REQUEST**

```
curl -X POST --header 'Content-Type: multipart/form-data' --header
'Accept: application/json' --header 'Authorization:
d1313dd8-2ed9-4699-8e88-2b6a089ae2a6' -F
fileFormat=@/path/to/file_format/delimited_format.txt -F
fileFormatType=DELIMITED
'http://<myMaskingEngine>:8282/masking/api/file-formats'
```
### **RESPONSE**

```
{ "fileFormatId": 123, "fileFormatName": "delimited_format.txt",
"fileFormatType": "DELIMITED"
}
```

### **More info**

http://&lt;myMaskingEngine&gt;:8282/masking/api-client/#!/fileFormat/createFileFormat

## Creating an SSH Key

### **REQUEST**

``` bash
curl -X POST --header 'Content-Type: multipart/form-data' --header
'Accept: application/json' --header 'Authorization:
d1313dd8-2ed9-4699-8e88-2b6a089ae2a6' -F
sshKey=@/path/to/ssh_key/this_file_name_is_your_ssh_key_name.txt
'http://<myMaskingEngine>:8282/masking/api/ssh-keys'
```

### **RESPONSE**

``` json
{ "sshKeyName": "this_file_name_is_your_ssh_key_name.txt"
}
```

### **More info**

http://&lt;myMaskingEngine&gt;:8282/masking/api-client/#!/sshKey/createSshKey
