Notes from Roy Fielding's Dissertation
======================================

https://www.ics.uci.edu/~fielding/pubs/dissertation/software_arch.htm


Introduction
------------

* Starts with a Monty Python reference
* Divided into four sections

  + Chapters 1-3: application of architectural styles and frameworks to
    network software
  + Chapter 4: architectural requirements of the web
  + Chapter 5: REST
  + Chapter 6: Six years experience using the REST architectural style to
    drive the design of the HTTP and URI protocols (also by Fielding)

* REST is an architectural style, *not* an interface


Chapters 1-3
------------

Chapter 1: Software Architecture
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Defining a (locally scoped) meaning of software architecture, since there are
a lot of different interpretations of its meaning. Commences with a sequence
of definitions of that collectively mean "software architecture".

Runtime Abstraction
+++++++++++++++++++

  A **software architecture** is an abstraction of the run-time elements of a
  software system during some phase of its operation. A system may be
  composed of many levels of abstraction and many phases of operation, each
  with its own software architecture.

* This definition defines architecture at a given abstraction level such that
  it consists of the abstract interfaces a given element present to other
  elements
* It is a recursive definition (architectural elements at a given layer may
  have their own architecture, and so forth)
* It is explicitly related to the runtime abstractions present in a system,
  and not to source-code level implementations (e.g. local functions vs shared
  libraries)

Elements
++++++++

  A **software architecture** is defined by a configuration of architectural
  elements -- components, connectors, and data -- constrained in their
  relationships in order to achieve a desired set of architectural
  properties.

Components
**********

  A **component** is an abstract unit of software instructions and internal
  state that provides a transformation of data via its interface

* Behavior of a component is part of the architecture only **"insofar as that
  behavior can be observed or discerned from the point of view of another
  component . . . a component is [therefore] defined by its interface . . .
  rather than its implementation"**

Connectors
**********

  A **connector** is an abstract mechanism that mediates communication,
  coordination, or cooperation among components.

* E.g. "shared representations, remote procedure calls, message-passing
  protocols, and data streams"
* Transfer data elements from one interface to another *without changing data*

Data
****

  A **datum** is an element of information that is transferred from a
  component, or received by a component, via a connector

* E.g. "byte-sequences, messages, marshalled parameters, and serialized
  objects"
* Explicitly does not include information "permanently resident or hidden
  within a component"

Configurations
++++++++++++++

  A **configuration** is the structure of architectural relationships among
  components, connectors, and data during a period of system run-time

Properties
++++++++++

  The set of architectural **properties** of a software architecture include
  all properties that derive from the selection and arrangement of components,
  connectors, and data within the system.

* Includes both functional properties and non-functional properties, like
  reusability, efficiency, and extensibility

Styles
++++++

  An **architectural style** is a coordinated ste of architectural constraints
  that restrict the roles/features of architectural elements and the allowed
  relationships among those elements within any architecture that conforms
  to that style

* Provides an abstraction for the interaction of components
* "Encapsulates important decisions about the architectural elements and
  emphasizes constraints on the elements and their relationships"
* Uses a metaphor of architectural styles as classes and new architectures
  as instances, with multiple inheritance possible to create hybrid
  architectures

Patterns and Pattern Languages
++++++++++++++++++++++++++++++

  A **design pattern** is defined as an important and recurring system
  construct. A **pattern language** is a system of patterns organized
  in a structure that guides the patterns' application.

* Able to describe relatively complex protocols of interactions between
  objects as a single abstraction

Views
+++++

Views are perspectives from which an architecture may be evaluated, e.g.
a process view, "which emphasizes the data flow through the components,"
a data view, which "emphasizes the processing flow," and a connection view,
which "emphasizes the relationship between components and the state of
communication."


Chapter 2: Network-based Application Architectures
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This chapter limits itself to architecture among the highest level of
components, where interactions between components are "realized in network
communication." The discussion is limited to "network-based application
architecture."

* A network-based application architecture is one where communication
  between components is restricted to message passing or its equivalent
* Application software architecture is a level of the system that is
  "business-aware," able to represent the goals of a user action as
  architectural properties

Evaluating the Design of Application Architectures
++++++++++++++++++++++++++++++++++++++++++++++++++

The evaluation of an application architecture requires investigation of the
constraints it places on a system and on the properties derived from those
constraints, specifically whether they contribute to the application's
objectives.

We can evaluate an architecture style by:

* An application's functional requirements
* The cumulative properties arising from the sum of the architecture's
  constraints

  + It is suggested this be done through a derivation tree, where
    architectural styles are combined, with the constraints of each
    adding to the cumulative properties present at any given node
  + Traversing the tree can then yield the combination of styles providing
    the set of properties most aligned with the application's goals.

Architectural Properties of Key Interest
++++++++++++++++++++++++++++++++++++++++

Performance
***********

  Component interactions can be the dominant factor in
  determining user-perceived performance and network efficiency.

Network Performance
^^^^^^^^^^^^^^^^^^^

* **Throughput**: the rate at which information, including both application
  data and communication overhead, is transferred between components
* **Overhead**: initial setup overhead and per-interaction overhead
* **Bandwidth**: a measure of the maximum available throughput over a given
  network link
* **Usable Bandwidth**: the portion of bandwidth actually available to the
  application

An architectural style impacts network performance via number of network
interactions required per user action and the granularity of data elements.

User-perceived Performance
^^^^^^^^^^^^^^^^^^^^^^^^^^

Measured in latency and completion time.

* **Latency**: the time period between initial stimulus and the first
  indication of a response. Comprises:

  + Time required to recognize the event
  + Time required to setup component interactions
  + Time required to transmit each interaction to the components
  + Time required to process each interaction on each component
  + Time required to complete sufficient transfer and processing of the
    result to begin rendering something usable

* **Completion time**: the amount of time required to complete an action

Lower latency can sometimes lead to an improved perception of performance,
even when it comes at a cost of increasing the completion time.

Network Efficiency
^^^^^^^^^^^^^^^^^^

  the best application performance is obtained by not using the network

The most efficient architectural styles for use in network applications are
those which minimize the use of the network. This is done via:

* Caching prior interactions
* Utilizing replicated data
* Allowing disconnected operation
* Allowing some data processing to be performed locally

Scalability
***********

An architecture capable of supporting large numbers of components or
component interactions within an active configuration is said to be
**scalable**

Improved by:
* Simplifying components
* Distributing services across many components (decentralization)
* Controlling interactions and configurations as a result of monitoring

Style considerations:
* Application state
* Extent of distribution
* Component coupling

Impacted by:
* Frequency of interactions
* Load distribution over time
* Requirement of guaranteed delivery vs bet-effort
* Synchronous vs asynchronous handling
* Controlled or anarchic (trusted components or not)

Simplicity
**********

Primarily achieved by separation fo concerns in component functionality.

Modifiability
*************

Systems will always require gradual and fragment change.

Network-based systems often need to be dynamically modifiable.

Evolvability
^^^^^^^^^^^^

  The degree to which a component implementation can be changed without
  negatively impacting other components.

Architectural styles constraining the maintenance and location of
application state affect the ability to dynamically evolve. Similar techniques
as used to support partial failure conditions in distributed systems
are appropriate for dynamic evolution.

Extensibility
^^^^^^^^^^^^^

  The ability to add functionality to a system

The reduction of coupling is t he primary means of improving extensibility,
e.g. event-based systems

Customizability
^^^^^^^^^^^^^^^

  The ability to temporarily specialize the behavior of an architectural
  element, such that it can then perform an unusual service. A component
  is customizable if it can be extended by one client of that component's
  services without adversely impacting other clients of that component

Related to simplicity and scalability. Influenced by remote-execution and
code-on-demand styles

Configurability
^^^^^^^^^^^^^^^

Post-deployment modification of components or their configurations such that
they are capable of using a new service or data element type.

Reusability
^^^^^^^^^^^

  Reusability is a property of an application architecture if its components,
  connectors, or data elements can be reused, without modification, in other
  applications

Influenced by reduction of coupling and constraining the generality of
component interfaces.

Visibility
^^^^^^^^^^

  The ability of a component to monitor or mediate the interaction between
  two other components.

Allows shared caching of interactions, layered services, reflective monitoring,
and security.

Portability
^^^^^^^^^^^

  Software is portable if it can run in different environments

Reliability
^^^^^^^^^^^

  The degree to which an architecture is susceptible to failure at the system
  level in the presence of partial failures within components, connectors,
  or data.
