+++
title = "Storage blobs."
description = "Azure blobs storage"
weight = 5
+++


## General characterístics
A service to store large amount of unstructured object data(text||binary). The data can be access from anywhere in the word via HTTP or HTTPS.
Common uses:

1. Serving images or documents directly to a browser.
2. Storing files for distributed access.
3. Streaming video and audio.
4. Storing data for backup and restore.
5. Storing data for analysis.

### Concepts

**Account:** The accoun can be

+ General-purpose storage account. Two performance tiers
    - Standard: Supports tables, queues, files, block blobs, append blobs, page blobs and VHD
    - Premium: only VHD
+ Blob storage account. Only supports block blobs and append only blobs. Exposes two access tiers
    - Hot. Frequently accessed tier.
    - Cold.Infrequently accessed tier.
        + At least 30 days 
    - Archive.Infrequently accessed tier.
        + At least 180 days.
        + A file in the archive tier can not be read, copied or modified.
        + A file in the archive tier can be read metadata, deleted or rehidratated (can take up to 15 hours). 
        + The blob tier can be changed


**Container:** dsdsd

**Blob:** sdsds


