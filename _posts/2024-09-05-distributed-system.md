---
layout: post
title: "Distributed Systems Design Fundamentals"
author: "Leonardo Marques"
categories: course
tags: [software, computer science]
image: distributed-system/ds-udi.jpg
---

[Course](https://learn.particular.net/courses/distributed-systems-design-fundamentals-online)

Welcome to the Distributed Systems Design Fundamentals course.

This course is part of a five-day recorded training. We believe this course will change how you think about distributed systems design and give you the confidence to make architectural and technological choices.

Enjoy!

Udi Dahan and the Team
in Particular

---

## Fallacies of Distributed Computing

Decades of distributed systems development have taught us many lessons. In this module, Udi covers many historical mistakes as well as proven best practices for scalable and robust design. (click on the videos below)

- [Fallacy #1: The network is reliable](https://particular.net/blog/the-network-is-reliable)

[![Fallacy #1](https://i.ytimg.com/vi/8fRzZtJ_SLk/maxresdefault.jpg)](https://www.youtube.com/watch?v=8fRzZtJ_SLk&list=PL1DZqeVwRLnD3EjyciYAO82dT9Owiq8I5)

- [Fallacy #2: Latency is zero](https://particular.net/blog/latency-is-zero)

[![Fallacy #2](https://i.ytimg.com/vi/fgu5hM4CI6g/maxresdefault.jpg)](https://www.youtube.com/watch?v=fgu5hM4CI6g&list=PL1DZqeVwRLnD3EjyciYAO82dT9Owiq8I5&index=2)

- [Fallacy #3: Bandwidth is infinite](https://particular.net/blog/bandwidth-is-infinite)

[![Fallacy #3](https://i.ytimg.com/vi/t02qwodryNk/hq720.jpg?sqp=-oaymwEhCK4FEIIDSFryq4qpAxMIARUAAAAAGAElAADIQj0AgKJD&rs=AOn4CLBuLNaL5YbLjRg-4KYnWH8abeDMqg)](https://www.youtube.com/watch?v=t02qwodryNk&list=PL1DZqeVwRLnD3EjyciYAO82dT9Owiq8I5&index=3)

- [Fallacy #4: The network is secure](https://particular.net/blog/the-network-is-secure)

[![Fallacy #4](https://media.licdn.com/dms/image/D5610AQELTkv_Q-XFUg/image-shrink_800/0/1716531325883?e=2147483647&v=beta&t=c9azCzriezUZtOY3VhrFXZJDrOynISRj2Xu43LBEpBk)](https://www.youtube.com/watch?v=ctryjSB_KZ0&list=PL1DZqeVwRLnD3EjyciYAO82dT9Owiq8I5&index=4)

- [Fallacy #5: Topology doesn't change](https://particular.net/blog/topology-doesnt-change)

[![Fallacy #5](https://i.ytimg.com/vi/SF6qwCaHGOM/sddefault.jpg)](https://www.youtube.com/watch?v=SF6qwCaHGOM&list=PL1DZqeVwRLnD3EjyciYAO82dT9Owiq8I5&index=5)

- [Fallacy #6: There is one administrator](https://particular.net/blog/there-is-one-administrator)

[![Fallacy #6](https://i.ytimg.com/vi/HJusnKtkjFY/hqdefault.jpg)](https://www.youtube.com/watch?v=HJusnKtkjFY&list=PL1DZqeVwRLnD3EjyciYAO82dT9Owiq8I5&index=6)

- [Fallacy #7: Transport cost is zero](https://particular.net/blog/transport-cost-is-zero)

[![Fallacy #7](https://i.ytimg.com/vi/18oFataWXqQ/hq720.jpg?sqp=-oaymwEhCK4FEIIDSFryq4qpAxMIARUAAAAAGAElAADIQj0AgKJD&rs=AOn4CLBuA5u5MQBt1t7Qw33uj6J-zs6r3g)](https://www.youtube.com/watch?v=18oFataWXqQ&list=PL1DZqeVwRLnD3EjyciYAO82dT9Owiq8I5&index=7)

- [Fallacy #8: The network is homogeneous](https://particular.net/blog/the-network-is-homogeneous)

[![Fallacy #8](https://i.ytimg.com/vi/99iTZGzH_3s/maxresdefault.jpg)](https://www.youtube.com/watch?v=99iTZGzH_3s&list=PL1DZqeVwRLnD3EjyciYAO82dT9Owiq8I5&index=8)


## Coupling

Coupling measures the dependency between two parts of a system. Loose coupling has become a buzzword in complex systems development, yet few understand its dimensions fully. In this module, Udi covers the five dimensions of coupling as well as patterns for dealing with them.

- [Putting your events on a diet](https://particular.net/blog/putting-your-events-on-a-diet?_gl=1*i157ol*_ga*MTM0NjIyMDg1NS4xNzIzNTQwMzgw*_ga_GMZ1FS541B*MTcyNTUyNjE5NS40MC4xLjE3MjU1MjYzNTMuMC4wLjA.)

- Microservices and Rules Engines – a blast from the past - Udi Dahan (NDC Conferences - Jul 5, 2017)

[![Microservices and Rules Engines](https://i.ytimg.com/vi/Fuac__g928E/maxresdefault.jpg)](https://www.youtube.com/watch?v=Fuac__g928E)

## Intro to Messaging

In this module, Udi explains how messaging can solve most of your service-to-service communication in a reliable way using asynchronous communication instead of directly calling methods. This produces a system that's more reliable, more stable, and safer than traditional RPC calls.

- [I caught an exception. Now what?](https://particular.net/blog/but-all-my-errors-are-severe?_gl=1*1sozi6x*_ga*MTM0NjIyMDg1NS4xNzIzNTQwMzgw*_ga_GMZ1FS541B*MTcyNTUyNjE5NS40MC4xLjE3MjU1Mjg4NDEuMC4wLjA.)

- [Architectural Principles ](https://docs.particular.net/architecture/messaging)

- [Messaging](https://docs.particular.net/nservicebus/messaging/?_gl=1*1o2bc9q*_ga*mtm0njiymdg1ns4xnzizntqwmzgw*_ga_gmz1fs541b*mtcyntuynje5ns40mc4xlje3mju1mjg5mtkumc4wlja.)

- [Async/await webinar series ](https://particular.net/webinars/async-await-best-practices?_gl=1*1jxoymk*_ga*MTM0NjIyMDg1NS4xNzIzNTQwMzgw*_ga_GMZ1FS541B*MTcyNTUyNjE5NS40MC4xLjE3MjU1Mjg5OTEuMC4wLjA.)

## Sagas/Long-Running Business Processes Modelling

The distributed communication patterns wouldn't be complete without a discussion on orchestration. In almost any event-driven architecture, you’ll have services managing multiple events in order to make decisions. The saga pattern is a great fit there, and not at all difficult to implement.

- [Sagas](https://docs.particular.net/nservicebus/sagas/?_gl=1*1nh2cmq*_ga*mtm0njiymdg1ns4xnzizntqwmzgw*_ga_gmz1fs541b*mtcynty0ndm2nc40oc4xlje3mju2nduxmtuumc4wlja.)

- [Simple Saga Usage](https://docs.particular.net/samples/saga/simple/?_gl=1*v3wkv9*_ga*mtm0njiymdg1ns4xnzizntqwmzgw*_ga_gmz1fs541b*mtcynty0ndm2nc40oc4xlje3mju2nduxotaumc4wlja.)

- [Pattern: Saga](https://microservices.io/patterns/data/saga.html)

- [NServiceBus sagas: Integrations](https://docs.particular.net/tutorials/nservicebus-sagas/3-integration/)

Sagas: Event Choreography & Orchestration (NServiceBus)

[![sagas](https://i.ytimg.com/vi/rO9BXsl4AMQ/maxresdefault.jpg)](https://www.youtube.com/watch?v=rO9BXsl4AMQ)

## Saga Design

Now that you've learned the theory behind orchestration and sagas, it's time to practice. In this exercise, you will design a saga that orchestrates the buying of digital goods in the mobile gaming space. Udi discusses different considerations and potential solutions.

### Saga Overview
![saga exercise](/assets/img/distributed-system/saga-exercises.png)

### Service Examples

![service examples](/assets/img/distributed-system/service.png)


### Similar To Hexagonal Architecture

![hexagonal architecture](/assets/img/distributed-system/hexagonal.png)