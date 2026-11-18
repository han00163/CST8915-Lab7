## YouTube Link: 





## 1. RabbitMQ issues:

### 1.1 Whether RabbitMQ is a stateless or stateful application?

RabbitMQ is a stateful application. It stores messages, queues and users on disk, but the lab's YAML deploys it as a Deployment with no persistent storage. 

### 1.2 The implications of running RabbitMQ without persistent storage? 

Without a persistent storage, RabbitMQ can only store messages, queues inside the container. In case of crash/re-start, information is lost.  

### 1.3 What happens when the RabbitMQ pod is deleted or restarted?

A new pod starts with a different name, as a brand-new RabbitMQ node with empty storage. All messages and queues are lost when RabbitMQ pod is deleted or restarted. 

### 1.4 Potential solutions to this problem(research-based)

- Have the app use durable queues and persistent messages. Storage alone isn’t enough, because a durable queue only means that the queue definition will survive a server restart, not the messages in it.

- Run RabbitMQ as a StatefulSet with a PersistentVolumeClaim.

- Run 3 replicas with quorum queues.

### 1.5 Does using Azure Service Bus solve the issues identified with RabbitMQ Configuration in this Lab? 

Mostly yes, for storage and availability. All Service Bus components, including compute, networking, and storage, are replicated across zones. 

The trade-off is a code rewrite, because Azure Service Bus and RabbitMQ's AMQP are on different versions. 



## 





