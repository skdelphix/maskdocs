# Delphix Masking Terminology

Before getting started with the Delphix Masking Engine, an overview of
universal terms and concepts will build and unify how different masking
components come together. The following provides a brief overview of the
key concepts within the masking service.

## High Level Concepts

These concepts are the high level concepts users run into.

<table>
<thead>
<tr class="header">
<th><strong>Term</strong></th>
<th><strong>Definition</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Application</td>
<td>An Application is a tag that is assigned to one or more environments. We recommend using an application name that is the same as the application associated with the environments.</td>
</tr>
<tr class="even">
<td>Connector</td>
<td>Connectors are any set of data (database, file, etc) that have been connected to the Delphix Data Platform. These data sources can be physical or virtualized data sources.</td>
</tr>
<tr class="odd">
<td>Domain</td>
<td>A domain represents a correlation between various sensitive data categories (social security numbers) and the way it should be secured.</td>
</tr>
<tr class="even">
<td>Environment</td>
<td>An environment is a construct that can be used to describe a collection of masking jobs associated with a group of data sources.</td>
</tr>
<tr class="odd">
<td>In-place</td>
<td>In-place masking is 1 of 2 procedures that can be used to apply masking algorithms to a data source. By choosing the In-place option, Delphix will read data from the data source, secure the data in the Engine and then update the data source with the secure data.</td>
</tr>
<tr class="even">
<td>On-the-fly</td>
<td>On-the-fly masking is the second procedure that can be used to apply masking algorithms to a data source. By choosing the On-the-fly option, Delphix will read data from the data source, secure the data in the Engine and then place the secure data in a target source (different from the location of the original data source).</td>
</tr>
<tr class="odd">
<td>Inventory</td>
<td>An inventory describes all of the data present in a particular data source and defines the methods which will be used to secure it. Inventories typically include the table name, column name, the data classification, and the chosen algorithm.</td>
</tr>
<tr class="even">
<td>Profile</td>
<td><p>Profiling uses a variety of different methods to classify data in a data source into different categories. These categories are known as domains.</p>
<p>The profile process also assigns recommended algorithms for securing the data based on the the domain.</p></td>
</tr>
<tr class="odd">
<td>Ruleset</td>
<td>A rule set is group of tables or flat files within a particular data source that a user may choose to run profile, masking, or tokenization jobs on.</td>
</tr>
</tbody>
</table>

## Masking Algorithms

The following terminology is around the different Algorithms that users
may use to secure their data.

<table>
<thead>
<tr class="header">
<th><strong>Term</strong></th>
<th><strong>Definition</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Secure Lookup</td>
<td>The most commonly used type of algorithm. It is easy to generate and works with different languages. When this algorithm replaces real, sensitive data with fictional data, it is possible that it will create repeating data patterns, known as “collisions.” For example, the name “Tom” and “Peter” could both be masked as “Matt.” Because names and addresses naturally recur in real data, this mimics an actual data set. However, if you want the masking engine to mask all data to unique outputs, you should use segmented mapping, described below.</td>
</tr>
<tr class="even">
<td>Segment Mapping</td>
<td>Produces no overlap or repetition in the masked data. You can mask up to a maximum of 36 values using segmented mapping. You might use this method if you need columns with unique values, such as Social Security Numbers, primary key columns, or foreign key columns. You can set the algorithm to produce alphanumeric results (letters and numbers) or only numbers.</td>
</tr>
<tr class="odd">
<td>Mapping</td>
<td><p>Allows you to state what value will replace the original data. There will be no collisions in the masked data, because it always matches the same input to the same output. For example “David” will always become “Ragu” and “Melissa” will always become “Jasmine.” The algorithm checks whether an input has already been mapped; if so, the algorithm changes the data to its designated output. You can use a mapping algorithm on any set of values, of any length, but you must know how many values you plan to mask.</p>
<p>NOTE: When you use a mapping algorithm, you cannot mask more than one table at a time. You must mask tables serially.</p></td>
</tr>
<tr class="even">
<td>Binary Lookup</td>
<td>Replaces objects that appear in object columns. For example, if a bank has an object column that stores images of checks, you can use binary lookup algorithm to mask those images. The Delphix Engine cannot change data within images themselves, such as the name on X-rays or driver’s licenses. However, you can replace all such images with a new, fictional image. This fictional image is provided by the owner of the original data.</td>
</tr>
<tr class="odd">
<td>Tokenization</td>
<td><p>The only type of algorithm that allows you to reverse its masking. For example, you can use a tokenization algorithm to mask data before you send it to an external vendor for analysis. The vendor can then identify accounts that need attention without having any access to the original, sensitive data. Once you have the vendor’s feedback, you can reverse the masking and take action on the appropriate accounts.</p>
<p>Like mapping, a tokenization algorithm creates a unique token for each input such as “David” or “Melissa.” The Delphix Engine stores both the token and original so that you can reverse masking later.</p></td>
</tr>
<tr class="even">
<td>Min Max</td>
<td>Values that are extremely high or low in certain categories allow viewers to infer someone’s identity, even if their name has been masked. For example, a salary of $1 suggests a company’s CEO, and some age ranges suggest higher insurance risk. You can use a min max algorithm to move all values of this kind into the midrange.</td>
</tr>
<tr class="odd">
<td>Data Cleaning</td>
<td>Does not perform any masking. Instead, it standardizes varied spellings, misspellings, and abbreviation for the same name. For example, “Ariz,” “Az,” and “Arizona” can all be cleaned to “AZ.”</td>
</tr>
<tr class="even">
<td>Free Text Redaction</td>
<td><p>Helps you remove sensitive data that appears in free-text columns such as “Notes.” This type of algorithm requires some expertise to use, because you must set it to recognize sensitive data within a block of text.</p>
<p>One challenge is that individual words might not be sensitive on their own, but together they may be. This algorithm uses profiler sets to determine which information it needs to mask. You can decide which expressions the algorithm uses to search for material such as addresses. For example, you can set the algorithm to look for “St,” “Cir,” “Blvd,” and other words that suggest an address. You can also use pattern matching to identify potential sensitive information. For example, a number that takes the form 123-45-6789 is likely to be a Social Security Number.</p>
<p>You can use free text redaction algorithm to show or hide information by displaying either a “black list” or a “white list.”</p></td>
</tr>
</tbody>
</table>

## Profile Job Concepts

The following set of concepts are options available to the user for
configuring a profiling job.

<table>
<thead>
<tr class="header">
<th><strong>Term</strong></th>
<th><strong>Definition</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Job Name</td>
<td>A free-form name for the job you are creating. Must be unique.</td>
</tr>
<tr class="even">
<td>Multi-Tenant</td>
<td>Check the box if the job is for a multi-tenant database. This option allows existing rulesets to be-reused to mask identical schemas via different connectors. The connector can be selected at job execution time.</td>
</tr>
<tr class="odd">
<td>Rule Set</td>
<td>Select a ruleset that this job will execute against.</td>
</tr>
</tr>
<tr class="odd">
<td>No. of Streams</td>
<td>The number of parallel streams to use when running the jobs. For example, you can select two streams to run two tables in the ruleset concurrently in the job instead of one table at a time.</td>
</tr>
<tr class="odd">
<td>Min Memory (MB) <em>optional</em></td>
<td>Minimum amount of memory to allocate for the job, in megabytes.</td>
</tr>
<tr class="even">
<td>Max Memory (MB) <em>optional</em></td>
<td>Maximum amount of memory to allocate for the job, in megabytes.</td>
</tr>
<tr class="odd">
<td>Feedback Size <em>optional</em></td>
<td>The number of rows to process before writing a message to the log. Set this parameter to the appropriate level of detail required for monitoring your job. For example, if you set this number significantly higher than the actual number of rows in a job, the progress for that job will only show 0 or 100%</td>
</tr>
<tr class="even">
<td>Profile Sets <em>optional</em></td>
<td><p>The name of a profile set, which is a subset of expressions (for example, a subset of financial expressions).</p>
</td>
</tr>
<tr class="odd">
<td>Comments <em>optional</em></td>
<td>Add comments related to this job.</td>
</tr>
<tr class="even">
<td>Email <em>optional</em></td>
<td>Add email address(es) to which to send status messages. Separate addresses with a comma (,).</td>
</tr>
</tbody>
</table>

## Masking Job Concepts

These concepts are options available to the user for configuring a
masking job.

<table>
<thead>
<tr class="header">
<th><strong>Term</strong></th>
<th><strong>Definition</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Job Name</td>
<td>A free-form name for the job you are creating. Must be unique across the entire application.</td>
</tr>
<tr class="even">
<td>Masking Method</td>
<td>Select either In-Place or On-The-Fly.</td>
</tr>
<tr class="odd">
<td>Multi-Tenant</td>
<td>Check box if the job is for a multi-tenant database.</td>
</tr>
<tr class="even">
<td>Rule Set</td>
<td>Select a ruleset for this job to execute against.</td>
</tr>
<tr class="odd">
<td>Masking Method</td>
<td>Select either In-place or On-the-fly.</td>
</tr>
<tr class="odd">
<td>Min Memory (MB) optional</td>
<td>Minimum amount of memory to allocate for the job, in megabytes.</td>
</tr>
<tr class="even">
<td>Max Memory (MB) optional</td>
<td>Maximum amount of memory to allocate for the job, in megabytes.</td>
</tr>
<tr class="odd">
<td>Update Threads</td>
<td><p>The number of update threads to run in parallel to update the target database.</p>
<p>For database using T-SQL, multiple update/insert threads can cause deadlock. If you see this type of error, reduce the number of threads that you specify in this box.</p></td>
</tr>
<tr class="even">
<td>Commit Size</td>
<td>The number of rows to process before issuing a commit to the database.</td>
</tr>
<tr class="odd">
<td>Feedback Size</td>
<td>The number of rows to process before writing a message to the logs. Set this parameter to the appropriate level of detail required for monitoring your job. For example, if you set this number significantly higher than the actual number of rows in a job, the progress that job will show 0% or 100%.</td>
</tr>
<tr class="even">
<td>Bulk Data <em>optional</em></td>
<td>For In-Place masking only. The default is for this check box to be clear. If you are masking very large tables in-place and require performance improvements, check this box. Delphix will mask data to a flat file, and then use inserts instead of updates to bulk load the target table.</td>
</tr>
<tr class="odd">
<td>Disable Trigger <em>optional</em></td>
<td>Whether to automatically disable database triggers. The default is for this check box to be clear and therefore not perform automatic disabling of triggers.</td>
</tr>
<tr class="even">
<td>Drop Index <em>optional</em></td>
<td>Whether to automatically drop indexes on columns which are being masked and automatically re-create the index when the masking job is completed. The default is for this check box to be clear and therefore not perform automatic dropping of indexes.</td>
</tr>
<tr class="odd">
<td>Prescript <em>optional</em></td>
<td>Specify the full pathname of a file that contains SQL statements to run before the job starts, or click Browse to specify a file. If you are editing the job and a pre script file is already specified, you can click the Delete button to remove the file. (The Delete button only appears if a prescript file was already specified.) For information about creating your own prescript files, see Create SQL Statements to Run Before and After Jobs.</td>
</tr>
<tr class="even">
<td>Postscript <em>optional</em></td>
<td>Specify the full pathname of a file that contains SQL statements to be run after the job finishes, or click Browse to specify a file. If you are editing the job and a postscript file is already specified, you can click the Delete button to remove the file. (The Delete button only appears if a postscript file was already specified.) For information about creating your own postscript file, see Creating SQL Statement to Run Before and After Jobs.</td>
</tr>
<tr class="odd">
<td>Comments <em>optional</em></td>
<td>Add comments related to this masking job.</td>
</tr>
<tr class="even">
<td>Email <em>optional</em></td>
<td>Add email address(es) to which to send status messages.</td>
</tr>
</tbody>
</table>
