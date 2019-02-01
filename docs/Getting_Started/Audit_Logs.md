
# Audit Logs

Delphix helps you keep a record of user actions taken in the UI or directly through our REST APIs. You can access these audit logs directly from our UI or through our APIs.

## Audit Log UI Page

The Audit Log page can be found in the UI under the Audit tab. This page contains information on what action occurred, the user that performed the action and the time at which the action occurred. It also provides the ability to filter based on:

  - user
  - time range
  - arbitrary search string
  - action type or action target, or both (create, connector or create database
     connector)

## Audit Log APIs

With 5.3.2.0, Delphix introduced an endpoint to get all Audit Logs. This endpoint contains the user name, action type, target, status, start time, and end time.
For more information please refer to [API documentation](https://maskingdocs.delphix.com/Delphix_Masking_APIs/Masking_Client/Masking_API_Client/).

## What Gets Logged?

User actions are categorized into the following:

|    |  |  |    | |  |   |
| ------------- | --------   | ---------- | ---------  | ---------- | -------  | ----------    |
| Cancel        | Create     | Delete     | Edit       | Export     | Get      | Get All       |
| Import        | Lock       | Login      | Logout     | Run        | Test     | Unlock        |


The objects that user actions target are categorized into the following:

|    |       |     |           |  |         |       |
| ------   | ------  | ---     | -------      | -----     |----     | ---- |
| Algorithm | Analytics | Application | Application Log | Async Task | Audit Log |   |
| Column Metadata   | Database Connector | Ruleset Connector           | Database Ruleset                 |  Domain                  | Encryption Key             | Environment               |   
| Execution         | File Connector     | File Download               | File Field Metadata              | File Format              | File Metadata              | File Ruleset              |
| File Upload       | LDAP               | Mainframe Dataset Connector | Mainframe Dataset Field Metadata | Mainframe Dataset Format | Mainframe Dataset Metadata | Mainframe Dataset Ruleset |
| Masking Job       | Profile Expression | Profile Job                 | Profile Set                      | Re Identification Job    | Role                       | SSH Key                   |
| SSO               | Syncable Object    | System Information          | Table Metadata                   | Tokenization             | User       |     |

## Retention Policy

The default policy stores the last one million Audit Log entries. Any entries older than the most recent million are removed daily. Additionally, there is a fail-safe mechanism that prevents an attacker from forcing an unbounded number of actions to be logged to overload the system's disk space. In the event that such an attack occurs, Delphix also logs it to the application logs.

## Recommendation

If a full record of all Audit Log entries is desired, Delphix recommends using the new API to periodically retrieve new entries from the Audit Logs.
