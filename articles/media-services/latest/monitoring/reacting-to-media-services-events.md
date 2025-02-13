---
title: Reacting to Azure Media Services events 
description: This article describes how to use Azure Event Grid to subscribe to Media Services events. 
services: media-services
documentationcenter: ''
author: IngridAtMicrosoft
manager: femila
editor: ''

ms.service: media-services
ms.workload: 
ms.topic: conceptual
ms.date: 07/08/2021
ms.author: inhenkel
---
 
# Handling Event Grid events

[!INCLUDE [media services api v3 logo](../includes/v3-hr.md)]

Media Services events allow applications to react to different events (for example, the job state change event) using modern serverless architectures. It does so without the need for complicated code or expensive and inefficient polling services. Instead, events are pushed through [Azure Event Grid](https://azure.microsoft.com/services/event-grid/) to event handlers such as [Azure Functions](https://azure.microsoft.com/services/functions/), [Azure Logic Apps](https://azure.microsoft.com/services/logic-apps/), or even to your own Webhook, and you only pay for what you use. For information about pricing, see [Event Grid pricing](https://azure.microsoft.com/pricing/details/event-grid/).

Availability for Media Services events is tied to Event Grid [availability](../../../event-grid/overview.md) and will become available in other regions as Event Grid does.  

## Media Services events and schemas

Event grid uses [event subscriptions](../../../event-grid/concepts.md#event-subscriptions) to route event messages to subscribers. Media Services events contain all the information you need to respond to changes in your data. You can identify a  Media Services event because the eventType property starts with "Microsoft.Media.".

For more information, see [Media Services event schemas](../media-services-event-schemas.md).

## Samples and How-to

The Media Services [samples repository for .NET](https://github.com/Azure-Samples/media-services-v3-dotnet) demonstrates how to use the latest Event Grid and Event Hubs client libraries to receive events in your own custom applications.

In addition, the following how-to articles demonstrate the use of Event Grid through the CLI and Azure portal.

* [Monitor events - portal](../monitor-events-portal-how-to.md)
* [Monitor events - CLI](../job-state-events-cli-how-to.md)

## Practices for consuming events

Applications that handle Media Services events should follow a few recommended practices:

* As multiple subscriptions can be configured to route events to the same event handler, it is important not to assume events are from a particular source, but to check the topic of the message to ensure that it comes from the storage account you are expecting.
* Similarly, check that the eventType is one you are prepared to process, and do not assume that all events you receive will be the types you expect.
* Ignore fields you don’t understand.  This practice will help keep you resilient to new features that might be added in the future.
* Use the "subject" prefix and suffix matches to limit events to a particular event.

> [!NOTE]
> Events are subject to the Event Grid [Service Level Agreement (SLA)](https://azure.microsoft.com/support/legal/sla/event-grid/v1_0/). If you want to get event notifications using APIs, see examples on how to consume events, with [.NET SDK](https://github.com/Azure-Samples/media-services-v3-dotnet) or [Java SDK](https://github.com/Azure-Samples/media-services-v3-java).

## Next steps

* [Monitor events - portal](../monitor-events-portal-how-to.md)
* [Monitor events - CLI](../job-state-events-cli-how-to.md)
