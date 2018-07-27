# createInventory

``` bash
#!/bin/bash
 
#
# This script will login, create table metadata for a given table name and ruleset, and then update an
# inventory (i.e. assign an algorithm and domain to a specific column of the table). It depends on helpers
# in the helpers script as well as host and login information found in apiHostInfo and loginCredentials, respectively.
# This script uses jq to process JSON. More information can be found here - https://stedolan.github.io/jq/.
#
 
source apiHostInfo
eval $(cat loginCredentials)
source helpers
 
login
 
#
# When deciding which connector, ruleset, and table to use we simply use the first ones found of each. You are
# encouraged to modify this to suit your needs. Please see the respective functions in helpers for more information.
#
get_connector_id
get_ruleset_id
get_table
 
echo "* creating table metadata for ruleset id '$RULESET_ID' with table '$TABLE_NAME'..."
TABLE_METADATA_RESPONSE=$(curl $SSL_CERT -s -X POST -H ''"$AUTH_HEADER"'' -H 'Content-Type: application/json' -H 'Accept: application/json' --data @- $MASKING_ENGINE/table-metadata <<EOF
{
    "tableName": "$TABLE_NAME",
    "rulesetId": $RULESET_ID
}
EOF)
check_error "$TABLE_METADATA_RESPONSE"
TABLE_METADATA_ID=$(echo $TABLE_METADATA_RESPONSE | jq -r '.tableMetadataId')
echo "using table metadata '$TABLE_METADATA_ID'"
 
get_column_metadata_id
 
curl $SSL_CERT -X PUT -H ''"$AUTH_HEADER"'' -H 'Content-Type: application/json' -H 'Accept: application/json' --data @- $MASKING_ENGINE/column-metadata/$COLUMN_METADATA_ID  <<EOF
{
    "algorithmName": "AddrLine2Lookup",
    "domainName": "ADDRESS_LINE2"
}
EOF
 
echo

```