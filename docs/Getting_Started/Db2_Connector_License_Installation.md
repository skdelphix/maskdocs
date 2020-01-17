# DB2 Connector License Installation

If you have been licensed to use the Delphix Masking DB2 Connector for Mainframe
or DB2 Connector for iSeries, you will need to obtain the respective DB2 Connector
package (tar file) and apply it to your Masking Engine(s). Each package is intended
to be installed and run from a workstation or laptop, not from the Delphix Appliance. 
These packages contain a script that must be used in a bash shell and depends on
the availability of the **curl** and **ssh** commands to install the respective license
on your remote Delphix Appliance. 

#### Applying DB2 Connector for Mainframe

1.  Go to <https://download.delphix.com/files/list/DB2%20Masking%20Mainframe/> and download DB2MaskingMainframe.tar 
2. Extract its contents using tar -xvf DB2MaskingMainframe.tar
3. cd db2-license
4. ./installdb2license.sh -h MASKING_ENGINE_HOST -P MASKING_ENGINE_PORT -u MASKING_ENGINE_ADMIN_USERNAME -p MASKING_ENGINE_ADMIN_PASSWORD [-C MASKING_ENGINE_PUBLIC_KEY_FILE] 

Where:

**MASKING_ENGINE_HOST** is the hostname for where the masking engine is running.

**MASKING_ENGINE_PORT** is the port for where the masking engine is listening on the MASKING_ENGINE_HOST (default is port 8282).

**MASKING_ENGINE_ADMIN_USERNAME** is the username for connecting to the masking engine (e.g., delphix_admin).

**MASKING_ENGINE_ADMIN_PASSWORD** is the masking engine password for <MASKING_ENGINE_ADMIN_USERNAME>.

**MASKING_ENGINE_PUBLIC_KEY_FILE** is the optional trusted server certificate (server public key) obtained from the masking engine.

!!! note
    To run the enablement script securely, run installdb2license.sh specifying your secure port (e.g., 8443) and trusted server certificate (server public key) using the -C option.

The script will enable the DB2 Mainframe connector and then recycle the Masking Engine, prompting the user for the Delphix sysadmin password for <MASKING_ENGINE_HOST> to first stop the Masking Engine and then to start it. After the DB2MaskingMainframe.tar package has been applied to your Masking Engine(s), "Database - MAINFRAME DB2" will appear in the Connector drop-down of the Masking Engine UI and can be used in the same way as other Database Connectors to create, profile, mask, certify, and provision rulesets.

#### Applying DB2 Connector for iSeries

1. Go to <https://download.delphix.com/files/list/DB2%20Masking%20i-Series/> and download DB2MaskingISeries.tar  
2. Extract its contents using tar -xvf DB2MaskingISeries.tar 
3. cd db2-license
4. ./installdb2license.sh -h MASKING_ENGINE_HOST -P MASKING_ENGINE_PORT -u MASKING_ENGINE_ADMIN_USERNAME -p MASKING_ENGINE_ADMIN_PASSWORD  [-C MASKING_ENGINE_PUBLIC_KEY_FILE] 

Where:

**MASKING_ENGINE_HOST** is the hostname for where the masking engine is running.

**MASKING_ENGINE_PORT** is the port for where the masking engine is listening on the MASKING_ENGINE_HOST (default is port 8282).

**MASKING_ENGINE_ADMIN_USERNAME** is the username for connecting to the masking engine (default is delphix_admin).

**MASKING_ENGINE_ADMIN_PASSWORD** is the masking engine password for MASKING_ENGINE_ADMIN_USERNAME.

**MASKING_ENGINE_PUBLIC_KEY_FILE** is the optional trusted server certificate (server public key) obtained from the masking engine.

!!! note
    To run the enablement script securely, run installdb2license.sh specifying your secure port (e.g., 8443) and trusted server certificate (server public key) using the -C option.

The script will enable the DB2 iSeries connector and then recycle the Masking Engine, prompting you for the Delphix sysadmin password for <MASKING_ENGINE_HOST> to first stop the Masking Engine and then to start it. After the DB2MaskingISeries.tar package has been applied to your Masking Engine(s), "Database - ISeries DB2" will appear in the Connector drop-down of the Masking Engine UI and can be used in the same way as other Database Connectors to create, profile, mask, certify, and provision rulesets.
