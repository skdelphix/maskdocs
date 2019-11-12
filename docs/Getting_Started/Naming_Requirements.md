# Naming Requirements

This section describes the naming equirements for Masking Engine objects
which are allowed to be created / renamed manually.

##Affected configurable objects
  
| configurable objects |
| ----------- |
| algorithm |
| application |
| connector |
| domain |
| environment |
| file format |
| job |
| profiling group |
| record type |
| role |
| rule set |
| scheduled job |
| search expression |

For all of the above:

 - Leading/trailing white space is not allowed

 - The following special characters are not allowed:

| Symbol | Name |
| --------- | --------- |
| [ | open bracket |
| ] | close bracket |
| ( | open parenthesis |
| ) | close parenthesis |
| { | open brace |
| } | close brace |
| ~ | tilde |
| ! | exclamation  mark |
| @ | at |
| # | pound |
| $ | dollar |
| % | percent |
| ^ | carat |
| * | asterisk |
| " | quote |
| ? | question mark |
| : | colon |
| ; | semi-colon |
| , | comma |
| / | forward slash |
| \ | back slash |
| \\\ | double back slash |
| ` | back quote |
| + | plus |
| = | equal |
| < | less than |
| > | greater than |
| ' | single quote |
| \| | pipe |


##Upgrade
During an upgrade of a Masking Engine to a 6.0 or later release, a name with leading or trailing white space will be automatically trimmed, and a counter value might be appended to the end of the name to prevent a naming conflict. For example:

 | pre-upgrade name | post-upgrade name | upgrade change |
 | ---------- | --------- | --------- |
 | "alg_SecureLookup" | "alg_SecureLookup" | no change |
 | " alg_SecureLookup" | "alg_SecureLookup1" | leading white space trimmed and counter value appended |
 | "alg_SecureLookup " | "alg_SecureLookup2" | trailing white space trimmed and counter value appended |
 
 If any name from the above mentioned "configurable entities" table has a restricted special character - an upgrade will fail with the corresponding error message.
 
##Create / Rename  
If an attempt is made to create a new entity (or to modify the name of the existing one) with leading or trailing white space or any of the special characters listed above, the operation will fail on a 6.0 or later release with a corresponding error message.
 
##Environment [Export](/Connecting_Data_to_Masking_Service/Managing_Environments/#exporting-an-environment) - [Import](/Connecting_Data_to_Masking_Service/Managing_Environments/#importing-an-environment)
 If any entity name exported from a pre-6.0 version contains leading or trailing white spaces or the special characters listed above, the import operation will fail on a 6.0 or later release with a corresponding error message.

##Sync
 If a sync bundle from a pre-6.0 version contains leading or trailing white space or any of the special characters listed above, then the Sync import operation will fail on a 6.0 or later release, with a corresponding error message.
