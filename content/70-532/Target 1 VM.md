+++
title = "Create and manage azure resource manager resource machines."
description = "Virtual Machines"
weight = 2
+++

## Summary
+ Final mark percentage: **30-35%**


## Rought edges 10%
+ You can not set any OS on an Azure VM. If you need an OS which is not offered on the azure store then you can not use Azure VM to run that OS
+ Want the machine but do not want to pay OS fees (not posible).
+ Run software which is highly dependent on hardware configuration in order to give maximum performance.
+ Software which needs specific hardware configuration for example low procesor requirements but a very high RAM requirement.
+ Specific software configuration for example run the OS on other drive than the C one.

## role-access based security (RBAC)Each 

## Objetive 1.1 
Creating a VM presents the following options:

+ Deployment model (ARM | Clasic)
+ VM Name
+ VM User with a password of 12 to 16 characters long
+ Resource group (Existing|Create new)
+ Size
+ Availability set (ensures one machine of a set is allways up and runnnig to meet the 99.95 even under planned or unplanned maintenance scenearios)
+ Storage
    - Disk type (HDD || SSD)
    - Managed Disk (NO || YES)
+ Virtual network
    - Name
    - address space
    - subnet name
    - subnet address range
+ Public ip address (can set to none)
    - name
    - assignment (Dynamyc | Static)
+ Network Security Group (firewall) can be set to none
    - Name
    - Inbound rules. By default allows RDP wich means open port 3389 for  TCP connections to any machine.
    - Outbound rule
+ Auto-shutdown (off | on)
+ Monitoring
    - Boot diagnostics
    - Gest OS diagnostics
    - Diagnostics storage account
+ Backup


Creating a VM produces the following artifacts

+ VM
+ One Network interface
+ One public Address
+ One Virtual Network
+ One network security Group
+ One Storage Account
+ One Disk

Resource groups are for:

+ Payment control
+ Access control
+ Create alerts
+ View log files

Section Links

+ https://docs.microsoft.com/en-us/azure/virtual-machines/
+ https://docs.microsoft.com/en-us/azure/virtual-machines/windows/
+ https://docs.microsoft.com/en-us/azure/virtual-machines/virtual-machines-windows-ps-create?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json
+ https://docs.microsoft.com/en-us/azure/virtual-machines/virtual-machines-linux-quick-create-portal?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json

## 1.2 Desired state configuration
You can programatically set the configuration of a VM
**configuration drift**: Inconsistent configuration items (CIs) across computers or devices.

First thing we need is an automation account add==> monitoring + mamagement ==> Automation
Automation account ask for the following properties:

1. Name
2. Subscription
3. Resource group (create new | Use existing)
4. Location
5. Run as account (yes | no)

On the automation account we can 

1. add scripts under Configuration management ==> DSC configurations
2. Add resources to automate under Configuration management ==> DSC nodes
On the auto
 
### LINKS

+ https://docs.microsoft.com/en-us/azure/automation/automation-dsc-overview
+ https://docs.microsoft.com/en-us/azure/automation/automation-dsc-getting-started
+ https://docs.microsoft.com/en-us/azure/automation/automation-dsc-compile


## 1.3 Availability 

**Fault domain**. Hardware layer. Diferents racks
**Update domain**. Maintenance plans
**Virtual machines**

**Load balancer**
+ Type (public | internal)
+ Frontend pool
+ Backend Pools. add (VM | Availability set)