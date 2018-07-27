# getSyncableObjectsExport

``` bash
#!/bin/bash
 
#
# This script will log in and get all syncable objects on
# the Masking Engine and then, given a grouping command, save the
# exported document in a file and export all syncable objects
# in the indicated group 
#
# Grouping command:
# algoType: -t <LOOKUP | BINARYLOOKUP | SEGMENT | TOKENIZATION | MAPPLET | KEY>
# algoCd: -n <RegexForAlgoName>
#
# Currently the response from GET /syncable-objects is saved
# to getobj_response.json, and the grouped input for /export
# in grouped_export_list.json, and the final export response
# into export_response.json. But of course, this can script
# can be modified to save to other specified places.
#
 
source apiHostInfo
eval $(cat loginCredentials)
source helpers
 
login
 
echo "* GET /syncable-objects"
GETOBJ_RESPONSE=$(curl $SSL_CERT -X GET -H ''"$AUTH_HEADER"'' -H 'Content-Type: application/json' $MASKING_ENGINE/syncable-objects)
echo $GETOBJ_RESPONSE > "./getobj_response.json"
 
# Create a temporary export list file
GROUPED_EXPORT_LIST="./grouped_export_list.json"
echo "[]" > $GROUPED_EXPORT_LIST
 
if [[ $1 == "-t" ]]; then
   ALGO_TYPE=$2
   echo "* Filter for all syncable objects of algorithm type $ALGO_TYPE" 
 
   jq -c '.responseList[]' getobj_response.json | while read i; do
      if [[ $(echo $i | jq '.objectType') == \"$ALGO_TYPE\" ]]; then
         # The key to getting the correct json format here was to use
         # the --argjson instead of --arg. --arg will stringify everything
         # and escape all special characters like {, ", etc.
         echo $(cat $GROUPED_EXPORT_LIST | jq --argjson obj "$i" '. |= . + [$obj]') > $GROUPED_EXPORT_LIST
      fi
   done
elif [[ $1 == "-n" ]]; then
   ALGO_NAME_REGEX=$2
   echo "* Filter for all syncable objects where algorithmCd matches the regex $ALGO_NAME_REGEX"
 
   jq -c '.responseList[]' getobj_response.json | while read i; do
      if [[ "$(echo $i | jq '.objectIdentifier.algorithmName')" =~ \"$ALGO_NAME_REGEX\" ]]; then
          echo $(cat $GROUPED_EXPORT_LIST | jq --argjson obj "$i" '. |= . + [$obj]') > $GROUPED_EXPORT_LIST
      fi
   done
fi
 
echo "* Export syncable objects from $GROUPED_EXPORT_LIST"
EXPORT_RESPONSE=$(curl $SSL_CERT -X POST -H ''"$AUTH_HEADER"'' -H 'Content-Type: application/json' -H 'Accept: application/json' -d "$(<$GROUPED_EXPORT_LIST)" $MASKING_ENGINE/export)
 
# Save the grouped export response into a file
echo $EXPORT_RESPONSE > export_response.json
echo '* Completed exporting. Check "export_response.json" for the export document. This export document json object will be what you literally put in as the input for import'


```