# Customizing the Virtualization Engine Connection to a Masking Engine for Masked Provisioning

## Introduction

During the VDB provisioning process, the Virtualization Engine can optionally run a masking job from the Delphix Masking Engine on the VDB. By default, the Virtualization Engine attempts to obtain a list of masking jobs from a Masking Engine on its localhost. It's possible to split the Virtualization Engine and Masking Engine apart on separate hosts. If the Virtualization Engine and Masking Engine are on different hosts, use these instructions to customize the host address, port number, and/or login credentials that the Virtualization Engine will use to contact the Masking Engine.

!!! warning "Important Validation Notices"

    When using seperate Virtualization and Masking engines, ensure that the versions are compatible. See the [compatiblity matrix](Provision_Masked_VDBs/#virtualization-and-masking-engine-compatibility-matrix).
    
    Old versions of the serviceconfig or any information associated with them are not tracked. In particular, if you have been using the local masking service or a remote service and then change to a new remote service Delphix will start throwing out any old job information on the next masking job/fetch or GUI reload. Users should not rely on that information being preserved through serviceconfig updates.
    
    Delphix does not validate network availability between the two engines or any other hosts that both engines might want to communicate with. The state or availability of either host is not checked, if either host becomes unduly slow, congested, or unresponsive Delphix will not be able to issue compelling warnings regarding those issues.

## Instructions
If the Virtualization Engine and Masking Engine are on different hosts, use these instructions to customize the host address, port number, and/or login credentials that the Virtualization Engine will use to contact the Masking Engine.

!!! note 

    This does not alter the Delphix Masking Engine UI port. It is specific to coordinating communication between the Virtualization Engine and a Masking Engine about available masking jobs and job results.

To change the Virtualization Engine's connection details for its Masking Engine:

1. Using a shell, login to the **CLI** using **delphix_admin**.
2. At the **CLI** root prompt, type **maskingjob**.
3. At the **maskingjob** prompt, type **serviceconfig**.
4. To list service configurations, type **ls**.
5. At the serviceconfig, type select **`MASKING_SERVICE_CONFIG-1**.
6. To view the configurations, type **ls**.
7. With this service config selected, enter **update**.
8. In the update mode, use the **set** command to modify the configuration. For example, type **set port=[YOUR DESIRED PORT NUMBER]** to change the port number.
9. Commit the change by typing **commit**.
10. Type **ls** to confirm the configurations.
11. Type **exit** to exit the CLI.
