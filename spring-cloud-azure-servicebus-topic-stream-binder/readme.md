# Spring Cloud Azure Service Bus Topic Stream Binder

The project provides **Spring Cloud Stream Binder for Azure Service Bus Topic** which allows you to build message-driven 
microservice using **Spring Cloud Stream** based on [Azure Service Bus Topic](https://azure.microsoft.com/en-us/services/service-bus/) service.

## Service Bus Topic Binder Overview

The Spring Cloud Stream Binder for Azure Service Bus Topic provides the binding implementation for the Spring Cloud Stream.
This implementation uses Spring Integration Service Bus Topic Channel Adapters at its foundation. 

### Consumer Group

Service Bus Topic provides similar support of consumer group as Apache Kafka, but with slight different logic.
This binder rely on `Subscription` of a topic to act as a consumer group.

### Partitioning Support

This binder implementation has no partition support even service bus topic supports partition.

## Samples 

Please use this [sample](../spring-cloud-azure-samples/spring-cloud-azure-servicebus-topic-binder-sample/) as a reference
for how to use this binder in your projects. 

## Feature List 

- [Dependency Management](#dependency-management)
- [Configuration Options](#configuration-options)

### Dependency Management

**Maven Coordinates** 
```
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>spring-cloud-azure-servicebus-topic-stream-binder</artifactId>
</dependency>

```
**Gradle Coordinates** 
```
dependencies {
    compile group: 'com.microsoft.azure', name: 'spring-cloud-azure-servicebus-topic-stream-binder'
}
```

### Configuration Options 

The binder provides the following configuration options in `application.properties`.

#### Spring Cloud Azure Properties ####

Name | Description | Required | Default 
---|---|---|---
spring.cloud.azure.credential-file-path | Location of azure credential file | Yes |
spring.cloud.azure.resource-group | Name of Azure resource group | Yes |
spring.cloud.azure.region | Region name of the Azure resource group, e.g. westus | Yes | 
spring.cloud.azure.servicebus.namespace | Service Bus Namespace. Auto creating if missing | Yes |

#### Serivce Bus Topic Producer Properties ####

It supports the following configurations with the format of `spring.cloud.stream.servicebus.bindings.<channelName>.producer`.

**_sync_**

Whether the producer should act in a synchronous manner with respect to writing records into a stream. If true, the 
producer will wait for a response after a send operation.

Default: `false`

**_sendTimeout_**

Effective only if `sync` is set to true. The amount of time to wait for a response after a send operation, in milliseconds.

Default: `10000`
 
#### Service Bus Topic Consumer Properties ####

It supports the following configurations with the format of `spring.cloud.stream.servicebus.bindings.<channelName>.consumer`.

**_checkpointMode_**

The mode in which checkpoints are updated.
If `RECORD`, checkpoints occur after each record is received by Spring Channel.
If `MANUAL`, checkpoints occur on demand by the user via the `Checkpointer`. You can get `Checkpointer` by `Message.getHeaders.get(AzureHeaders.CHECKPOINTER)`callback.

Default: `RECORD`
