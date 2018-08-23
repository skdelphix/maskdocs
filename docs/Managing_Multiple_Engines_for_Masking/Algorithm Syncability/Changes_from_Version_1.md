## New Syncable Objects

We have the following new syncable objects added in 5.3. Refer to the
main documentation for more information on what they are, and how to use
them.

  - DATABASE_CONNECTOR
  - DATABASE_RULESET
  - DATE_SHIFT
  - DOMAIN
  - FILE_CONNECTOR
  - FILE_FORMAT
  - FILE_RULESET
  - GLOBAL_OBJECT
  - MASKING_JOB

## Key per Algorithm

In pre-5.3, a global key for the engine was used by all algorithms that
required a seed to determine the outcome of masked values. This included
algorithms such as Lookup and Binary Lookup. Thus, in 5.2, exporting a
Lookup Algorithm would automatically export the global encryption key as
a dependency. In this release, we allow each algorithm to have its own
independent key, exported as a part of the algorithm. Refer to the **Key
Management** section for more detail.

## Changed Model of Import Status Reporting

In pre-Krypton, the import status looked like this:

``` json
{
"objectIdentifier": {
"keyId": "global"
},
"objectType": "KEY",
"importStatus": "SUCCESS"
}
```

Starting in Krypton, the import status of an object has extended to
include the id or name it has imported into to reduce any confusion
introduced with IntegerIdentifiers. For more information on the reason
for this change, refer to Logic Behind Overwrite of IntegerIdentifier
and StringIdentifier. For examples on what it now looks like, refer to
the **Example User Workflow** page.

## Changed Granularity of Transactions for Import

Starting in Krypton, an import of however many objects becomes an atomic
execution rather a per-object basic atomicity. This means that the
execution will either succeed or fail in importing all objects or none
at all. Refer to the Error Handling of Import logic flow diagram for
more information.

## Filter for /syncable-objects

Now that we have a large list of syncable objects, we have added a new
feature for filtering based on the object type. Refer to the
**Endpoint** section in the main documentation and the **Example User
Workflow** page for more information.

## Async Endpoints

Exporting a large MASKING\_JOB with many dependencies can potentially
take a long time. So we have decided to provide a new endpoint that
exports and imports the objects asynchronously. Refer to the
**Endpoint** section in the main documentation and the **Example User
Workflow** page for more information.
