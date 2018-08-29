# Delphix Masking Engine Activities
Once you have provisioned a virtual database (VDB) for masking use in the Delphix Engine, you will need to complete the following activities in the Delphix Masking Engine. The five primary tasks to be completed are:

1. Add a masking application.
2. Add a masking environment.
3. Add a connector to the newly provisioned VDB.
4. Create masking rule sets to identify, select, and configure which tables you want to mask.
5. Run a masking job to mask the data.
Below is a visualization of this data masking user workflow:
![](./media/masking_steps.png)

## Login to the Delphix Masking Engine
1. Login to a web browser that points to  http://<server_or_IPAddress>:8282/dmsuite
2. Enter default username: delphix_admin.
3. Enter default user password:  Delphix_123.
4. The auto default user role is the Administrator role.

## Link a dSource
Follow the detailed steps found in the documentation: Link an Oracle Data Source.

## Provision a VDB to Prepare to Configure a Masking Job
In order to prepare data for masking, you must first provision a virtual databases (VDBs) in the Delphix Engine. This database will be used to configure the masking job. If you would like to test the functionality of the masking job while preserving the original data in the VDB, you may provision a second VDB to validate against. To do so, repeat these steps.

1. Login to the **Delphix Management** application.
2. Click **Manage**.
3. Select **Datasets**.
4. Select a **dSource**.
5. Select the **TimeFlow** tab and select a **dSource snapshot**.
6. Click the **Provision VDB** icon. 
7. Review the information for **Installation Home**, **Database Unique Name**, **SID**, and **Database Name**. Edit as necessary.
8. Review the **Mount Base** and **Environment User**. Edit as necessary.
9. If you want to use login credentials on the target environment that are different from the login credentials associated with the **Environment User**, select **Specify Privileged Credentials**.
10. Click **Next**.
11. Select a **Target Group** for the VDB and a **Snapshot Policy** for the VDB.
12. Click **Next**.
13. Specify any **Pre or Post Scripts** that should be used during the provisioning process.
14. Click **Advanced** to select Oracle Node Listeners or enter any VDB configuration settings or file mappings.
15. Click **Next**.
16. Click **Submit**.

