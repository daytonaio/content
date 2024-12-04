---
title: 'Monolithic'
description:
  'In the context of software architecture, monolithic refers to an approach
  where an application is built as a single, unified unit rather than being
  divided into smaller, independent services. It describes a system design where
  all components and functionalities are tightly coupled and interdependent
  within a single codebase. Monolithic systems are traditionally characterized
  by having a single large executable or deployment artifact.'
---

# Monolithic

## Definition

In the context of software architecture, monolithic refers to an approach where
an application is built as a single, unified unit rather than being divided into
smaller, independent services. It describes a system design where all components
and functionalities are tightly coupled and interdependent within a single
codebase. Monolithic systems are traditionally characterized by having a single
large executable or deployment artifact.

The term "monolithic" gained prominence when contrasting it with modular and
microservices architectures. While monolithic architectures have been widely
used in the past, they can become complex to maintain as the size of the
application grows or when multiple teams work on different parts of the system
simultaneously.

In a monolithic architecture, any changes or updates to one component often
require rebuilding and redeploying the entire application. This can result in
longer development cycles, increased risk, and difficulties in scaling and
isolating individual functionalities. Additionally, since the components are
tightly coupled, it can be challenging to adopt new technologies or make changes
without affecting other parts of the system.

Despite their drawbacks, monolithic architectures can be simpler to develop and
initially deploy compared to more distributed architectures like microservices.
They are also suitable for smaller applications with limited scalability
requirements or situations where the overhead of managing distributed systems
outweighs the benefits. However, modern software development practices often
favor more modular and loosely coupled architectures, such as microservices or
serverless, to enable agility, scalability, and independent development and
deployment of different components.
