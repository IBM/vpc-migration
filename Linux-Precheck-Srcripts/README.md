# Precheck Scripts #
There is a set of minimum image requirements when you migrate a virtual/guest machine to IBM Cloud
as a custom image. More information can be found [here](https://cloud.ibm.com/docs/vpc?topic=vpc-managing-images).

It is highly recommended to test the precheck scripts on a clone of the virtual/guest machine and
not on the actual system.

## Red Hat ##
Resource: [Creating a Linux custom image](https://cloud.ibm.com/docs/vpc?topic=vpc-create-linux-custom-image)

A script written in BASH that automates some of the tasks are described in the link above.  This
script can be used if you are planning to do the migration yourself or use in conjunction with VPC+ 
Cloud Migration tool.

The script checks the following:
- If the system meets the minimum supported major version (7.x)
     - If missing, then exit.  User will need to upgrade the OS.
- Check for virtio drivers
     - If missing, then exit.  User will need to install the virtio driver.
- Check for cloud-init and correct data source.
     - If missing cloud-init, then install from yum repository and add the correct data sources.
     - If data sources are missing, then make a backup copy of cloud.cfg to cloud.cfg.bak and correct 
the data source parameters.
     - If the virtual server instance is from IBM classic infrastructure and has secondary attached
volumes, then check for NOFAIL flag.  If not present, then add NOFAIL.

**NOTE:** The script does depend on yum in order to install cloud-init.  Make sure your repository is
active and current.

To execute the script, run the following command: </br>
```./rhel_precheck.sh```
