# createEnvironment

``` bash
#!/bin/bash
 
#
# This script will login and create an environment with an application. It depends on helpers in the helpers
# script as well as host and login information found in apiHostInfo and loginCredentials, respectively.
#
 
source apiHostInfo
eval $(cat loginCredentials)
source helpers
 
login
 
#
# When deciding which application to place the environment in we simply choose the first application found. You are
# encouraged to modify this to suit your needs. Please see get_application_id in helpers for more information.
#
get_application_id
 
echo "* creating environment 'newEnv' in application '$APPLICATION_ID'..."
curl $SSL_CERT -X POST -H ''"$AUTH_HEADER"'' -H 'Content-Type: application/json' -H 'Accept: application/json' --data @- $MASKING_ENGINE/environments <<EOF
{
    "environmentName": "newEnv",
    "application": "$APPLICATION_ID",
    "purpose": "MASK"
}
EOF
 
echo

```