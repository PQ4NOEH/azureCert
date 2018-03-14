+++
title = "Storage queues."
description = "Azure queue storage"
weight = 4
+++


## General characterístics
Used to store and retrieve messages. Characteristics include:

+ A message can have up to 64KB.
+ Maximum message TTL 7 days.
+ A queue may contain up to 500TB.
+ May track message processing progress.
+ A log with all transaction done over the messages is manteined.
+ A queue may contain millions of messages.
+ The queue does not guaranty delivery order.
+ At least once
+ No duplicate detection
+ You Batched receive up to 32 messages
+ pulling subscriber
+ scheduled delivery
+ Queue auto-forwarding
+ Update message content
+ poison message support. Using DequeueCount property of a message
+ If the content of the message is not XML-safe, then it must be Base64 encoded. If you Base64-encode the message, the user payload can be up to 48 KB, instead of 64 K
+ A message might me peeked
+ A queue allows arbirary key/value pair appended to the queue description.
+ Authentication is done via Symmetric key
+ Security model Delegated access via SAS tokens
+ Do not support Identity provider federation

## Queue Level Operations
### Configuration
```xml
    <add key="StorageConnectionString" value = "UseDevelopmentStorage=true;"/> 
    <add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=[AccountName];AccountKey=[AccountKey]" />
```
### Connect
```C#
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(_storageConnectionString);
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    return queueClient.GetQueueReference(_queueName);
```
### Create
```C#
    queue.CreateIfNotExistsAsync();
```
### Delete
```C#
    queue.DeleteAsync();
```
### Count number of messages
```C#
    queue.ApproximateMessageCount;
```
### Set queue metadata
```C#
    queue.Metadata.Add("key1", "value1");
    queue.Metadata.Add("key2", "value2");
    await queue.FetchAttributesAsync();
```
### Set ACL 
```C#
    SharedAccessQueuePolicy accessQueuePolicy = new SharedAccessQueuePolicy();
    accessQueuePolicy.SharedAccessStartTime = new DateTimeOffset(DateTime.Now);
    accessQueuePolicy.SharedAccessExpiryTime = new DateTimeOffset(DateTime.Now.AddMinutes(10));
    accessQueuePolicy.Permissions = SharedAccessQueuePermissions.Update;
    QueuePermissions permissions = new QueuePermissions();
    permissions.SharedAccessPolicies.Add("key1", accessQueuePolicy);
    await queue.SetPermissionsAsync(permissions);
```
### Get ACL
```C#
    await queue.GetPermissionsAsync();
```
### Manage Cors 
```C#
    CorsRule corsRule = new CorsRule
    {
        AllowedHeaders = new List<string> {"*"},
        AllowedMethods = CorsHttpMethods.Get,
        AllowedOrigins = new List<string> {"*"},
        ExposedHeaders = new List<string> {"*"},
        MaxAgeInSeconds = 3600
    };

    ServiceProperties serviceProperties = await queueClient.GetServicePropertiesAsync();
    serviceProperties.Cors.CorsRules.Add(corsRule);
    await queueClient.SetServicePropertiesAsync(serviceProperties);
```
## Message level operations
### Peek
#### One message
```C#
    queue.PeekMessageAsync();
```
#### Up to 32 messages
```C#
    queue.PeekMessagesAsync(5);
```

### Dequeue
#### One message
Has to be done in two steps:

1. Get the message. this will make the message invisible to other listeners (by default 30 seconds, you can specify the time.)
2. Delete the message.

This two phase approach is great because you can recover in case of failure, power of or any reason.
```C#
    var message = queue.GetMessageAsync();
    //message procesing code
    queue.DeleteMessageAsync(message);
```
#### Up to 32 messages
```C#
    foreach(var message = queue.GetMessagesAsync(32))
    {
        //message procesing code
        queue.DeleteMessageAsync(message);
    }
```

### Update message
```C#
    CloudQueueMessage message = await queue.GetMessageAsync();
    message.SetMessageContent("Updated contents.");
    await queue.UpdateMessageAsync(
                message,
                TimeSpan.Zero,  // For the purpose of the sample make the update visible immediately
                MessageUpdateFields.Content |
                MessageUpdateFields.Visibility);
```
