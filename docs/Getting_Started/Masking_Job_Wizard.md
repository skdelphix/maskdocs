Delphix Maskings Job Wizard  enables users to create and modify masking jobs. 
While the wizard facilitates a number of workflows and operations, more
advanced functionality and a finer control of features is available directly
in the masking application. The Job Wizard currently functions only with certain
data platforms, but these constraints do not apply when working directly in the
masking application.

# Supported Data Platforms
The following data platforms are currently supported from within the Job Wizard:
 - Oracle Database
 - RDS Oracle Database
 - MSSQL Server Database
 - Sybase Database

This restricted list only affects your use of the wizard; an expanded number of
platforms are supported directly in the masking application. Some operations
within the Job Wizard are also limited. See below for details.

# Supported Operations
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
    Operations marked with an asterisk are limited in the Job Wizard but fully supported in the main application. |

# What is Not Supported in the Wizard
The following data platforms and operations are not supported in the Job Wizard.
To access additional functionality, use the main masking application.

## Unsupported Data Types
The following data types are supported when using the main masking application
but are not currently supported in the Job Wizard:

- DB2 Database
- PostgreSQL Database
- Generic Database
- Delimited File
- Excel Sheet File
- Fixed File
- Mainframe - VSAM File
- XML File

## Unsupported Operations
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

# Opening the Masking Job Wizard
When you first login to masking, the welcome screen offers a link to learn more
or begin masking immediately. To open the Job Wizard, click Run on the welcome
page.

!(./images/welcome.png)
