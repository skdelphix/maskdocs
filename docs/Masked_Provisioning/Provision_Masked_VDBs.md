# Provision Masked VDBs
Masked virtual databases (VDBs) function just like normal VDBs. The only distinction is that the data they contain has been masked by a masking job. Masked VDBs can be replicated to a separate Delphix Engine (in non-prod) without sending the original data that was obfuscated during masking using a process called Selective Data Distribution (SDD). This topic describes how to work with masked VDBs.

## Prerequisites

Before attempting to create a Masked VDB, you should be familiar with both Delphix Virtualization and Delphix Masking concepts and workflows.


## Restrictions
- A single masking job cannot be assigned to multiple VDBs simultaneously. If you are using the same masking ruleset on multiple VDBs, be sure to create a unique job for each VDB to avoid any issues with provisioning or refreshing.
- Provisioning or refreshing masked VDBs is only supported for Oracle, MS SQL Server and Sysbase. Provisioning or refreshing other types of masked VDBs such as DB2 are not support.
- You cannot apply additional masking jobs to a masked VDB or its children.
- If a masking job has been applied to a VDB, you cannot create an unmasked snapshot of that VDB.
- Masking must take place during the process of provisioning a VDB. If an existing VDB has not had a masking job applied to it, then you cannot mask that particular VDB at any point in the future. All the data within the VDB and its parents will be accessible if it is replicated using SDD.
- When selecting a connector to use for Masked Provisioning, a "basic" connector must be used **unless** you are masking an Oracle Pluggable Database (PDB), in which case an "advanced" connector must be used.

## Identifying and Navigating to Masked VDBs
Masked VDBs appear in the Virtualization Engine's Datasets pane, just like regular VDBs. They are most obviously identified by the different icon used to represent them. In addition, a masked VDBs Configuration tab will contain information about the masking job that you applied to it. Generally, anything you can do with an unmasked VDB is also possible with a masked VDB.
![] (/media/masked_vdb.png)

## Provisioning Masked VDBs
- In the Virtualization Engine, associate a masking job with a dSource.
- Use the dSource provision wizard to provision a VDB with a masking job.

### Associating a Masking Job with the dSource
To provision a masked VDB, you must first indicate that the masking job you are using is complete and applicable to a particular database. You do this by associating the masking job with a dSource.

1. In the **Datasets** panel on the left-hand side of the screen, click the dSource to which the masking job is applicable and with which it will be associated.
2. Click the **Configuration** tab.
3. Click the **Masking** tab.
  ![] (/media/masking_tab.png)

4. Click the **pencil** icon to edit.  All masking jobs on this Delphix Engine that have not been associated with another dSource will be listed on the right-hand side.
5. Select the **job** you want to associate with this dSource.
6. Click the **green checkmark** to confirm.
  ![] (/media/mask_job.png)
7. Repeat for any other jobs that you want to associate with this dSource at this time.

The Delphix Engine now considers this masking job to be applicable to this dSource and ready for use. When provisioning from snapshots of this dSource, this masking job will now be available.

!!! note

    Masking jobs can also be associated with virtual sources in addition to dSources.

### Provisioning a Masked VDB using the dSource Provisioning Wizard
The steps required to provision a masked VDB are almost identical to the steps required to provision an unmasked VDB. Once you have created a masked VDB, you cannot un-mask it, nor can you alter which masking job it uses. All snapshots in the VDBs TimeFlow will always be masked using the masking method that you selected when you provisioned the masked VDB.

1. In the **Datasets** panel on the left-hand side of the screen, select the dSource.
2. Click the **TimeFlow** tab.
3. Click **Provision VDB** icon.
4. Review the information for Installation Home, Database Unique Name, SID, and Database Name. Edit as necessary.
5. Review the Mount Base and Environment User. Edit as necessary.
    - If you want to use login credentials on the target environment that are different from the login credentials associated with the Environment User, select Specify Privileged Credentials.
6. Click **Next**.
7. If necessary, edit the **Target Group** for the VDB.
8. Select the **None** option for the Snapshot Policy for the VDB.
    - **Snapshot Policy Selection**: For almost all use cases involving Masked VDBs, a Snapshot Policy of None is appropriate. Using a Snapshot Policy in conjunction with SDD can result in the leak of sensitive data.
9. Click **Next**.
10. Click **Mask this VDB**. You will be presented with two options to mask this VDB:
    - Select an existing masking job: Choose this option if you want to mask using preconfigured Masking Job. Only masking jobs that have been associated with the parent dSource will be available.
    - **Selecting Unique Masking Jobs**: If you are using the same masking ruleset on multiple VDBs, be sure to create a unique job for each VDB to avoid any issues when provisioning or refreshing.
    ![] (/media/mask_rule_set.png)
    - Masking using scripts(s): Alternatively, you may define some Configure Clone scripts in the Hooks step to perform masking.
    - **Defining Configure Clone Hooks to Mask VDB**: If you choose to mask using script(s), you must define the Configure Clone hooks to run masking jobs yourself. If you don't define any Configure Clone hooks in the Hooks step, the data will be marked as masked, but it will not be masked.
    ![] (/media/mask_hooks.png)
11. Click **Next**.
12. Specify any **Pre or Post Scripts** that should be used during the provisioning process. If the VDB was configured before running the masking job using scripts that impact either user access or the database schema, those same scripts should also be used here. Be sure to define the **Configure Clone** hooks to run the masking job if you choose to mask using script(s) in the Masking step.
    ![] (/media/hooks.png)
13. Click **Next**.
14. Click **Submit**.

If you click Actions in the the upper right-hand corner, the Actions sidebar will appear and list an action indicating that masking is running. You can verify this and monitor progress by going to the Masking Engine page and clicking the Monitor tab.

![] (/media/monitor.png)

!!! note

    Once you have created a masked VDB, you can provision its masked data to create additional VDBs, in the same way that you can provision normal VDBs. Since the parent masked VDB contains masked data, child VDBs will only have masked data. This is a great way to distribute multiple independent copies of masked data that is both time- and space-efficient.

## Refresh a Masked VDB
You refresh a masked VDB in exactly the same way as you refresh a normal VDB. As with provisioning a masked VDB, the masking job will be run during the refresh process. 

1. Login to the Delphix Management application.
2. Click Manage.
3. Select Datasets.
4. Select the VDB you want to refresh.
5. Click the Refresh VDB button (2 circular arrows).
6. Select More Accurate and Next.
7. Select desired refresh point snapshot or click the eye icon to choose Latest available range, A point in time, or An SCN to refresh from.
8. Click Next. 
9. Click Submit to confirm.
10. Click the Actions link to watch the progress of the refresh job.
11. To see when the VDB was last refreshed/provisioned, check the Time Point on the Status page.

## Disassociating a Masking Operation on a dSource
If a masking job is found to be unsuitable or should be retired, you can disassociate it though the same database card that you used to associate it.

1. Deselect the job.
2. Click green arrow to confirm.
Note that this will only prevent the creation of new masked VDBs with this job. It will not alter existing masked VDBs in any way. When disassociating a job, review the existing masked VDBs and consider whether you need to delete or disable any of them.

## Masked VDB Data Operations

The following data operations are available to masked VDBs:

- Rewind : Alter the database to contain masked data from a previous point in time.  
- Refresh : Get new data from the parent dSouce and mask it.
- Disable	: Turn off the database and remove it from the host system.	
- Enable : Turn on the database and make it available on the host system.


## Virtualization and Masking Engine Compatibility Matrix

| **Virtualization Engine Version** | **Masking Engine Version** |
| --------------------------------- | -------------------------- |
| 5.0 releases | 5.0 releases (minor versions do not need to match) |
| 5.1 releases | 5.1 releases (minor versions do not need to match) |
| 5.2 releases | 5.2 releases (minor versions do not need to match) |
| 5.2.5.0 (or later 5.2 minor release) | 5.2.5.0 (or later 5.2 minor release) |
| 5.3 releases | 5.3 releases (minor versions do not need to match) |

