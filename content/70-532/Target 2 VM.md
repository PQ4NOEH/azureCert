+++
title = "Storage."
description = "Design and implement a storage and data strategy"
weight = 3
+++

## Summary
+ Final mark percentage: **30-35%**
+ content
    - Files
    - Blobs
    - Tables
    - Queues
    - Azure search

## Storage accounts
They are two types of storage accounts:

1. General. Allows you to storage
    - Blobs
    - Tables
    - Queues
2. Blobs. Only allows to store blobs files but in contrast gives you some beneficts:

### creating an storage account

Properties

1. Name
2. Deployment model (Resource manager || clasic)
3. Account kind
    - General purpose v1
    - General purpose v2
    - Blob
        - Block blob. Used to hold ordinary files up to 4.7 TB
        - page Blobs. Used to hold random access files up to 8 TB. These are used for the VHD files that back VMs.
        - Append blobs.These are like block blobs but optimized for append operations.
4. Performance. 
    - Standard (Magnetic drive)
    - Premium (Solid state drives). Only for VMs 99,9% even a out of an availavility set. Best suited for I/O intensive operation like Databases
5. Replication.
    - Locally-redundant storage (LRS). three copies.
    - Zone-redundant storage (ZRS clasic)
    - Geo-redundant storage (GRS)
    - Read-access geo-redundant storage (RA-GRS)
6. Secure transfer. Forces to use SSL
7. Subscription
8. Resource group
9. Location
10. Virtual network. Enabling this will grant exclusive access to the account from within the specified network and subnetworks.

### Azure blobs
Files in binary format. three types:
+ Block blob. Used to hold ordinary files up to 4.7 TB
+ page Blobs. Used to hold random access files up to 8 TB. These are used for the VHD files that back VMs.
+ Append blobs.These are like block blobs but optimized for append operations.

### Azure Files
Enables to set up highly avalaible network file shares that can be used using the SMB.
You can access the file from any part in the world using the url which includes the sas token.
File shares can be used in many common scenarios:

1. on-premises application.
2. Configuration files.
3. Diagnogtic logs, metrics or chrash dumps.

At this time AD-based authentication is not supported but is planned to be supported.


