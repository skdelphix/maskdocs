# Installation/First Time Setup

This section walks you step by step on how to download and install the
Delphix Engine software onto your infrastructure (VMware, AWS EC2, or
Azure).

## Installing OVA on VMware

For detailed recommendations on hardware prerequisites for VMware,
please see [Getting Started - Prerequisites](Prerequisites/). Here are the steps to
getting your OVA installed:

  1. Download the OVA file from Delphix’s Download site.
    Note, you will need a support login from your sales team or
    welcome letter. Navigate to “Virtual Appliance” and download the
    appropriate OVA. If unsure, use the HWv8\_Standard type.

  2. Login using the vSphere client to the vSphere server
    (or vCenter Server) where you want to install the Delphix Engine.

  3. In the vSphere Client, click File.

  4. Select Deploy OVA Template and then browse to the OVA
    file. Click Next.

  5. Select a hostname for the Delphix Engine. This
    hostname will be used in configuring the Delphix Engine network.

  6. Select the data center where the Delphix Engine will
    be located.

  7. Select the cluster and the ESX host.

  8. Select one (1) data store for the Delphix OS. This
    datastore can be thin-provisioned and must have enough free space
    to accommodate the 300GB comprising the Delphix operating system.

  9. The Delphix VM Configuration Storage requires a minimum of 10GB. The VMFS volume should have enough available space to hold all ESX configuration and log files associated with the Delphix Engine.

      The Delphix Engine system disk should be stored in a VMDK system drive. The VMFS volume where the .ova is deployed should therefore have at least 300GB of free space prior to deploying the .ova. The VMFS volume must be located on shared storage in order to use vMotion and HA features.	

  10. Select the virtual network you want to use. If using
    multiple physical NICs for link aggregation, you must use vSphere
    NIC teaming. Do not add multiple virtual NICs to the Delphix
    Engine itself. The Delphix Engine should use a single virtual
    network. For more information, see Optimal Network Architecture
    for the Delphix Engine.

  11. Click Finish. The installation will begin and the
    Delphix Engine will be created in the location you specified.

  12. Jump to “Activating the Masking Service” section
    below to learn how to activate the masking service now that you
    have the software installed.

## Installing AMI on AWS EC2

For detailed recommendations on hardware prerequisites for AWS EC2,
please see [Getting Started - Prerequisites](Prerequisites/). Here are the steps to
getting your AMI installed:

  1. On the Delphix download site, click the AMI you would
    like to share and accept the Delphix License agreement.
    Alternatively, follow a link given by your Delphix solutions
    architect.

  2. On the Amazon Web Services Account Details form
    presented:

      - Enter your AWS Account Identifier, which can be found here:
        https://console.aws.amazon.com/billing/home?\#/account. If you
        want to use the GovCloud AWS Region, be sure to enter the ID
        for the AWS Account which has GovCloud enabled.

      - Select which AWS Region you would like the AMI to be shared
        in. If you would like the AMI shared in a different region,
        contact your Delphix account representative to make the proper
        arrangements.

  3. Click Share. The Delphix Engine will appear in your
    list of AMIs in AWS momentarily.

  4. Reference the Installation and Configuration
    Requirements for AWS/EC2 when deploying the AMI.

  5. Jump to “Activating the Masking Service” section below
    to learn how to activate the masking service now that you have the
    software installed.

## Installing VHD on AZURE

For detailed recommendations on hardware prerequisites for Azure, please
see [Getting Started - Prerequisites](Prerequisites/). Here are the steps to getting your
VHD installed:

  1. On the [Microsoft Azure
    Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/delphix.delphix_dynamic_data_platform?tab=Overview),
    search for Delphix. Click **GET IT NOW**.

  2. Reference the Installation and Configuration
    Requirements for the Delphix Engine in Azure when deploying the
    VHD.

  3. Jump to “Activating the Masking Service” section below
    to learn how to activate the masking service now that you have the
    software installed.

## Activating the Masking Service

Once you have installed your Delphix Engine, you will need to activate
the masking service through the CLI and then set up your first
administrator user.

To activate the Masking service via the CLI, do the following:

  1. Connect to the CLI via SSH as **sysadmin** or with
    other system administrator credentials.

  2. Start the Delphix Masking Engine with: system ;
    startMasking ; commit ; exit

  3. Access the UI by navigating to http://&lt;Delphix Engine
    IP or DNS name&gt;:8282/masking.

  4. Login as user **Admin** and password **Admin-12**.

  5. Change the **Admin** password to a unique value for
    your installation.

     a.  To change the password, go to the **Admin** tab.

     b.  Click **Users**.

     c.  Edit the **Admin** user.

     d.  Change the **Admin** user's password.

Congratulations\! You are now ready to start using the masking service\!
