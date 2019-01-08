The following tables specify which algorithms are syncable between
masking engines (in addition to the masking engine key).

!!! note
    Only users with masking admin privilege are able to export and import algorithms.

## User-defined Algorithms

| **Type**                 | **Syncable** | **Workaround**                                        |
| ------------------------ | ------------ | ----------------------------------------------------- |
| Lookup                   | Yes          | NA                                                    |
| Binary Lookup            | Yes          | NA                                                    |
| Segmented Mapping        | Yes          | NA                                                    |
| Mapping                  | No           | None                                                  |
| Tokenization             | Yes          | NA                                                    |
| Minmax                   | Yes          | NA                                                    |
| Cleansing                | Yes          | NA                                                    |
| Free Text Redaction      | Yes          | NA                                                    |
| Custom Algorithm/Mapplet | Yes          | NA (see “Custom Algorithm Syncability Guide” section) |

## Built-In Algorithms

Note that syncing built-in algorithms do not actually import the
files associated with them but just updates their individual keys if they
have them.

While some of the built in algorithms are not synchronizable, mainly due
to them being non-deterministic, we still can support export of
inventories that contain any built in algorithm. We just do not
guarantee consistent masking of those non-synchronizable built in
algorithms between engines.

| **Algorithm API Name**    | **Algorithm UI Name**     | **Type**     | **Syncable** | **Workaround**       |
| ------------------------- | ------------------------- | ------------ | ------------ | -------------------- |
| AccNoLookup               | ACCOUNT SL                | lookup       | Yes          | NA                   |
| AccountTK                 | ACCOUNT\_TK               | tokenization | Yes          | NA                   |
| AddrLine2Lookup           | ADDRESS LINE 2 SL         | lookup       | Yes          | NA                   |
| AddrLookup                | ADDRESS LINE SL           | lookup       | Yes          | NA                   |
| BusinessLegalEntityLookup | BUSINESS LEGAL ENTITY SL  | lookup       | Yes          | NA                   |
| CommentLookup             | COMMENT SL                | lookup       | Yes          | NA                   |
| CreditCard                | CREDIT CARD               | calculated   | No           | None                 |
| DateShiftDiscrete         | DATE SHIFT(DISCRETE)      | calculated   | Yes          | NA                   |
| DateShiftFixed            | DATE SHIFT(FIXED)         | calculated   | No           | Already synchronized |
| DateShiftVariable         | DATE SHIFT(VARIABLE)      | calculated   | No           | None                 |
| DrivingLicenseNoLookup    | DR LICENSE SL             | lookup       | Yes          | NA                   |
| DummyHospitalNameLookup   | DUMMY\_HOSPITAL\_NAME\_SL | lookup       | Yes          | NA                   |
| EmailLookup               | EMAIL SL                  | lookup       | Yes          | NA                   |
| FirstNameLookup           | FIRST NAME SL             | lookup       | Yes          | NA                   |
| FullNMLookup              | FULL\_NM\_SL              | lookup       | Yes          | NA                   |
| LastNameLookup            | LAST NAME SL              | lookup       | Yes          | NA                   |
| LastCommaFirstLookup      | LAST\_COMMA\_FIRST\_SL    | lookup       | Yes          | NA                   |
| NameTK                    | NAME\_TK                  | tokenization | Yes          | NA                   |
| NullValueLookup           | NULL SL                   | lookup       | Yes          | NA                   |
| TelephoneNoLookup         | PHONE SL                  | lookup       | Yes          | NA                   |
| RandomValueLookup         | RANDOM\_VALUE\_SL         | lookup       | Yes          | NA                   |
| SchoolNameLookup          | SCHOOL NAME SL            | lookup       | Yes          | NA                   |
| SecureShuffle             | SECURE SHUFFLE            | calculated   | No           | None                 |
| SsnTK                     | SSN\_TK                   | tokenization | Yes          | NA                   |
| USCountiesLookup          | US\_COUNTIES\_SL          | lookup       | Yes          | NA                   |
| USCitiesLookup            | USCITIES\_SL              | lookup       | Yes          | NA                   |
| USstatecodesLookup        | USSTATE\_CODES\_SL        | lookup       | Yes          | NA                   |
| USstatesLookup            | USSTATES\_SL              | lookup       | Yes          | NA                   |
| WebURLsLookup             | WEB\_URLS\_SL             | lookup       | Yes          | NA                   |
| RepeatFirstDigit          | ZIP+4                     | calculated   | No           | Already synchronized |
