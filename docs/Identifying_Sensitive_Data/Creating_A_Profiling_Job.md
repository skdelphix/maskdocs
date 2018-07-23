# Creating A Profiling Job

This section describes how users can create a profile job.

## Creating a New Profiling Job

You can create profiling jobs for databases, copybooks, delimited files,
fixed-width, and Excel files.

A Profiling job for a mainframe system cannot assign groups because it
does not have the heuristics needed to determine sensitive elements per
group. The Profiler assigns group-sensitive elements to a single group.
Then, in inventory, groups are updated as needed to establish the
sensitive element field group sets.

To create a new profiling job:

1.  Click **Profile**.

2.  The **Create Profiling Job** window appears.

    ![](./media/image2.png)

3.  *Create Profile Job*

4.  You will be prompted for the following information:
    
    1.  **Job Name** — A free-form name for the job you are creating.
        Must be unique.
    
    2.  **Multi Tenant** — Check the box if the job is for a
        multi-tenant database. This option allows existing rulesets to
        be re-used to mask identical schemas via different connectors.
        The connector can be selected at job execution time.
    
    3.  **Rule Set** — Select a rule set that this job will execute
        against.
    
    4.  **Generator** — The default value is **Delphix**.
    
    5.  **No. of Streams** — The number of parallel streams to use
        when running the jobs. For example, you can select two streams
        to run two tables in the ruleset concurrently in the job
        instead of one table at a time.
    
    6.  **Remote Server** — (optional) The remote server that will
        execute the jobs. This option lets you choose to execute jobs
        on a remote server, rather than on the local Delphix instance.
        Note: This is an add-on feature for Delphix Standard Edition.
    
    7.  **Min Memory (MB)** — (optional) Minimum amount of memory to
        allocate for the job, in megabytes.
    
    8.  **Max Memory (MB)** — (optional) Maximum amount of memory to
        allocate for the job, in megabytes.
    
    9.  **Feedback Size** — (optional) The number of rows to process
        before writing a message to the logs. Set this parameter to
        the appropriate level of detail required for monitoring your
        job. For example, if you set this number significantly higher
        than the actual number of rows in a job, the progress for that
        job will only show 0 or 100%.
    
    10. **Profile Sets** — (Optional) The name of a profiler set,
        which is a subset of expressions (for example, a subset of
        financial expressions). (See Delphix Administrator's Guide.)
    
    11. **Note:** If you do not select a profile set, Delphix will use
        all defined expressions instead of just a subset.
    
    12. **Comments** — (optional) Add comments related to this job.
    
    13. **Email** — (optional) Add e-mail address(es) to which to send
        status messages. Separate addresses with a comma (,).

5.  When you are finished, click **Save**.
