## Managing Inventories

An inventory describes all of the data present in a particular data source and defines the methods which will be used to secure it. Inventories typically include the table or file name, column/field name, the data classification, and the chosen algorithm.

## The Inventory Screen

From anywhere within an environment, click the **Inventory** tab to see the Inventory Screen. This displays the inventory for the environment's rule sets.

## Inventory Settings

To specify your inventory settings:

1. On the left-hand side of the screen, select a **Rule Set** from the drop-down menu.
2. Below this, **Contents** lists all the tables or files defined for the rule set.

![](./media/inventory_settings.png)

3. Select a **table** or **file** for which you want to create or edit the inventory of sensitive data.
The **Columns** or **Fields** for that specific table or file appear.

4. If a column is a primary key (PK), Foreign Key (FK), or index (IDX), an icon indicating this will appear to the Right of the column name. If there is a note for the column, a Note icon will appear. To read the note, click the icon.
5. If an algorithm associated with a column is a custom algorithm (formerly known as Mapplet) then (**custom**) in red text will appear after the algorithm name.
6. If you selected a table, metadata for the column appears: **Data Type** and **Length** (in parentheses). This information is read-only.
7. Choose how you would like to view the inventory:

  - **All Fields** — Displays all columns in the table or all fields in the file (allowing you to mark new columns or fields to be masked).
  - **Masked Fields** — Filters the list to just those columns or fields that are already marked for masking.

8. Choose how to determine whether to mask/unmask a column:

 - **Auto** — The default value. The profiling job can determine or update the algorithm assigned to a column and whether to mask the column.
 - **User** — The user's choice overrides the profiling job. The user manually updates the algorithm assignment, mask/unmask option of the column. The Profiler will ignore the column, so it will not be updated as part of the Profiling job. In order to use the Secure Lookup algorithm, the user would select it as a user-defined algorithm and assign it to the specific column. Secure Lookup automates the creation of a secure lookup algorithm by building a list of replacement values based on the existing unique values in the target column and creating a secure lookup using those values. In that respect, it is simply shuffling the values.

## Managing a Database inventory

The following sections apply to databases.

### Setting Column Criteria for a Table

**Note:**
    You must select a database from the Select Rule Set drop-down menu on the left, not a file system.

To set criteria for sensitive columns:
1. Click the green edit icon to the right of a column's name.
2. To mask the selected column, select the **Mask** check box.

 - If you do not want to mask this column, clear this check box.

3. From the Domain drop-down menu, select the appropriate sensitive data element type for the column.
4. The Delphix masking engine defaults to a **Masking Algorithm** as specified in the Settings screen. If necessary, you can override the default algorithm for a column.

 - To select a different masking algorithm, choose one from the Algorithm dropdown.
 - To identify a custom algorithm, a text as custom in parenthesis will appear with the algorithm name.

For detailed descriptions of these algorithms, please see [Securing Sensitive Data  - Configuring Your Own Algorithms].

If you select a DATESHIFT algorithm and you are not masking a datetime or timestamp column, you must specify a **Date Format**. (This field only appears if you select a DATESHIFT algorithm from the Masking Algorithm dropdown.) For a list of acceptable formats, click the **Help** link for Date Format. The default format is yyyy-MM-dd.

1. Select the Row Type according to its purpose, using "All Row" as a convention for all rows.
 If you need to create a row type (for example, if filter conditions are required), see Row Types and Creating New Row Types for a Table next.
2. Select an ID Method:

 - **Auto** — The default value. The profiling job can determine or update whether to mask a column.
 - **User** — The user decides whether to mask/unmask a column. The user's choice overrides the profiling job. (The user masking is done after the profiling job is finished.)

3. You can add/remove notes in the **Notes** text field.
4. When you are finished, click **Save**.
 You must click Save for any edits to take effect.

### Creating a New Row Type

1. From an Environment's Inventory tab, click +Row Types in the upper right.
The **Row Type** window appears, listing existing row types.
2. Click **+ Add a Row Type**. The **Add Row Type** window appears.
3. Name the **Row Type** according to its purpose. For example, if you want to subset the rows to only take rows with addresses, you can name this row type "Address Rows".
4. To limit the masking to a subset of rows, specify an appropriate **Where Clause**.
5. Click **Save**.

## Managing a File Inventory

### Setting Field Criteria for a file

To set criteria for sensitive fields:

1. From an Environment's Inventory tab, click the green edit icon to the right of the field you want.
2. To mask this field, check the **Mask** check box (in the View Inventory pane).
3. Clear this check box if you do not want to mask this field.
4. Choose the appropriate sensitive data element type for the field from the **Domain** drop-down.
5. Delphix defaults to a masking **Algorithm** as specified in the Settings screen. If necessary, you may override the default algorithm for a field.
6. To select a different masking algorithm, choose one from the **Algorithm** drop-down.
7. Choose a **Record Type** from the drop-down.
8. Click **Save** when you are finished.

**Note:**
    You must click Save for any edits to take effect.

## Defining fields

To create new fields:
1. From an Environment's Inventory tab, click **Define fields** to the far right.
The Edit Fields window appears.

![](./media/define_fields.png)

2. Edit the fields as described in **Setting Field Criteria for a File**.
3. When you are finished, click **New** to create a new field, or click **Save** to update an existing field.

### Adding Record Types for files

To add a new Record Format:
1. In the upper right-hand corner of an environment's **Inventory** tab, click **Record Types**. The Record Type window appears.
2. Click **+Add a Record Type** towards the bottom of the window. The Add Record Type window appears.
3. Enter values for the following fields:

 - **Record Type Name** — A free-form name for this record format.
 - **Header/Body/Trailer** — If the file has header or trailer records, you will need to create file formats for them. Select the appropriate type. Delphix allows for masking of multiple headers, multiple trailers, and multiple types of body records.
 - **Record Type ID** — (optional) For body records, specify the value of the record type code or other identifier that allows Delphix to identify records that qualify as this record type.
 - **Position #** — (optional) Specify the field number (for delimited files) or the character position number (for fixed files) of the beginning of the Record Type Identifier within the data record.
 - **Length #** — (optional) For fixed files, specify the length of the Record Type Identifier within the data record.

4. Click **Save** when you are finished.

## Redefine Conditions

For Mainframe files, the inventory also allows for the entry of Redefine Conditions, which are used to handle any occurrences of COBOL's REDEFINES construct that might appear in the Copybook. In COBOL, the REDEFINES keyword allows an area of a record to be interpreted in multiple different ways. In the example below, for instance, each record can hold either the details of a person (PERSON-DET) or the details of a company (COMP-DET).

![](./media/redefine.png)

Depending on which group is present, different masking algorithms may need to be applied. Below is the inventory corresponding to this copybook, which allows algorithms to be selected separately for each group.

![](./media/inventory.png)

In order to do any masking however, the masking engine must be able to determine, for each record, which fields should be read, so that the correct algorithms can be applied. In order to do this, the masking engine uses Redefine Conditions, which are specified in the inventory. Redefine Conditions are boolean expressions which can reference any fields in the record when they are evaluated.

In the example copybook above, the field CUST-TYPE is used to indicate which group is present. If CUST-TYPE holds a 'P', a PERSON-DET group is present, and if it holds a 'C', COMP-DET is present. This can be expressed in the inventory by specifying a Redefine Condition with the value [CUST-TYPE]='P' . This expression indicates that, for each record read from the source file during the masking job, the value of the field CUST-TYPE should be read and compared against the string 'P'. If it is equal, the masking engine will read from the record the fields subordinate to PERSON-DET, and will apply any masking algorithms specified on those fields. Similarly, a Redefine Condition with the value [CUST-TYPE]='C' should be applied to the COMP-DET field.
Exactly one of the conditions should evaluate to 'true' for each group of redefined fields. For example, a copybook might have fields A, B REDEFINES A, and C REDEFINES A. Of the Redefine Conditions attached to A, B, and C, one and only one should evaluate to true for each record.

### Entering a Redefine Condition

1. Click on the orange **REDEFINED** or **REDEF** button next to the redefined or redefining field
2. Enter a condition in the dialog box which appears. This is the expression, which, when it evaluates to true, causes the subordinate fields to be read and, if they have algorithms assigned, masked.

![](./media/editprops.png)

3. Click **Submit**.

### Format of Redefine Conditions


Redefine Conditions allow fields to be compared against either number or string literals. Square brackets enclosing a field name indicate a variable, which takes on the value of the named field:

```
[Field1] = 'An example String'
```

String literals can be enclosed in either single or double quotes. For fields that are numeric (e.g. PIC S99V9), the operators <, <=, >, and >= can be used in addition to the =operator, e.g.

```
[Field2] <= -10.5
```
Also, conditions can be joined using AND, OR, and NOT to form more complex conditions:

```
([Field3] > 2.5 AND [Field3] < 10) OR NOT [FIELD4] = 'Z'
```

## Importing and Exporting an Inventory


**To export an inventory**:
1. Click the **Export** icon at the upper right. The Export Inventory popup appears with the name of the currently selected Rule Set as the Inventory Name and a corresponding .csv **File Name**.
2. Click **Save**.

A status popup appears. When the export operation is complete, you can click on the **Download file** name to access the inventory file

**To import an inventory**:

1. In the upper right-hand corner, click the **Import** icon. The Import Inventory popup appears.
2. Click **Select** to browse for the name of a comma-separated (.csv) file.
3. Click **Save**.

The inventory you imported appears in the Rule Set list for this environment.

!!! info

The format of an imported.csv file must exactly match the format of the exported inventory. If you plan to import an inventory, before importing the inventory, you should export it and then update the exported file as needed before you import it.
