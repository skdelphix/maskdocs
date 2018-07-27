# create DatabaseConnector

``` bash
#!/bin/bash
 
#
# This script will login and create a database connector in an environment. It depends on helpers in the helpers
# script as well as host and login information found in apiHostInfo and loginCredentials, respectively.
#
 
source apiHostInfo
eval $(cat loginCredentials)
source helpers
 
login
 
#
# When deciding which environment to place the connector in we simply choose the first environment found. You are
# encouraged to modify this to suit your needs. Please see get_environment_id in helpers for more information.
#
get_environment_id
 
echo "* creating database connector 'connector' in environment '$ENVIRONMENT_ID'..."
curl $SSL_CERT -X POST -H ''"$AUTH_HEADER"'' -H 'Content-Type: application/json' -H 'Accept: application/json' --data @- $MASKING_ENGINE/database-connectors <<EOF
{
    "connectorName": "connector",
    "databaseType": "ORACLE",
    "environmentId": $ENVIRONMENT_ID,
    "host": "myHost",
    "password": "myPassword",
    "port": 1234,
    "schemaName": "MYSCHEMA",
    "sid": "mySID",
    "username": "MYUSERNAME"
}
EOF
 
echo
```