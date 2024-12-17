---
layout: post
title: "Cloud Architecture Design Patterns"
author: "Leonardo Marques"
categories: course
tags: [software, cloud]
image: cloud-design/cloud.png
---

|
[Course](https://www.coursera.org/learn/cloud-architecture-design-patterns)
|

## Introduction to Cloud Architecture

Cloud architecture is essentially the blueprint of how various technologies and services come together to create a Cloud environment. Imagine it as a city plan where data centers are buildings, and networking components are the roads connecting them.

- *Infrastructure as a Service (IaaS)*: Similarly, with infrastructure as a service, you get the virtualized hardware and storage, but you have to manage everything else.

- *Platform as a Service (PaaS)*: you get the hardware and software tools necessary to develop the applications you need.

- *Software as a Service (IaaS)*: Everything is provided for you and you just enjoy the service. Examples include Google Workspace and Microsoft Office 365.

**Cloud Computing Advantages**
- Cloud services allow you to easily scale resources up or down based on the map.

- Liminating the need for a physical hardware and maintenance.
- Disaster recovery and backup.
- Automatic updates and patches.

**Cloud Computing Challenges**
- Security and privacy.
- Downtime and reliability.
- Complicate compliances when storing data in the Cloud.

#### Article: [Introduction to Cloud Computing: Concepts, Models, Characteristics & Benefits](https://www.upgrad.com/blog/introduction-to-cloud-computing/)


## Core Cloud Design Patterns

### Load Balancer Pattern

- A load balancer is a critical component in Cloud architecture that distributes incoming network traffic across multiple servers.

- This ensures that no single server becomes overwhelmed, improving both the performance and reliability of your applications.
- Load balancers optimize resource use, maximize through output, minimize response time, and avoid overload on any single resource

![load balancer](/assets/img/cloud-design/load-balancer.png)

### Circuit Breaker Pattern

- A crucial design pattern for managing failures and maintaining system stability.

- These patterns are design patterns used to detect failures and encapsulate the logic of preventing a failure from constantly reoccurring, which can lead to cascading failures across multiple systems

***Circuit breaker typically has three states:***

- *Closed*: the circuit breaker is in normal operation mode, allowing all requests to pass through.
- *Open*: when the failure threshold is reached, the circuit opens, blocking all requests to the failing service.

- *Half-Open*: after predefined timeout, the circuit breaker allows a limited number of test request to check if the service has recovered

***Circuit breakers work***
- *Failure Detection*: When a service call fails repeatedly, the circuit breaker records these failures. If the number of the failures exceed the threshold, the circuit breaker trips and moves to the open state.

- *Fallback Mechanism*: When in the open state, circuit breaker can invoke fallback logic, such as a returning to a default response or cached value.

- *Recovery Testing*: After a timeout, the circuit breaker enters a half open state and sends a few test requests to check if the service is back to normal. If the test requests succeed, the circuit breaker resets to the closed state, if they fail, it reopens.

![circuit breaker](/assets/img/cloud-design/circuit-breaker.png)

### Auto-Scaling Pattern

- The auto scaling pattern allows Cloud applications to automatically adjust the amount of computational resources based on the current load.

- This ensures that applications can handle increased demands while optimizing costs during periods of low activity.

![auto scaling](/assets/img/cloud-design/auto-scaling.png)


#### Article: [Cloud Design Patterns: An Overview](https://medium.com/@vinciabhinav7/cloud-design-patterns-an-overview-part-1-41a0c3edc227)


## Advanced Cloud Design Patterns

### Microservices Architecture

- Microservices architecture is an approach to applications development where a large scale application is built as a suit of a small, independently deployable services.

- Each service run its own process and communicates through lightweight mechanisms.

- Often HTTP based API.

***Key Principles of Microservices***

- *Single Responsibility*: Each microservice is designed to perform a specific business function, ensuring clear separation of concerns.

- *Independence*: Microservices operate independently, allowing for individual deployment, scaling, and updating without affecting the entire system.

- *Decentralized Data Management*: Each microservices manage its own database promoting data encapsulation and reducing tight coupling between services.

- *Communication*: Services communicate through well defined APIs, often using restful HTTP or messaging queues.

![microservices](/assets/img/cloud-design/microservice.png)


### Event-Driven Architecture

- Event-driven architecture, or EDA for short, is a design pattern where the flow of the program is determined by the events such as user actions, sensor outputs or messages from other programs or services.

- It allows for asynchronous communication between different parts of an application.

***Key Principles of EDA***

- *Event Producers*: Components that generate events when something notable happens, for example a user clicks a button or a sensor detects a change.

- *Event Consumers*: Components that a lesson for an approach event, Consumers can trigger further actions for workflow in response to events.

- *Event Channels*: Pathways to which events are transmitted from producers to consumers, this can include message queues or event streams.

- *Event Processing*: Events can be processed in real-time or stored for later processing depending on the applications needs, the icing on the cake are the benefits of event-driven architecture.

**One of the benefits being scalability. It decouples producers and consumers allowing each to scale independently based on demand. Also we have to take into consideration the flexibility. It enhances modularity and reusability by allowing components to be easily added, removed or modified without affecting others.**

![EDA](/assets/img/cloud-design/event-driven.png)


### Serverless Architecture

- Serverless architecture is a cloud computing execution model where the cloud provider dynamically manages the infrastructure.

- You write the code and define the triggers, and the provider handles everything else, including scaling, patching, and managing servers.

*Key Principles of Serverless Architecture*

- *Function as a Service*: Developers deploy individual functions rather than the entire applications, Functions are invent driver and execute in response to the specific triggers.

- *Backend as a Service*: We can use third-party services for backend functionality, such as authentication, databases, and storage without managing the underlying infrastructure, then we have automatic scaling, resources automatically scale up or down based on the map, ensuring optimal performance and cost efficiency.

- *Event Driven Execution*: Functions are triggered by events, such as HTTP requests, database changes, or message queues, promoting decoupled and reactive systems.

![serveless](/assets/img/cloud-design/serveless.png)

![serveless-2](/assets/img/cloud-design/serveless2.png)


#### Article: [Serverless Microservices Overview](https://www.datadoghq.com/knowledge-center/serverless-architecture/serverless-microservices/)