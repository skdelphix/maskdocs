# apiHostInfo

``` bash
#!/bin/bash
 
#
# This file contains all the host information for the masking engine. Additionally,
# this file allows configuration of SSL if desired.
#
 
 
# update host name
HOST="myMaskingEngine.com"
API_PATH="masking/api"
 
# To connect via SSL, set $SSL to "on" and update the port if necessary (default 8443).
# Additionally, you must update the path to the ssl certificate.
SSL="off"
SSL_PORT="8443"
# update cert name
SSL_CERT_PATH="self-signed.cer"
 
if [ "$SSL" = "on" ]
then
    MASKING_ENGINE="https://$HOST:$SSL_PORT/$API_PATH"
    SSL_CERT="--cacert $SSL_CERT_PATH"
else
    MASKING_ENGINE="http://$HOST:8282/$API_PATH"
    SSL_CERT=""
fi
```