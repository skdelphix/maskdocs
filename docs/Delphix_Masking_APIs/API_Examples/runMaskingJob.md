#runMaskingJob

```
#!/bin/bash
#
# This script will login and run a masking job. It depends on helpers in the helpers
# script as well as host and login information found in apiHostInfo and loginCredentials, respectively.
#
source apiHostInfo
eval $(cat loginCredentials)
source helpers

login
#
# When deciding which masking job to run we simply choose the first masking job found. You are
# encouraged to modify this to suit your needs. Please see get_masking_job_id in helpers for more information.
#
get_masking_job_id

echo "* running masking job '$MASKING_JOB_ID'..."
curl $SSL_CERT -X POST -H ''"$AUTH_HEADER"'' -H 'Content-Type: application/json' -H 'Accept: application/json' --data @- $MASKING_ENGINE/executions <<EOF
{
    "jobId": "$MASKING_JOB_ID"
}
EOF
echo




```
