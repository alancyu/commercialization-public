---
title: Private Cloud Simulator for Windows Server 2016
description: Private Cloud Simulator for Windows Server 2016
MSHAttr:
- 'PreferredSiteName:MSDN'
- 'PreferredLib:/library/windows/hardware'
ms.assetid: D9E3FA7A-B5ED-4B1E-A78B-4788FDF91C3E
author: dawn.wood
ms.author: dawnwood
ms.date: 10/11/2018
ms.topic: article
---

# Private Cloud Simulator for Windows Server 2016

## <span id="Introduction"></span><span id="introduction"></span><span id="INTRODUCTION"></span>Introduction

The current industry trend is for private cloud solutions to comprise tightly integrated software and hardware components in order to deliver a resilient private cloud with high performance. Issues in any of the components (software, hardware, drivers, firmware, and so forth) can compromise the solution and undermine the promises made regarding a Service Level Agreement (SLA) for the private cloud.

Some of these issues are surfaced only under a high-stress, cloud-scale deployment, and are potentially hard to find using traditional standalone, component-focused tests. The Private Cloud Simulator is a cloud validation test suite that enables you to validate your component in a cloud scenario and identify these types of issues.

## Target Audience

The target audience for this document are those working towards validating their hardware for Windows Server 2016 Logo, Microsoft Azure Stack (MAS) solutions and Windows Server Software Defined (WSSD) datacenter offerings (that offer SDDC Standard, SDDC Premium Additional Qualifiers on the Windows Server Catalog).

| Component Type                          | Windows Server 2016 Logo | WSSD (SDDC Standard/Premium) | Azure Stack |
|-----------------------------------------|--------------------------|------------------------------|-------------|
| **Network Interface Cards (NICs)**      | Yes                      | Yes                          | Yes         |
| **SAS HBA**                             | No                       | Yes                          | Yes         |
| **Hard Disk Drives (HDD): SAS, SATA**   | No                       | Yes                          | Yes         |
| **Solid State Drives (SSD): SAS, SATA** | No                       | Yes                          | Yes         |
| **NVMe devices**                        | No                       | Yes                          | Yes         |
| **SCSI Enclosures**                     | No                       | Yes                          | Yes         |
| **Solutions**                           | Not Applicable           | Yes                          | Yes         |

In the future this guidance is expected to expand to cover the following device classes:

* iSCSI, FCOE, and Fiber Channel HBAs
* Storage Arrays

## Supporting Documents

*  [Failover-Clustering](https://technet.microsoft.com/en-us/library/hh831579.aspx)
*  [Windows Server 2016 Storage Spaces Direct cluster](https://technet.microsoft.com/en-us/library/mt693395.aspx)
*  [Microsoft Azure Stack Logo Requirements](http://aka.ms/getreq) released via Microsoft Collaborate to Microsoft partners

## Test Overview

Private Cloud Simulator (PCS) simulates a live datacenter/private cloud by creating VM workloads, simulating data center operations (load balancing, software/hardware maintenance), and injecting compute/storage faults (unplanned hardware/software failure). PCS uses a Microsoft SQL Server database to record test and solution data during the run. It then presents a report that includes operation pass/fail rates and logs whihch provide the capability to correlate data for pass/fail determination and failure diagnosis (as applicable).

### Topology

PCS lab environment contains the following elements:

* An Active Directory domain controller/DNS/DHCP server for the test domain.
  * You can find information about Active Directory at <https://msdn.microsoft.com/library/bb727067.aspx>
  * [Active Directory Domain Services Functional Levels](https://technet.microsoft.com/en-us/library/understanding-active-directory-functional-levels.aspx) needs to be Windows Server 2012 or higher.
* A dedicated HLK controller machine.
* A dedicated PCS controller machine.
* A minimum 3-node compute cluster, which hosts Hyper-V virtual machines.

Notes:

* All the above machines must be joined to the same test domain.
* All PCS tests need to be run as the same user in the 'Domain Admins' group for the test domain.
* Use the same user with Domain Admin credentials to install the HLK controller.

### HLK Controller System Requirements

Minimum system requirements are as shown in the table below.

| Resource                | Minimum requirement            |
|-------------------------|--------------------------------|
| CPU (or vCPU)           | 4 cores                        |
| Memory                  | 12 GB RAM                      |
| Available disk space    | 200 GB                         |
| Operating system        | Windows Server 2016 Datacenter |
| Active Directory domain | Join it to the test domain     |

### Setup HLK 

* Follow the [Windows HLK Getting Started guide](https://msdn.microsoft.com/library/windows/hardware/dn915002) to [download](https://developer.microsoft.com/windows/hardware/windows-hardware-lab-kit) and install HLK controller software.
* Download the supplemental content package file **PCSFiles.vhd** for Windows Server 2016 from the [HLK website](https://developer.microsoft.com/en-us/windows/hardware/windows-hardware-lab-kit).
* Copy the **PCSFiles.vhd** file to the **Tests\\amd64** test folder on the HLK Controller. Below is the default path for an HLK installation:

    `C:\Program Files (x86)\Windows Kits\10\Hardware Lab Kit\Tests\amd64`

### Get IOMeter files

* IOMeter is a workload that must be installed on the HLK controller.
* Download the i386 Windows version of IOMeter release dated 2006.07.27 from the IOMeter website.
* Run the setup (or unzip the package) to unpack the files.
* Copy **IOMeter.exe**, **Dynamo.exe** to **Tests\\amd64\\pcs\\GuestScenarioManager\\IOMeter** folder on the HLK controller. Below is the default path for an HLK installation:
    
    `C:\Program Files (x86)\Windows Kits\10\Hardware Lab Kit\Tests\amd64\pcs\GuestScenarioManager\IOMeter`

### PCS Controller System Requirements

Minimum system requirements are as shown in the table below.

| Resource                     | Minimum requirement            |
|------------------------------|--------------------------------|
| CPU (or vCPU)                | 4 cores                        |
| Memory                       | 12 GB RAM                      |
| Free space on the boot drive | 200 GB                         |
| Operating system             | Windows Server 2016 Datacenter |
| Active Directory domain      | Join it to the test domain     |

### Setup PCS

* PCS controller MUST be a Generation v2 VM or a physical machine.
* **Secure Boot** and **BitLocker** MUST be disabled. This is required because PCS enables **TestSigning** boot configuration. If you are using Generation 2 Hyper-V VM as PCS controller, stop the VM to disable Secure Boot in the VM's settings.
* Install the HLK Client using the [Windows HLK Getting Started guide](https://msdn.microsoft.com/library/windows/hardware/dn915002) and open the requisite ports.
* Install .NET Framework 3.5 (This feature is not included by default in Windows Server 2016).
  * Generic Installation Instructions can be found at the following locations:
    * <https://msdn.microsoft.com/library/hh506443>
    * <https://msdn.microsoft.com/library/windows/desktop/hh848079>
  * For builds released via Microsoft Connect, see details below:
    * Mount the ISO supplied with the build and find the file at **MountedDriveLetter:\\sources\\sxs\\microsoft-windows-netfx3-ondemand-package.cab**
    * Copy the file to a local folder on the PCS controller
    * Install the package by executing this command line using admin privileges      
      ```
      PS> Add-WindowsFeature Net-Framework-Features -source <Local Folder>
      ```

aa

### Run PCS tests from Windows HLK




