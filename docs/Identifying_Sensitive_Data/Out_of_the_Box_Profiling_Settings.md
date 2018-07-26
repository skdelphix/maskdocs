# Out of the Box Profiling Settings

The Delphix Platform comes out of the box with over 50 profile
expressions to help you discover over 30 types (account numbers,
addresses, etc.) of sensitive data.

## Account Numbers

An account number is the primary identifier for ownership of an account,
whether a vendor account, a checking or brokerage account, or a loan
account. An account number is used whether or not the identifier uses
letters or numbers. Below are the profile expressions Delphix uses to
identify account numbers:

| **Expression Name**| **Domain** | **Expression Level**|**Expression**|
| --- |--- | --- | --- |
| Account Number| ACCOUNT_NO | Column| `(?>(acc(oun\|n)?t)_?(num(ber)?\|nbrjno)?)(?!\w\*(ID\|type))` |
                                                     
## Physical Addresses 

Below are the profile expressions Delphix uses to identify physical
addresses:

| **Expression Name** |  **Domain** | **Expression Level**| **Expression** |
| ---| --- | --- | --- |
| Address                | ADDRESS       | Column |`^(?:(?!postalcode\|city\|state\|country\|email\|(l\|ln\|lin\|line)?_?2{1}\|ID).)*addre?s?s?_?(?:(?!city\|state\|country\|email|(l\|ln\|lin\|line)?_?2{1}\|ID).)*$`|
| Street Address         | ADDRESS       | Column | `(?>(str(eet)?_?addre?s?s?\|street))(?!\w*(ID\|type))`|
| Data - Address         | ADDRESS       | Data | `(.*[\s]+b(ou)?|(e)?v(ar)?d[\d]*.*)\|(.*[\s]+st[.]?(reet)?[\s]*.*)\|(.*[\s]+ave[.]?(nue)?[\s]*.*)\|(.*[\s]+r(oa)?d[\s]*.*)\|(.*[\s]+\|(a)?n(e)?[\s]*.*)\|(.[\s]+cir(cle)?[\s]*.*1`|
| Address Line2 - before | ADDRESS_LINE2 | Column | `^(?:(?!email\|ID).)*(l\|ln\|lin\|line)?2{1}_?addre?s?s?(?:(?!email\|ID).)*$`|
| Address Line2 - after  | ADDRESS_LINE2 | Column  | `^(?:(?!email\|ID).)*addre?s?s?_?(l\|ln\|lin\|line)?_?2{1}(?:(?!email\|ID).)*$`|
| Data - Address Line 2  | ADDRESS_LINE2 | Data | `(.*[\s]*ap(ar)?t(ment)?[\s]+.*)|(.*[\s]*s(ui)?te[\s]+.*)\|(c(are)?[\s]*[\\\\]?[/]?o(f)?[\s]+.*)`|

## Beneficiary ID 

Below are the profile expressions Delphix uses to identify beneficiary
IDs:

| **Expression Name**|   **Domain**| **Expression Level** | **Expression**|
| ---| --- | --- | --- |
| Beneficiary Number| BENEFICIARY_NO| Column | `(?>(bene(ficiary)?)_?(num(ber)?|nbr\|no))(?!\w*ID)1  |
| Beneficiary ID | BENEFICIARY_NO| Column | `(?>(bene(ficiary)?)_?id)` |                                                                                                       |


## Biometrics 

Below are the profile expressions Delphix uses to biometric data:

| **Expression Name** |   **Domain**| **Expression Level** | **Expression** |
| ---| ---| --- | --- |
| Biometric | BIOMETRIC | Column  | biometric  |                                                                                                       |


## Certificate ID 

Below are the profile expressions Delphix uses to identify certificate
IDs:

| **Expression Name** | **Domain** | **Expression Level** | **Expression** |
| ---| --- | --- | --- |
| Certificate Number | CERTIFICATE_NO  | Column | `(?>cert(ificate)?_?(num(ber)?\|nbr\|no\|id))`|
| Certificate ID | CERTIFICATE_NO  | Column | `(?>cert(ificate)?_?id)` |                                                                                                       |


## City 

Below are the profile expressions Delphix uses to identify cities:

| **Expression Name** | **Domain** | **Expression Level** | **Expression**|
| ----| --- | --- | --- |
| City | CITY  | Column  | `ci?ty(?!\w*ID)` |


## Country 

Below are the profile expressions Delphix uses to identify countries:

| **Expression Name** | **Domain** | **Expression Level** | **Expression** |
| ---| --- | --- | --- |
| Country   | COUNTRY  | Column | `c(ou)?nty(?!\w*ID)`|


## Credit Card 

Below are the profile expressions Delphix uses to identify credit cards:

| **Expression Name** | **Domain** | **Expression Level**|  **Expression**|
| ---| --- | --- | --- |
| Card Number  | CREDIT CARD | Column  | `(?>ca?rd_?(num(ber)?\|nbr\|no)?)(?!\w*ID)`|
| Credit Card Number | CREDIT CARD | Column  | `(?>cre?di?t_?(ca?rd)?_?(num(ber)?\|nbr\|no)?)(?!\w*ID)`|
| Data - Credit Card | CREDIT CARD  | Data | `^(?:3[47][0-9]{13}|4[0-9]{12}(?:[0-9]{3})?(?:[0-9]{3})?\|(?:5[1-5][0-9]{2}\|222[1-9]\|22[3-9][0-9]\|2[3-6][0-9]{2}\|27[01][0-9]\|2720)[0-9]{12}\|6(?:(011\|5[0-9][0-9])[0-9]{2}\|4[4-9][0-9]{3}\|2212[6-9]\|221[3-9][0-9]\|22[2-8][0-9]{2}\|229[0-1][0-9]|2292[0-5])[0-9]{10}?(?:[0-9]{3})?\|3(?:0[0-5,9]\|6[0-9])[0-9]{11}\|3[89][0-9]{14}?(?:[0-9]{1,3})?)$`|
                                                                                               

## Customer Number

Below are the profile expressions Delphix uses to identify customer IDs:

| **Expression Name**|   **Domain** | **Expression Level** | **Expression**|
| --- | --- | --- | --- |
| Customer Number| CUSTOMER_NUM | Column| `(?>(cu?st(omer\|mr)?)_?(num(ber)?\|nbr|no)?)(?!\w*ID)`|


## Date of Birth

Below are the profile expressions Delphix uses to identify dates of
birth:

| **Expression Name**| **Domain** | **Expression Level**|  **Expression**|
| ---| --- | --- | --- |
| Birth Date | DOB | Column |`(?>(bi?rth)_?(date?\|day\|dt))(?!\w*ID)` |
| Birth Date1 | DOB | Column `(?>dob\|dtofb\|(day\|date?\|dt)_?(of)?_?(bi?rth))(?!\w*ID)`|
| Birth Date2 | DOB | Column|`(?>b_?(date?\|day))(?!\w*ID)`|
| Admission Date| DOB | Column  |`(?>(adm(it\|ission)?)_?(date?\|day\|dt))(?!\w*ID)`|
| Treatment Date | DOB | Column |`(?>(tr(ea)?t(ment)?)_?(date?\|day|dt))(?!\w*ID)`|
| Discharge Date | DOB| Column |`(?>(ds\|disc(h\|harge)?)_?(date?\|day\|dt))(?!\w*ID)`|


## Driver License Number

Below are the profile expressions Delphix uses to identify driver
license numbers:

| **Expression Name** | **Domain** | **Expression Level** | **Expression** |
| --- | --- | --- | --- |
| Drivers License Number  | DRIVING_LC | Column | `(?>(dri?v(e?rs?e?)?)_?(license|li?c)?_?(num(ber)?\|nbr|no)?)(?!\w*ID)` |
| Drivers License Number1 | DRIVING_LC | Column | `(^license$\|(license\|li?c)_?(num(ber)?\|nbr\|no))(?!\w*ID)` |   


## Email

Below are the profile expressions Delphix uses to identify emails:

| **Expression Name** | **Domain** | **Expression Level** | **Expression** |
| --- | --- | ---  | ---|
| Email  | EMAIL  | Column  | `^(?:(?!invalid).)*email(?!\w*ID)`|
| Data - Email | EMAIL | Column | `\b[A-Z0-9._%+-]+@[A-Z0-9.-]+\.[A-Z]{2,6}\b`|   


## First Name

Below are the profile expressions Delphix uses to identify first names:

| **Expression Name**      |   **Domain**    | **Expression Level** |        **Expression**                      |
| ------------------------ | -------------   | -------------------  | ------------------------------------------ |
| First Name               | FIRST_NAME      | Column               | (?>(fi?rst)_?(na?me?)|f_?name)(?!\w*ID)    |
| Middle Name              | FIRST_NAME      | Column               | (?>(mid(dle)?)_?(na?me?)|m_?name)(?!\w*ID) |   


## IP Address

Below are the profile expressions Delphix uses to IP addresses:

| **Expression Name**      |   **Domain**    | **Expression Level** |                                      **Expression**                                                         |
| ------------------------ | -------------   | -------------------  | ----------------------------------------------------------------------------------------------------------- |
| IP Address               | IP ADDRESS      | Column               | (?>(ip_?addre?s?s?))(?!\w*(ID|type))                                                                        |
| Data - IP Address        | IP ADDRESS      | Data                 | \b(?:(?:25[0-5]|2[0-4][0-9]|1[0-9][0-9]|[1-9]?[0-9])\.){3}(?:25[0-5]|2[0-4][0-9]|1[0-9][0-9]|[1-9]?[0-9])\b |  |   


## Last Name

Below are the profile expressions Delphix uses to identify last names:

| **Expression Name**      |   **Domain**    | **Expression Level** |                          **Expression**                                 |
| ------------------------ | -------------   | -------------------  | ----------------------------------------------------------------------- |
| Last Name                | LAST_NAME       | Column               | ^(?:(?!portal|ID).)*((la?st)_?(na?me?)|l_?name)(?:(?!portalname|ID).)*$ |
   

## Plate Number 

Below are the profile expressions Delphix uses to identify plate
numbers:

| **Expression Name**      |   **Domain**    | **Expression Level** |                                  **Expression**                                                   |
| ------------------------ | -------------   | -------------------  | ------------------------------------------------------------------------------------------------- |
| License Plate            | PLATE_NO        | Column               | ^(?:(?!template|ID|type).)*(license|li?c)?_?plate_?(num(ber)?|nbr|no)?(?:(?!template|ID|type).)*$ |   |
  

## PO Box Numbers

Below are the profile expressions Delphix uses to identify PO box
numbers:

| **Expression Name**      |   **Domain**    | **Expression Level** |   **Expression**    |
| ------------------------ | -------------   | -------------------  | ------------------- |
| PO Box                   | PO_BOX          | Column               | po_?box             |
| Data - PO Box            | PO_BOX          | Data                 | po box|p\.o\        |  


## Precinct

Below are the profile expressions Delphix uses to identify precincts:

| **Expression Name**      |   **Domain**    | **Expression Level** |       **Expression**         |
| ------------------------ | -------------   | -------------------  | ---------------------------- |
| Precinct                 | PRECINCT        | Column               | (>?precinct|prcnct)(?!\w*ID) |


## Record Number

Below are the profile expressions Delphix uses to identify record
numbers:

| **Expression Name**      |   **Domain**    | **Expression Level** |             **Expression**                        |
| ------------------------ | -------------   | -------------------  | ------------------------------------------------- |
| Record Number            | RECORD_NO       | Column               | (?>rec(ord)?_?(num(ber)?|nbr|no))(?!\w*(ID|type)) |


## School Name

Below are the profile expressions Delphix uses to identify school names:

| **Expression Name**      |   **Domain**    | **Expression Level** |       **Expression**        |
| ------------------------ | -------------   | -------------------  | --------------------------- |
| School Name              | SCHOOL_NM       | Column               | (?>school_?na?me?)(?!\w*ID) |


## Security Code

Below are the profile expressions Delphix uses to identify security
codes:

| **Expression Name**      |   **Domain**    | **Expression Level** |       **Expression**                  |
| ------------------------ | -------------   | -------------------  | ------------------------------------- |
| Security Code            | SECURITY_CODE   | Column               | (?>se?cu?r(i?ty?)?_?co?de?)(?!\w*ID)  |


## Serial Number

Below are the profile expressions Delphix uses to identify serial
numbers:

| **Expression Name**      |   **Domain**    | **Expression Level** |         **Expression**                       |
| ------------------------ | -------------   | -------------------  | -------------------------------------------- |
| Serial Number            | SERIAL_NM       | Column               | (?>(ser(ial)?)_?(num(ber)?|nbr|no))(?!\w*ID) |


## Signature

Below are the profile expressions Delphix uses to identify signatures:

| **Expression Name**      |   **Domain**    | **Expression Level** |     **Expression**          |
| ------------------------ | -------------   | -------------------  | --------------------------- |
| Signature                | SIGNATURE       | Column               | signature(?!\w*(ID|type))   |


## Social Security Number

Below are the profile expressions Delphix uses to social security
numbers:

| **Expression Name**      |   **Domain**    | **Expression Level** |             **Expression**                                   |
| ------------------------ | -------------   | -------------------  | ------------------------------------------------------------ |
| Social Security Numbeer  | SSN             | Column               | ssn(?!\w*ID)                                                 |
| Data - SSN               | SSN             | Data                 | \b(?!000)(?!666)[0-8]\d{2}[- ](?!00)\d{2}[- ](?!0000)\d{4}\b |  


## Tax ID

Below are the profile expressions Delphix uses to identify tax IDs:

| **Expression Name**      |   **Domain**    | **Expression Level** |                       **Expression**                |
| ------------------------ | -------------   | -------------------  | --------------------------------------------------- |
| Tax ID Number            | TAX_ID          | Column               | tin$|^tin|_tin|tin_                                 |
| Tax ID Code or Number    | TAX_ID          | Column               | (ta?x)_?(id(ent)?)?_?((co?de?)|(num(ber)?|nbr|no))? |  


## Telephone Number

Below are the profile expressions Delphix uses to identify telephone
numbers:

| **Expression Name**        |   **Domain**    | **Expression Level** |                       **Expression**                                    |
| -------------------------- | -------------   | -------------------  | ----------------------------------------------------------------------- |
| Telphone or Contact Number | TELEPHONE_NO    | Column               | (?>((tele?)?phone)|(co?nta?ct|tel)_?(num(ber)?|nbr|no))(?!\w*(ID|type)) |
| Data - Phone Number        | TELEPHONE_NO    | Data                 | \(?\b[0-9]{3}\)?[-. ]?[0-9]{3}[-. ]?[0-9]{4}\b                          | 
| Fax Number                 | TELEPHONE_NO    |  Data                | (?>fax_?(num(ber)?|nbr|no)?)(?!\w*(ID|type))                            |


## Vin Number

Below are the profile expressions Delphix uses to identify vin numbers:

| **Expression Name**      |   **Domain**    | **Expression Level** |    **Expression**    |
| ------------------------ | -------------   | -------------------  | -------------------- |
| Vehicle                  | VIN_NO          | Column               | vehicle              |
| VIN                      | VIN_NO          | Column               | vin$|^vin|_vin|vin_  |   


## Web Address

Below are the profile expressions Delphix uses to identify web
addresses:

| **Expression Name**      |   **Domain**    | **Expression Level** |                                **Expression**                                           |
| ------------------------ | -------------   | -------------------  | --------------------------------------------------------------------------------------- |
| Web or URL Address       | WEB             | Column               | (?>(url|web_?addre?s?s?))(?!\w*(ID|type))                                               |
| Data - Web Address       | WEB             | Data                 | \b(?:(?:https?|ftp|file)://|www\.|ftp\.)[-A-Z0-9+&-@#/%=~_|$?!:,.]*[A-Z0-9+&-@#/%=~_|$] |   


## ZIP Code

Below are the profile expressions Delphix uses to identify zip codes:

| **Expression Name**      |   **Domain**    | **Expression Level** |        **Expression**                       |
| ------------------------ | -------------   | -------------------  | ------------------------------------------- |
| zip or Postal Code       | ZIP             | Column               | (?>(zip|post(al)?)_?((co?de?)?4?))(?!\w*ID) |
| Data - Zip Code          | ZIP             | Data                 | \b([0-9]{5})-([0-9]{4})\b                   |   

 
