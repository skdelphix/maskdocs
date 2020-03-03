# Change Log

## Changes in 6.0

### New Syncable Objects

We added the following new syncable objects in 6.0. Refer to the
main documentation for more information on what they are, and how to use
them.

- 6.0.0.0 Release
    - MOUNT_INFORMATION
- 6.0.1.0 Release
    - JDBC_DRIVER
    - REIDENTIFICATION_JOB
    - TOKENIZATION_JOB

## Changes in 5.3

### New Syncable Objects

We added the following new syncable objects in 5.3. Refer to the
main documentation for more information on what they are, and how to use
them.

- 5.3.0.0 Release
    - DATABASE_RULESET
    - DATE_SHIFT
    - DOMAIN
    - FILE_CONNECTOR
    - FILE_FORMAT
    - FILE_RULESET
    - GLOBAL_OBJECT
    - MASKING_JOB
- 5.3.3.0 Release
    - PROFILE_EXPRESSION
    - PROFILE_JOB
    - PROFILE_SET

We also added the following new syncable algorithms in 5.3.

- 5.3.2.0 Release
    - CLEANSING
    - MIN_MAX
- 5.3.3.0 Release
    - REDACTION

### Key per Algorithm

In pre-5.3, a global key for the engine was used by all algorithms that
required a seed to determine the outcome of masked values. This included
algorithms such as Lookup and Binary Lookup. Thus, in 5.2, exporting a
Lookup Algorithm would automatically export the global encryption key as
a dependency. In this release, we allow each algorithm to have its own
independent key, exported as a part of the algorithm. Refer to the [Key
Management](Key_Management) section for more detail.

### Changed Model of Import Status Reporting

In 5.2, the import status looked like this:

``` json
{
"objectIdentifier": {
"keyId": "global"
},
"objectType": "KEY",
"importStatus": "SUCCESS"
}
```

Starting in 5.3.0, the import status of an object has extended to
include the id or name it has imported into to reduce any confusion
introduced with IntegerIdentifiers. For more information on the reason
for this change, refer to Logic Behind Overwrite of IntegerIdentifier
and StringIdentifier. For examples on what it now looks like, refer to
the [Example User Workflow](Example_User_Workflow) section.

### Changed Granularity of Transactions for Import

Starting in 5.3, an import of however many objects is performed as an atomic
execution rather than using per-object atomicity. This means that the
execution will either succeed at importing all objects or fail and import none
at all. Refer to the Error Handling of Import logic flow diagram for
more information.

### Filter for /syncable-objects

Now that we have a large list of syncable objects, we have added a new
feature for filtering based on the object type. Refer to the
[Endpoints](Endpoints) page and the [Example User
Workflow](Example_User_Workflow) section for more information.

### Async Endpoints

Exporting a large MASKING\_JOB with many dependencies can potentially
take a long time. So we have decided to provide a new endpoint that
exports and imports the objects asynchronously. Refer to the
[Endpoints](Endpoints) section in the main documentation and the [Example User
Workflow](Example_User_Workflow) page for more information.
