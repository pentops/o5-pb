Messaging
=========

Messaging defines the way applications share data. There are three topologies available, defined below.

Applications are called Workers when they are the recipient of messages, and Senders when they are the sender.

Workers expose gRPC endpoints for each group of messages they receive, and an rpc endpoint for each specific message type.

The gRPC definition for all messaging endpoints must return `google.protobuf.Empty` - even for Reply type queues - as no service should ever be waiting for a reply. 

```proto
service FooTopic {
  option (pentops.messaging.v1.config).broadcast.topic_name = "foo";
  rpc Bar(BarMessage) returns (google.protobuf.Empty);
}
```

Senders fall into two broad categories: Those with databases and those without.

Any sender with a database should use the [Outbox pattern](https://microservices.io/patterns/data/transactional-outbox.html), where outbound messages are stored in a table, and committed atomically with other database changes. The platform will then take messages from the outbox table and send the message through the messaging infrastructure.

Senders without databases, e.g. a translation service, or even senders which have a database but do not mutate state in message processing (e.g. a read-only lookup reply) can instead send messages to the messaging infrastrcutre using gRPC requests intercepted by the platform. The platform will expose the gRPC service as defined in the protos and foward the messages as required. The platform returns OK + Empty when the message has been safely stored in the messaging infrastructure.

## Broadcast

![Broadcast Topology](https://user-images.githubusercontent.com/1665328/236639414-c8e07738-b2ff-4769-91b7-ff741a267884.png)

- Zero or more Sender applications
- Exactly one 'Topic'
- Zero or more Worker applications
  - One Queue per Worker application

## Unicast

![Unicast Topology](https://user-images.githubusercontent.com/1665328/236639416-86a7f6db-30c9-4b21-8113-1bf6c0fdacc2.png)

- Zero or more Sender applications
- Exactly one Worker application
- Exactly one Queue

## Reply

![Reply Topology](https://user-images.githubusercontent.com/1665328/236639378-bfbef3bf-e2ab-4f12-bf7e-fa5b1c856440.png)

- Exactly one Worker application
- Exactly one Input Queue
- Zero or more Sender applications
  - One Reply queue per Sender application
  
