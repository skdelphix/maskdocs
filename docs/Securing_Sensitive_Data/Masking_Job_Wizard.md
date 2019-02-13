# Masking Job Wizard  
The Delphix Masking job wizard enables users to create and modify masking jobs.
While the wizard facilitates a number of workflows and operations, more
advanced functionality and a finer control of features is available directly
in the masking application. The Job Wizard currently functions only with certain
data platforms, but these constraints do not apply when working directly in the
masking application.

## Supported Data Platforms
The following data platforms are currently supported from within the Job Wizard:
 - Oracle Database
 - RDS Oracle Database
 - MSSQL Server Database
 - Sybase Database

This restricted list only affects your use of the wizard; an expanded number of
platforms are supported directly in the masking application. Some operations
within the Job Wizard are also limited. See below for details.

## Supported Operations
While creating a masking job in the Job Wizard, you are able to do the following:

- Create a new application or use an existing application
- Create a new environment or use an existing environment
- Create a new connector*
- Create a new rule set
- Update inventory*
- Create a masking job*
- Update a masking job
- Change the connector for an existing job
- Change the rule set for an existing connector
- Run a newly created job immediately
- Run an updated job immediately after the update

!!! note
    Operations marked with an asterisk are limited in the Job Wizard but fully supported in the main application.

## What is Not Supported in the Wizard
The following data platforms and operations are not supported in the Job Wizard.
To access additional functionality, use the main masking application.

### Unsupported Data Types
The following data types are supported when using the main masking application
but are not currently supported in the Job Wizard:

- DB2 Database
- PostgreSQL Database
- Generic Database
- Delimited File
- Excel Sheet File
- Fixed File
- Mainframe Data Set
- XML File

### Unsupported Operations
The following operations are not yet supported from within the Job Wizard:

- Creating any connector or rule set for an unsupported data type
- Deleting any application, environment, connector, rule set, or masking job
- Importing or exporting any object
- Updating an environment
- Creating a connector using Advanced mode
- Updating a connector
- Updating a rule set
- Creating a job for an unsupported data type
- Modifying a job for an unsupported data type
- Monitoring running jobs
- Creating, editing, deleting, or running any Profile jobs

## Opening the Masking Job Wizard
When you first login to masking, the welcome screen offers a link to learn more
or begin masking immediately. To open the Job Wizard, click Run on the welcome
page.

![Welcome](./media/welcome.png)
To use the Job Wizard from the masking application, click the Create Job button
in the upper right-hand corner, as highlighted in the screenshot below.

![](./media/create_job.png)

## Creating a New Masking Job
The Job Wizard makes creating a new masking job much easier by guiding you
through the process. You can create new objects or choose to use existing ones
that have already been defined.  When creating a new masking job, the Job Wizard
follows this sequence:

- Job Naming
- Application/Environment Selection
- Connection Selection
- Rule Set Selection
- Inventory Selection
- Summary Page

You can navigate back and forth through the pages of the Job Wizard.

!!! note
    If the product times out due to long inactivity, you will need to start over. |

To create a new masking Job using the new Job Wizard, follow the procedure below:

1. Log into your Delphix Masking Engine and from the Welcome screen select  Run.
2. Select the New radio button and enter a name for your Masking job.
   ![] (./media/job.png)
3. Click Next.
4. From the drop-down menu select an Application and Environment. If none exist use the Add button to add one.
   ![] (./media/job_env.png)
5. Click Next.
6. Select a Connector from the drop-down menu. If none exists select the Add button, then use the Add Connector dialog to add a new connector. The Job Wizard only supports the following  Connector types:
   - Database - MS SQL
   - Database - Oracle
   - Database - RDS Oracle
   - Database - Sybase
   ![] (./media/job_connection.png)
7.Click Next.
8. On the Rule Set screen select an existing Rule set or create a new one by clicking the Add button.
  ![] (./media/job_rule_set.png)
9. Click Next.
10. From the Inventory screen select how your data will be masked. In the screenshot below we are masking subscriber last names.
   ![] (./media/job_inventory.png)
11. Click Next.
12. The final screen of the Job Wizard displays a Summary of your selections.
   ![] (./media/job_summary.png)
13. Clicking Run Masking Job Now and go to Monitor progress, saves your job and runs it immediately. Save Job allows you to save your job and run it at a later date. Note: Selecting this option means your data will not be masked until you run the job.

### When Objects Are Saved
Application, environment, connector, and rule set objects are created and
persist after you click the Add button and see a success message. If you cancel
the Job Wizard before completing the job setup, the objects you created will be
saved, and they will be available for use the next time you launch the Job Wizard.

The Inventory definition is saved when you change the selection of a table or
column, or when another View filter is applied.

The masking job is saved when you click either Save Job or Run Masking Job Now
and go to Monitor progress and a success message is returned on the
Summary screen.

## Updating an Existing Masking Job
You can use the Job Wizard to modify any masking job that targets a supported
data type.

1. On the Job screen of the Job Wizard, select Modify Existing
2. From the list of available jobs slect the one you want to modify. This list only shows jobs that are supported in the wizard. You can filter the job list by selecting the filter icon .
3. Once you select a job, you can change the following as part of the Modify flow:
   - Change/create new connector
   - Change/create new rule set
   - Update inventory
   - Save or run the modified job

 You cannot alter application and environment settings as part of the Modify
 flow, but you can do so in the main masking application.
