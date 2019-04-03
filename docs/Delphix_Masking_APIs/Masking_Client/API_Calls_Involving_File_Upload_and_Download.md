# API Calls Involving File Upload and Download

## File Download
API calls involving file download through API client are noteworthy because if the request fails, the API client will continue to show the "loading"  icon indefinitely.

To avoid this, make all file download calls through CURL instead. An example of a file download call using CURL is below.

```
curl -X GET --header 'Accept: application/octet-stream' --header
'Authorization: ec443730-124e-4958-a872-324a975bb500'
-o "/home/user/downloads"
'http://<myMaskingEngine>/masking/api/file-downloads/EXPORT-ZXhwb3J0X2RvY3VtZW50X2dGZU9JMVYxLmpzb24%3D'
```
The `-o` flag from above specifies the location to save the file to.
## File Upload
API calls involving file upload are noteworthy because the generated
curl from the Masking API client will be **missing the parameter
referencing the file**; as such, those commands from the Masking API
client **will not work**.

Instead, below are examples of working requests and responses for API
calls involving file upload.

For commands specific to your masking engine, work with your interactive
client at
http://**&lt;myMaskingEngine&gt;**/masking/api-client/

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
'http://<myMaskingEngine>/masking/api/file-formats'
```
### **RESPONSE**

```
{ "fileFormatId": 123, "fileFormatName": "delimited_format.txt",
"fileFormatType": "DELIMITED"
}
```

### **More info**

http://&lt;myMaskingEngine&gt;/masking/api-client/#!/fileFormat/createFileFormat

## Creating an SSH Key

### **REQUEST**

``` bash
curl -X POST --header 'Content-Type: multipart/form-data' --header
'Accept: application/json' --header 'Authorization:
d1313dd8-2ed9-4699-8e88-2b6a089ae2a6' -F
sshKey=@/path/to/ssh_key/this_file_name_is_your_ssh_key_name.txt
'http://<myMaskingEngine>/masking/api/ssh-keys'
```

### **RESPONSE**

``` json
{ "sshKeyName": "this_file_name_is_your_ssh_key_name.txt"
}
```

### **More info**

http://&lt;myMaskingEngine&gt;/masking/api-client/#!/sshKey/createSshKey
