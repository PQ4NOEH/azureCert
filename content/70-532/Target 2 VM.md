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

## Replication
The data in a storage account is allways repliated to ensure durability and high availability.
Replication ensures that your storage account meet the SLA even in the face of failure.

### Terms

**Storage scale unit:** Collection of racks of storage nodes.
**Fault domain (FD):** Group of units that represents a physical unit of failure.
**Upgrade Domain (UD):** Group of nodes that are upgraded together during the process of a service upgrade (Rollout).
**Recover Point Objetive (RPO):**  The number of minutes of potential data lost. Indicates the point in time to which data can be recovered. Azure Storage typically has an RPO of less than 15 minutes, although there is currently no SLA on how long geo-replication takes.
**Recovery Time Objective (RTO):** Measure of how long it takes to perform the failover and get the storage account back online. It includes the following actions


Replication options:

1. Locally redundant storage (LRS)
    - Replicated accross multiple centers: NO
    - Data can be be read from a secondary location as well as primary: NO
    - Objects durability over a year: 11 9´s
    - Write request ACK´s when all replicas commited
    - replicas in != domains and != update domains within one storage scale unit
    - Recomended
        + Highest maximum bandwidth of Azure Storage replication options
        + Stores data that can be easily reconstructed
        + Replicating data only within a country due to data governance requirements. Paired region
2. Zone-redundant storage (ZRS)
    - Inserts and updates to data are made synchronously and are strongly consistent.
    - Designed to simplify the development of highly available applications.
    - Replicated accross multiple centers: YES
    - Data can be be read from a secondary location as well as primary: NO
    - Objects durability over a year: 12 9´s
    - Enables customers to read and write data even if a single zone is unavailable or unrecoverable
    - Recomended:
        + Scenarios like transactional applications where downtime is not acceptable.
3. Geo-redundant storage (GRS)
    - An update is first committed to the primary region. Then the update is replicated asynchronously to the secondary region, where it is also replicated.
    - Replicated accross multiple centers: YES
    - Data can be be read from a secondary location as well as primary: NO
    - Objects durability over a year: 16 9´s
    - Considerations
        + In the event of a regional disaster it is posible to not have all changes migrated to the secondary region.
        + The replica is not available unless Microsoft initiates failover to the secondary region.
        + Secondary region is elected following region pairings
4. Read-access Geo-redundant storage (GRS)
    - Replicated accross multiple centers: YES
    - Data can be be read from a secondary location as well as primary: YES
    - Objects durability over a year: 16 9´s
    - considerations:
        + To access the second region append the suffix "-secondary" to the name of your account
        + Application has to manage the endpoint interaction
        + In the event of a regional disaster it is posible to not have all changes migrated to the secondary region.
        + When Microsoft initiates failover to the secondary region you will have RW access





