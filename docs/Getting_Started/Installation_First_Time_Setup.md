# Installation/First Time Setup

This section walks you step by step on how to download and install the
Delphix Engine software onto your infrastructure (VMware, AWS EC2, or
Azure).

## Installing OVA on VMware

For detailed recommendations on hardware prerequisites for VMware,
please see Getting Started - Prerequisites. Here are the steps to
getting your OVA installed:

  - **Step 1:** Download the OVA file from Delphix’s Download site.
    Note, you will need a support login from your sales team or
    welcome letter. Navigate to “Virtual Appliance” and download the
    appropriate OVA. If unsure, use the HWv8\_Standard type.

  - **Step 2:** Login using the vSphere client to the vSphere server
    (or vCenter Server) where you want to install the Delphix Engine.

  - **Step 3:** In the vSphere Client, click File.

  - **Step 4:** Select Deploy OVA Template and then browse to the OVA
    file. Click Next.

  - **Step 5:** Select a hostname for the Delphix Engine. This
    hostname will be used in configuring the Delphix Engine network.

  - **Step 6:** Select the data center where the Delphix Engine will
    be located.

  - **Step 7:** Select the cluster and the ESX host.

  - **Step 8:** Select one (1) data store for the Delphix OS. This
    datastore can be thin-provisioned and must have enough free space
    to accommodate the 300GB comprising the Delphix operating system.

  - **Step 9:** Select four (4) or more data stores for Database
    Storage for the Delphix Engine. The Delphix Engine will stripe all
    of the Database Storage across these VMDKs, so for optimal I/O
    performance each VMDK must be equal in size and be configured
    Thick Provisioned - Eager Zeroed. Additionally, these VMDKs should
    be distributed as evenly as possible across all four SCSI I/O
    controllers, as described in KB045 Re-configuring Controllers.

  - **Step 10:** Select the virtual network you want to use. If using
    multiple physical NICs for link aggregation, you must use vSphere
    NIC teaming. Do not add multiple virtual NICs to the Delphix
    Engine itself. The Delphix Engine should use a single virtual
    network. For more information, see Optimal Network Architecture
    for the Delphix Engine.

  - **Step 11:** Click Finish. The installation will begin and the
    Delphix Engine will be created in the location you specified.

  - **Step 12:** Jump to “Activating the Masking Service” section
    below to learn how to activate the masking service now that you
    have the software installed.

## Installing AMI on AWS EC2

For detailed recommendations on hardware prerequisites for AWS EC2,
please see Getting Started - Prerequisites. Here are the steps to
getting your AMI installed:

  - **Step 1:** On the Delphix download site, click the AMI you would
    like to share and accept the Delphix License agreement.
    Alternatively, follow a link given by your Delphix solutions
    architect.

  - **Step 2:** On the Amazon Web Services Account Details form
    presented:
    
      - Enter your AWS Account Identifier, which can be found here:
        https://console.aws.amazon.com/billing/home?\#/account. If you
        want to use the GovCloud AWS Region, be sure to enter the ID
        for the AWS Account which has GovCloud enabled.
    
      - Select which AWS Region you would like the AMI to be shared
        in. If you would like the AMI shared in a different region,
        contact your Delphix account representative to make the proper
        arrangements.

  - **Step 3:** Click Share. The Delphix Engine will appear in your
    list of AMIs in AWS momentarily.

  - **Step 4:** Reference the Installation and Configuration
    Requirements for AWS/EC2 when deploying the AMI.

  - **Step 5:** Jump to “Activating the Masking Service” section below
    to learn how to activate the masking service now that you have the
    software installed.

## Installing VHD on AZURE

For detailed recommendations on hardware prerequisites for Azure, please
see Getting Started - Prerequisites. Here are the steps to getting your
VHD installed:

  - **Step 1:** On the [<span class="underline">Microsoft Azure
    Marketplace</span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/delphix.delphix_dynamic_data_platform?tab=Overview),
    search for Delphix. Click **GET IT NOW.**

  - **Step 2:** Reference the Installation and Configuration
    Requirements for the Delphix Engine in Azure when deploying the
    VHD.

  - **Step 3:** Jump to “Activating the Masking Service” section below
    to learn how to activate the masking service now that you have the
    software installed.

## Activating the Masking Service 

Once you have installed your Delphix Engine, you will need to activate
the masking service through the CLI and then set up your first
administrator user.

To activate the Masking service via the CLI, do the following:

  - **Step 1:** Connect to the CLI via SSH as **sysadmin** or with
    other system administrator credentials.

  - **Step 2:** Start the Delphix Masking Engine with: system ;
    startMasking ; commit ; exit

<!-- end list -->

  - **Step 3:** Access the UI by navigating to http://\<Delphix Engine
    IP or DNS name\>:8282/dmsuite.

  - **Step 4:** Login as user **Admin** and password **Admin\_12**.

  - **Step 5:** Change the **Admin** password to a unique value for
    your installation.
    
    1.  To change the password, go to the **Admin** tab.
    
    2.  Click **Users**.
    
    3.  Edit the **Admin** user.

  - **Step 6:** Generate a unique secret key for your installation.
    
    4.  In the **Admin** tab, click **Users**.
    
    5.  Click **Generate New Key**. Once your Delphix Masking Engine
        is installed and enabled, you can prepare your data for
        masking

Congratulations\! You are now ready to start using the masking service\!
