---
layout: post
title:  "Converting AWS AMI to OVF"
date:   2020-08-29 01:00:00 +0100
categories: [vmware]
description: ""
image:
  feature: aws.png
  credit:
---

This is a short post covering the steps to convert an AWS AMI to a VMDK.

I recently had an issue in extracting an AMI from AWS. In performing this form of conversion there are a number of steps that need to be taken to ensure that the 

Firstly, follow the instructions at [https://docs.aws.amazon.com/vm-import/latest/userguide/v](https://docs.aws.amazon.com/vm-import/latest/userguide/vmexport_image.html) in order to export a vmdk to an S3 bucket.

Important notes here are to make this S3 bucket accessible by the vmimport role, that this guide requires. In addition, ensure that (depending on the region) the account id's detailed in [this link](https://docs.aws.amazon.com/vm-import/latest/userguide/vmexport.html) are added to the S3 bucket with full permissions.

Once this is all complete, which may take a few hours, download the resultant vmdk.

Next, run the following command over the exported and downloaded vmdk:
```
C:\Program Files (x86)\VMware\VMware Workstation>vmware-vdiskmanager.exe -r C:/Users/booj/Downloads/export-ami-abcdef.vmdk -t 0 C:/Users/booj/Downloads/out.vmdk
```

Finally, mount the vmdk resultant from the above command as the primary boot volume of a VMWare Workstation VM.  Ensure BIOS (not UEFI) is selected during the VM creation. Now simply export this VM.
