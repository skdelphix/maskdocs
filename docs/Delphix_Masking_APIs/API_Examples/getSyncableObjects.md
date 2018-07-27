# getSyncableObjects

``` bash
#!/bin/bash
 
#
# This script is an "out of the box" script that goes through
# Login and GET /syncable-objects with the authentication
# token from Login
#
 
source apiHostInfo
eval $(cat loginCredentials)
source helpers
 
login
 
echo "* GET /syncable-objects from $EXPORT_ENGINE"
EXPORT_RESPONSE=$(curl $SSL_CERT -X GET -H ''"$AUTH_HEADER"'' -H 'Accept: application/json' $MASKING_ENGINE/syncable-objects)
echo $EXPORT_RESPONSE


```