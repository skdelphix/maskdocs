# Prerequisites

This section will detail the hardware/software requirements needed to
deploy the Delphix Engine with the Masking service. The Delphix
Engine is a self-contained operating environment and application that is
provided as a Virtual Appliance. Our Virtual Appliance is certified to
run on a variety of platforms including VMware, AWS, and Azure.

The Delphix Engine should be placed on a server where it will not
contend with other VMs for network, storage or other compute resources.
The Delphix Engine is a CPU and I/O intensive application, and deploying it in
an environment where it must share resources with other virtual
machines, can significantly reduce performance.

Delphix Masking and Delphix Virtualization should never be
run inside the same virtual machine. Always use seperate, dedicated Delphix Engines for Masking and Virtualization.

## Client Web Browser

The Delphix Engine's graphical interface can be accessed from a variety of
different web browsers. The Delphix Engine currently supports the following web browsers:

* Microsoft Internet Explorer 11.0 or higher
* Microsoft Edge 40.x or higher
* Mozilla Firefox 35.0 or higher
* Chrome 40 or higher


!!! tip "TIP - Microsoft Internet Explorer"
    Make sure that Internet Explorer is not configured for compatibility mode.

## VMware Platform

This section covers the virtual machine requirements for installation of
a dedicated Delphix Masking Engine on the VMware Virtual platform.

#### Versions

The Delphix Engine can be run on several version of VMware ESX/ESXI ([see
support matrix](https://docs.delphix.com/docs/system-installation-configuration-and-management/installation-and-initial-configuration-requirements/virtual-machine-requirements-for-vmware-platform)).

#### Virtual CPUs

The minimum amount of virtual CPUs is 8v CPUs. CPU resource shortfalls
can occur under high I/O throughput conditions. Also, CPU reservation is
strongly recommended for the Delphix VM, so that Delphix is guaranteed
the full complement of vCPUs even when resources are overcommitted.

#### Virtual Memory

The minimum amount of virtual memory is 16GB vRAM but we highly
recommend 32GB or higher. The masking service on the Delphix Engine uses its memory to process database and file blocks. More memory can sometimes improve performance. Memory reservation is a requirement for the Delphix VM.
Overcommitting memory resources in the ESX server will significantly
impact the performance of the Delphix Engine. Reservation ensures that
the Delphix Engine will not stall while waiting for the ESX server to
page in the engine’s memory.

!!! tip "TIP - Do not allocate all memory to the Delphix VM"

    Never allocate all available physical memory to the Delphix VM. You must set aside memory for the ESX Server to perform hypervisor activities before you assign memory to Delphix and other VMs. The default ESX minimum free memory requirement is 6% of total RAM. When free memory falls below 6%, ESX starts swapping out the Delphix guest OS. We recommend leaving about 8-10% free to avoid swapping

    For example, when running on an ESX Host with 512GB of physical memory, allocate no more than 470GB (92%) to the Delphix VM (and all other VMs on that host).

#### Storage

##### System Disk

The minimum recommended storage size of the System Disk (rpool) is 300 GB.

The VMFS volume must be located on shared storage in order to use vMotion and HA features.

The VMDK for the System Disk is often created in the same VMFS volume as the Delphix VM definition. In that case, the datastore must have sufficient space to hold the VMDK for the System Disk and the Delphix VM definition.

##### Configuration Disk(s)

The minimum recommended storage size of the Configuration Volume (domain0) is 50 GB.

## AWS EC2 Platform

This section covers the virtual machine requirements for installation of
a dedicated Delphix Masking Engine on Amazon's Elastic Cloud Compute
(EC2) platform.

For best performance, the Delphix Masking Engine and all database/file
servers should be in the same AWS region.

#### Instance Types

The Delphix Masking Engine can run on a variety of different instances,
including large memory instances (preferred) and high I/O instances. We
recommend the following large memory and high I/O instances:

<table>
<thead>
<tr class="header">
<th>Large Memory Instances (preferred)</th>
<th>High I/O Instances (supported)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li>
<p>r4.2xlarge</p>
</li>
<li>
<p>r4.4xlarge</p>
</li>
<li>
<p>r4.8xlarge</p>
</li>
<li>
<p>r3.2xlarge</p>
</li>
<li>
<p>r3.4xlarge</p>
</li>
<li>
<p>r3.8xlarge</p>
</li>
</ul></td>
<td><ul>
<li>
<p>i3.2xlarge</p>
</li>
<li>
<p>i3.4xlarge</p>
</li>
<li>
<p>i3.8xlarge</p>
</li>
</ul></td>
</tr>
</tbody>
</table>

Larger instance types provide more CPU, which can prevent resource
shortfalls under high I/O throughput conditions. For more
information please refer to, [<span class="underline">Virtual Machine
Requirements for AWS EC2 Platform</span>](https://docs.delphix.com/docs/system-installation-configuration-and-management/installation-and-initial-configuration-requirements/virtual-machine-requirements-for-aws-ec2-platform).

!!! tip "TIP - Estimating Delphix VM Memory Requirements"

    On the AWS EC2 platform, the Delphix Masking Engine must have sufficient memory to operate when multiple masking jobs are running. Our recommendation is to provide 8 GB of memory for the Delphix Masking Engine in addition to any memory that will be used by running jobs.


#### Network Configurations

You must deploy the Delphix Engine and all database or file hosts
in a VPC network to ensure that private IP addresses are
static and do not change when you restart instances. When adding
environments to the Delphix Engine, you must use the host's VPC (static
private) IP addresses.

The EC2 Delphix instance must be launched with a static IP address;
however, the default behavior for VPC instances is to launch with a
dynamic public IP address – which can change whenever you restart the
instance. If you're using a public IP address for your Delphix Engine,
static IP addresses can only be achieved by using assigned AWS Elastic
IP
Addresses.

!!! tip "TIP - Port Configuration"
    The default security group will only open port 22 for secure shell (SSH) access. You must modify the security group to allow access to all of the networking ports used by the Delphix Engine and the various source and target engines. See [<span class="underline">General Network and Connectivity Requirements</span>](https://docs.delphix.com/docs/system-installation-configuration-and-management/installation-and-initial-configuration-requirements/general-network-and-connectivity-requirements) for information about specific port configurations.

#### Storage Configurations

##### Elastic Block Store (EBS) Requirements

All attached storage devices must be EBS volumes. Delphix does not
support the use of instance store volumes. Because EBS volumes are
connected to EC2 instances via the network, other network activity on
the instance can affect throughput to EBS volumes. EBS optimized
instances provide guaranteed throughput to EBS volumes and are required
(for instance types that support it) in order to provide consistent and
predictable storage performance.

Use EBS volumes with provisioned IOPs in order to provide consistent and
predictable performance. The number of provisioned IOPs depends on the
estimated IO workload on the Delphix Engine. Provisioned IOPs volumes
must be configured with a volume size at least 30 GiB times the number
of provisioned IOPs. For example, a volume with 3,000 IOPS must be
configured with at least 100 GiB.

I/O requests of up to 256 kilobytes (KB) are counted as a single I/O
operation (IOP) for provisioned IOPs volumes. Each volume can be
configured for up to 4,000 IOPs.

##### System Disk

The minimum recommended storage size for the System Disk (rpool) is 300 GB.

##### Configuration Disk(s)

The minimum recommended storage size of the Configuration Volume (domain0) is 50 GB.

## Azure Platform

This section covers the virtual machine requirements for installation of
a dedicated Delphix Masking Engine on Microsoft's Azure cloud platform.

For best performance, the Delphix Masking Engine and all database/file
servers should be in the same Azure Region.

#### Instance Types

The Delphix Engine can run on a variety of different Azure instances.
We recommend the following instances:

  - DS14v2 - 16 CPUs, 112GB, 32 devices

  - DS15v2 - 20 CPU, 140GB, 40 devices

  - GS3 - 8 CPUs, 112GB, 16 devices

  - GS4 - 16 CPUs, 244GB, 32 devices

  - GS5 - 32 CPUs, 448GB, 64 devices

!!! tip "TIP - Estimating Delphix VM Memory Requirements"

    On the Azure platform, the Delphix Masking Engine must have sufficient memory to operate when multiple masking jobs are running. Our recommendation is to provide 8 GB of memory for the Delphix Masking Engine in addition to any memory that will be used by running jobs.

#### Network Configurations

The Delphix Engine and all database/file servers must be in the same Azure Virtual Network (VNet).

!!! tip "TIP - Port Configuration"
    You must modify the Network Security Group (NSG) to allow access to all of the networking ports used by the Delphix Engine and the various data sources. See [<span class="underline">General Network and Connectivity Requirements</span>](https://docs.delphix.com/docs/system-installation-configuration-and-management/installation-and-initial-configuration-requirements/general-network-and-connectivity-requirements) for information about specific port configurations.

#### Storage Configurations

##### Requirements

When configuring storage for the Delphix Engine we recommend Azure
Premium Storage which uses solid-state drives (SSDs). Devices up to 4096 GB
are supported with a total maximum of 256 TB.

I/O requests of up to 256 kilobytes (KB) are counted as a single I/O
operation (IOP) for provisioned IOPs volumes. IOPS vary based on storage
size with a maximum of 7,500 IOPS.

##### System Disk

The minimum recommended storage size for the System Disk (rpool) is 300 GB.

##### Configuration Disk(s)

The minimum recommended storage size of the Configuration Volume (domain0) is 50 GB.

## Google Cloud Platform

This section covers the virtual machine requirements for installation of
a dedicated Delphix Masking Engine on Google Cloud Platform (GCP).

### Machine Types

The following is a list of instance types that are supported to deploy Delphix on GCP. Delphix periodically certifies new instance types, which will be added to the list here.

| **Requirements** | **Notes** |
| ----------- | --------- |
| n2-standard-(32,64,96)|Larger instance types provide more CPU, which can prevent resource shortfalls under high I/O throughput conditions.  |
| n2-highmem-(32,64,96)| Larger instances also provide more memory, which the Delphix Engine uses to cache database blocks. More memory will provide better read performance.|

### Network Configuration

| **Requirements** | **Notes** |
| ----------- | --------- |
|Virtual Private Cloud| You must deploy the Delphix Engine and database/file servers in a VPC network to ensure that private IP addresses are static and do not change when you restart instances. When adding connectors to the Masking Engine, you must use the host's VPC (static private) IP addresses.|
|Static Public IP| The GCP Delphix instance must be launched with a static IP address; however, the default behavior for VPC instances is to launch with a dynamic public IP address – which can change whenever you restart the instance. |
|Security Group Configuration| The default security group will only open port 22 for SSH access. You must modify the security group to allow access to all of the networking ports used by the Delphix Engine and the various source and target engines.|
|Premium Networking| It is recommended to use GCP Premium Tier Networking.|


### Storage Configuration

##### System Disk

The minimum recommended storage size for the System Disk (rpool) is 300 GB.

##### Configuration Disk(s)

The minimum recommended storage size of the Configuration Volume (domain0) is 50 GB.

### Additiona GCP Configuration Notes

 - Delphix supports both Zonal and Regional SSD persistent disks.
