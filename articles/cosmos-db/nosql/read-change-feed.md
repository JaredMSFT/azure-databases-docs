---
title: Read Azure Cosmos DB Change Feed
description: Learn how to work with the change feed in Azure Cosmos DB by using either a push model or a pull model.
author: markjbrown
ms.author: mjbrown
ms.service: azure-cosmos-db
ms.subservice: nosql
ms.custom: build-2023
ms.topic: how-to
ms.date: 07/14/2025
---

# Read the Azure Cosmos DB change feed
[!INCLUDE[NoSQL](../includes/appliesto-nosql.md)]

You can work with the Azure Cosmos DB change feed by using either a push model or a pull model. With a *push* model, the change feed processor pushes work to a client that has business logic for processing this work. However, the complexity in checking for work and storing state for the last processed work is handled within the change feed processor.

With a *pull* model, the client has to pull the work from the server. The client, in this case, not only has business logic for processing work but also for storing state for the last processed work, handling load balancing across multiple clients processing work in parallel, and handling errors.

When reading from the Azure Cosmos DB change feed, we usually recommend using a push model because you don't need to worry about:

- Polling the change feed for future changes.
- Storing state for the last processed change. If you read from the change feed processor, state is automatically stored in a [lease container](change-feed-processor.md#components-of-the-change-feed-processor).
- Load balancing across multiple clients consuming changes. For example, if one client can't keep up with processing changes and another has available capacity.
- [Handling errors](change-feed-processor.md#error-handling). For example, automatically retrying failed changes that weren't correctly processed after an unhandled exception in code or a transient network issue.

Most scenarios that use the Azure Cosmos DB change feed use one of the push model options. However, there are some scenarios where you might want the extra low-level control of the pull model. These include:

- Reading changes from a particular partition key.
- Controlling the pace at which your client receives changes for processing.
- Doing a one-time read of the existing data in the change feed (for example, to do a data migration).

## Read change feed with a push model

Using a push model is the easiest way to read from the change feed. There are two ways you can read from the change feed with a push model: [Azure Functions triggers](change-feed-functions.md) and the [change feed processor](change-feed-processor.md). Azure Functions uses the change feed processor behind the scenes, so these are both similar ways to read the change feed. Think of Azure Functions as simply a hosting platform for the change feed processor, not an entirely different way of reading the change feed.

### Azure Functions

Azure Functions is the simplest option if you're just getting started using the change feed. Due to its simplicity, it's also the recommended option for most change feed use cases. When you create an Azure Functions trigger for Azure Cosmos DB, you select the container to connect, and the Azure Function gets triggered whenever there's a change in the container. Because Azure Functions uses the change feed processor behind the scenes, it automatically parallelizes change processing across your container's [partitions](../partitioning-overview.md).

Developing with Azure Functions is an easy experience and can be faster than deploying the change feed processor on your own. Triggers can be created by using the Azure Functions portal or programmatically using SDKs. Visual Studio and VS Code provide support to write Azure Functions, and you can even use the Azure Functions CLI for cross-platform development. You can write and debug the code on your desktop, and then deploy the function with one button. To learn more, see [Serverless database computing using Azure Functions](serverless-computing-database.md) and [Using change feed with Azure Functions](change-feed-functions.md).

### Change feed processor library

#### Supported SDKs

|  .NET V3  |   Java    |  Node.JS  |  Python   |
| --------- | --------- | --------- | --------- |
|     ✓     |    ✓     |     ✕     |    ✕     |

The change feed processor gives you more control over the change feed and still hides most complexity. The change feed processor library follows the observer pattern, where your processing function is called by the library. The change feed processor automatically checks for changes and, if changes are found, *pushes* them to the client. If you have a high throughput change feed, you can instantiate multiple clients to read the change feed. The change feed processor automatically divides the load among the different clients. You don't have to implement any logic for load balancing across multiple clients or any logic to maintain the lease state.

The change feed processor guarantees an *at-least-once* delivery of all of the changes. In other words, if you use the change feed processor, your processing function is called successfully for every item in the change feed. If there's an unhandled exception in the business logic in your processing function, the failed changes are retried until they're processed successfully. To prevent your change feed processor from getting *stuck* continuously retrying the same changes, add logic in your processing function to write documents, upon exception, to a dead-letter queue. To learn more, see [Error handling](change-feed-processor.md#error-handling).

In Azure Functions, the recommendation for handling errors is the same. You should still add logic in your delegate code to write documents, upon exception, to a dead-letter queue. However, if there's an unhandled exception in your Azure Function, the change that generated the exception isn't automatically retried. If there's an unhandled exception in the business logic, the Azure Function moves on to processing the next change. The Azure Function doesn't retry the same failed change.

Like Azure Functions, developing with the change feed processor library is easy. However, you're responsible for deploying one or more hosts for the change feed processor. A host is an application instance that uses the change feed processor to listen for changes. While Azure Functions has capabilities for automatic scaling, you're responsible for scaling your hosts. To learn more, see [using the change feed processor](change-feed-processor.md#dynamic-scaling). The change feed processor library is part of the [Azure Cosmos DB SDK V3](https://github.com/Azure/azure-cosmos-dotnet-v3).

## Read the change feed with a pull model

The [change feed pull model](change-feed-pull-model.md) allows you to consume the change feed at your own pace. Changes must be requested by the client and there's no automatic polling for changes. If you want to permanently *bookmark* the last processed change (similar to the push model's lease container), you need to [save a continuation token](change-feed-pull-model.md#save-continuation-tokens).

Using the change feed pull model, you get more low-level control of the change feed. When reading the change feed with the pull model, you have three options:

- Read changes for an entire container.
- Read changes for a specific [FeedRange](change-feed-pull-model.md#use-feedrange-for-parallelization).
- Read changes for a specific partition key value.

You can parallelize the processing of changes across multiple clients, just as you can with the change feed processor. However, the pull model doesn't automatically handle load-balancing across clients. When you use the pull model to parallelize processing of the change feed, you'll first obtain a list of FeedRanges. A FeedRange spans a range of partition key values. You need to have an orchestrator process that obtains FeedRanges and distributes them among your machines. You can then use these FeedRanges to have multiple machines read the change feed in parallel.

There's no built-in *at-least-once* delivery guarantee with the pull model. The pull model gives you low-level control to decide how you would like to handle errors.

## Change feed in APIs for Cassandra and MongoDB

Change feed functionality is surfaced as change streams in API for MongoDB, and query with predicate in API for Cassandra. To learn more about the implementation details for API for MongoDB, see [Change streams in Azure Cosmos DB’s API for MongoDB](../mongodb/change-streams.md).

Native Apache Cassandra provides change data capture (CDC), a mechanism to flag specific tables for archival and rejecting writes to those tables once a configurable size-on-disk for the CDC log is reached. The change feed feature in Azure Cosmos DB for Apache Cassandra enhances the ability to query the changes with predicate via CQL. To learn more about the implementation details, see [Change feed in the Azure Cosmos DB for Apache Cassandra](../cassandra/change-feed.md).

## Next steps

* [Overview of change feed](../change-feed.md)
* [Serverless event-based architectures with Azure Cosmos DB and Azure Functions](change-feed-functions.md)
* [Using change feed processor library](change-feed-processor.md)
