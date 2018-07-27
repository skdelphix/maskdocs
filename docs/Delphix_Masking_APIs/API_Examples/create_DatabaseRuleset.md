# create DatabaseRuleset

``` bash
#!/bin/bash
 
#
# This script will login and create a database ruleset for a database connector. It depends on helpers in the helpers
# script as well as host and login information found in apiHostInfo and loginCredentials, respectively.
#
 
source apiHostInfo
eval $(cat loginCredentials)
source helpers
 
login
 
#
# When deciding which database connector we will use, we simply choose the first database connector found. You are
# encouraged to modify this to suit your needs. Please see get_connector_id in helpers for more information.
#
get_connector_id
 
echo "* creating database ruleset 'myRuleset' in db connector '$CONNECTOR_ID'..."
curl $SSL_CERT -X POST -H ''"$AUTH_HEADER"'' -H 'Content-Type: application/json' -H 'Accept: application/json' --data @- $MASKING_ENGINE/database-rulesets <<EOF
{
    "rulesetName": "myRuleset",
    "databaseConnectorId": $CONNECTOR_ID
}
EOF
 
echo

```