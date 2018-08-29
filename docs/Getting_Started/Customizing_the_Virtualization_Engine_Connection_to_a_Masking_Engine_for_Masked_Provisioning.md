# Customizing the Virtualization Engine Connection to a Masking Engine for Masked Provisioning

During the VDB provisioning process, the Virtualization Engine can optionally run a masking job from the Delphix Masking Engine on the VDB. By default, the Delphix Engine attempts to obtain a list of masking jobs from a Delphix Masking Engine on its localhost. It's possible to split the Delphix Engine and Delphix Masking Engine apart on separate hosts. If the Virtualization Engine and Delphix Masking Engine are on different hosts, use these instructions to customize the host address and/or port number that the Delphix Engine will use to contact the Delphix Masking Engine.

##Cross-Engine Version Compatibility
!!! Important Validation Notices
   When upgrading an engine, the other must be upgraded at the same time to the same version.
Delphix does not validate that the API version the Delphix Engine matches with the API version of the Delphix Masking Engine. With this in mind, Delphix recommends that users ensure both engines are on the exact same version.
There is no validation that a Masking Engine exists at the given server and port. Users should ensure that they are specifying an already existing engine, and are giving valid authentication for it.
Old versions of the serviceconfig or any information associated with them are not tracked. In particular, if you have been using the local masking service or a remote service and then change to a new remote service Delphix will start throwing out any old job information on the next masking job/fetch or GUI reload. Users should not rely on that information being preserved through serviceconfig updates.
Delphix does not do validate network availability between the two engines or any other hosts that both engines might want to communicate with.
The state or availability of either host is not checked, if either host becomes unduly slow, congested, or unresponsive Delphix will not be able to issue compelling warnings regarding those issues.

##Bridge Account
If the Virtualization Engine and Delphix Masking Engine are on different hosts, use these instructions to customize the host address and/or port number that the Delphix Engine will use to contact the Delphix Masking Engine.

!!! Note: This does not alter the Delphix Masking Engine UI port. It is specific to coordinating communication between the Masking Engine and a Virtualization Engine about available masking jobs and job results.

## Creating a Cross-Engine Bridge
To change the Masking Engine connection details on the Virtualization engine:

1. Using a shell, login to the **CLI** using **delphix_admin**.
2. At the **CLI root** prompt, type **maskingjob**.
3. At the **maskingjob** prompt, type **serviceconfig**.
4. To list service configurations, type **ls**.
5. At the serviceconfig, type select **`MASKING_SERVICE_CONFIG-1**.
6. To view the configurations, type **ls**.
7. With this service config selected, enter **update**.
8. In the update mode, type **set port=[YOUR DESIRED PORT NUMBER]**.
9. Commit the change by typing **commit**.
10. Type ls to confirm the configurations.
11. Type **exit** to exit the CLI.
12. Re-type the masking URL reflecting the new details and refresh the browser