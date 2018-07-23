# Prerequisites 

This section will detail the hardware/software requirements needed to
deploy the Delphix Masking (service on the Delphix Engine). The Delphix
Engine is a self-contained operating environment and application that is
provided as a Virtual Appliance. Our Virtual Appliance is certified to
run on a variety of platforms including VMware, AWS, and Azure.

The Delphix Engine should be placed on a server where it will not
contend with other VMs for network, storage or other compute resources.
The Delphix Engine is an I/O intensive application, and deploying it in
an environment where it must share resources with other virtual
machines, can significantly reduce performance.

## VMware Virtual Platform

This section covers the virtual machine requirements for installation of
a dedicated Delphix Masking Engine on the VMware Virtual platform.

#### VMWare Platform

The Delphix Engine can be run on several version of VMware ESX/ESXI(see
support matrix). With that being said, we highly recommend running
versions 5.0 or above for optimal performance.

#### Virtual CPUs

The minimum amount of virtual CPUs is 8v CPUs. CPU resource shortfalls
can occur under high I/O throughput conditions. Also, CPU reservation is
strongly recommended for the Delphix VM, so that Delphix is guaranteed
the full complement of vCPUs even when resources are overcommitted.

#### Virtual Memory

The minimum amount of virtual memory is 16GB vRAM but we highly
recommend 32GB or higher. The masking service on the Delphix Engine uses
its memory to cache database blocks. More memory provides better
performance. Memory reservation is a requirement for the Delphix VM.
Overcommitting memory resources in the ESX server will significantly
impact the performance of the Delphix Engine. Reservation ensures that
the Delphix Engine will not stall while waiting for the ESX server to
page in the engine’s memory.

!!! tip "TIP - Do not allocate all memory to the Delphix Engine"

    Never allocate all available physical memory to the Delphix VM. You must set aside memory for the ESX Server to perform hypervisor activities before you assign memory to Delphix and other VMs. The default ESX minimum free memory requirement is 6% of total RAM. When free memory falls below 6%, ESX starts swapping out the Delphix guest OS. We recommend leaving about 8-10% free to avoid swapping
    
    For example, when running on an ESX Host with 512GB of physical memory, allocate no more than 470GB (92%) to the Delphix VM (and all other VMs on that host).

#### Delphix Engine System Disk Storage

The minimum recommended storage on the Delphix Engine System Disk is
300GB. The System disk may need to be substantially larger if bulk
logging will be enabled. The actual size will depend on the data being
masked. The VMDK for the Delphix Engine system disk storage is often
created in the same VMFS volume as the Delphix VM definition. In that
case, the datastore must have sufficient space to hold the Delphix VM
configuration, the VMDK for the system disk, and a paging area if a
memory reservation was not enabled for the Delphix Engine.

!!! tip "TIP - Less Storage Is Needed For Earlier Versions"
    For versions 5.1.2 and below the recommended storage is 150 GB.

#### Client Browser

The Delphix Engine can be utilized from a variety of different browsers.
The Delphix Engine currently supports several browsers (see support
matrix).

!!! tip "TIP - Microsoft Internet Explorer"
    Make sure that Internet Explorer is not configured for compatibility mode.

## AWS EC2 Platform

This section covers the virtual machine requirements for installation of
a dedicated Delphix Masking Engine on Amazon's Elastic Cloud Compute
(EC2) platform. Delphix Masking and Delphix Virtualization should not be
run on the same EC2 instance.

For best performance, the Delphix Masking Engine and all database
servers should be in the same AWS region.

#### Instance Types

The Delphix Engine can run on a variety of different instances,
including large memory instances (preferred) and high I/O instances. The
Delphix Engine most closely resembles a storage appliance and performs
best when provisioned using a storage optimized instance type. We
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
<li>
<p>i2.2xlarge</p>
</li>
<li>
<p>i2.4xlarge</p>
</li>
<li>
<p>i2.8xlarge</p>
</li>
</ul></td>
</tr>
</tbody>
</table>

Larger instance types provide more CPU, which can prevent resource
shortfalls under high I/O throughput conditions. Larger instances also
provide more memory, which the Delphix Engine uses to cache database
blocks. More memory will provide better read performance. For more
information please refer to, [<span class="underline">Virtual Machine
Requirements for AWS EC2
Platform</span>](https://docs.delphix.com/display/DOCSDEV/.Virtual+Machine+Requirements+for+AWS+EC2+Platform+vJocaceanMaint).

#### Network Configurations

You must deploy the Delphix Engine and all of the source and target
environments in a VPC network to ensure that private IP addresses are
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
    The default security group will only open port 22 for secure shell (SSH) access. You must modify the security group to allow access to all of the networking ports used by the Delphix Engine and the various source and target engines. See **(insert link to more detailed section)** for information about specific port configurations.

#### EBS Configurations

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

#### General Storage Configurations

Allocate initial storage equal to the size of the physical source
databases. For high redo rates and/or high DB change rates, allocate an
additional 10-20% storage.

Add storage when storage capacity approaches 30% free. Keep all EBS
volumes the same size. Add new storage by provisioning new volumes of
the same size.

Maximize Delphix Engine RAM for a larger system cache to service reads.
Use at least 3 EBS volumes to maximize performance. This enables the
Delphix File System (DxFS) to make sure that its file systems are always
consistent on disk without additional serialization. This also enables
the Delphix Engine to achieve higher I/O rates by queueing more I/O
operations to its storage.

## Azure Platform

This section covers the virtual machine requirements for installation of
a dedicated Delphix Masking Engine on Microsoft's Azure cloud platform.
Delphix Masking and Delphix Virtualization should not be run on the same
Azure instance.  
  
For best performance, the Delphix Masking Engine and all database
servers should be in the same Azure Region.

#### Instance Types

The Delphix Engine can run on a variety of different Azure instances.
The Delphix Engine most closely resembles a storage appliance and
performs best when provisioned using a storage optimized instance type.
We recommend the following memory and storage optimized instances:

  - GS3 - 8 CPUs, 112GB, 16 TB (20,000 IOPS)

  - GS4 - 16 CPUs, 244GB, 32 TB (40,000 IOPS)

  - GS5 - 32 CPUs, 448GB, 64 TB (80,000 IOPS)

#### Network Configurations

Network Configuration for Delphix Engines running on the Azure Platform
can be configured on the Azure Virtual Network (VNet). Delphix Engine
and all the source and target environments must be accessible within the
same virtual
network.

!!! tip "TIP - Port Configuration"
    You must modify the security group to allow access to all of the networking ports used by the Delphix Engine and the various source and target engines. See **(insert link to more detailed section)** for information about specific port configurations.

#### Storage Configurations

When configuring storage for the Delphix Engine we recommend Azure
Premium Storage which uses solid-state drives (SSDs). Devices up to 1024
are supported with a total maximum of 64tb.

I/O requests of up to 256 kilobytes (KB) are counted as a single I/O
operation (IOP) for provisioned IOPs volumes. IOPS vary based on storage
size with a maximum of 5,000 IOPS.
