# Creating a custom image for Windows #

Resource: [Creating a Window custom image](https://cloud.ibm.com/docs/vpc?topic=vpc-create-windows-custom-image)

If you are looking to build a new Windows system image to be imported to
IBM Cloud VPC, this PowerShell script will check and install some of the
required pieces that is needed by IBM Cloud VPC.

**Note:** DO NOT use this PowerShell script with VPC+ Cloud Migration tool.  VPC+ Cloud Migration
tool can migrate Windows VSI without the need of this script.

The script checks the following:
- If the system meets the minimum supported Windows version
     - If fails, then exit.  User will need to update to the minimum supported version.
- Check for cloud-init, version (minimum 1.1.0) and correct parameters
     - If cloudbase-init is missing, then download from https://cloudbase.it/cloudbase-init/ and
install it.
     - If files and parameters do not meet the requirements as described in the above Windows resource,
then create a backup file and make the necessary modification.
- Check for virtio driver or version (minimum 0.1.185)
     - If missing virtio driver, then download it from https://fedorapeople.org/groups/virt/virtio-win/direct-downloads/stable-virtio/
and install it.

To run the script, ensure the following:

- The assumption is that the system has internet access.  If the system does not have internet
access, then another box download (CloudbaseInitSetup_Stable_x64.msi and virtio-win.iso) and copy
the files to the C:\temp folder.
- Windows has a PowerShell script policy that you might need to change -- https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.security/set-executionpolicy?view=powershell-7.1
     - If you change the policy, it’s a good practice to change the settings back.
- Usage ```PS C:\ .\windows_precheck.ps```
- The system still needs to go through Windows sysprep, device driver update, image conversion.
For more information, reference the above link. 
