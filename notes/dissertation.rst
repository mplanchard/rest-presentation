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

Chapter 3 - Network Based Architectural Styles
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This chapter catalogues a variety of existing architectural styles, evaluating
them according to the properties defined in the previous chapter.

Data-Flow Styles
++++++++++++++++

Pipe and Filter
***************

Each component reads streams of data on input and produces streams of
data on output while applying incremental transformation and processing.

* filters must be completely independent (no coupling)
* no shared state, control thread, or identity with other filters

Advantages:

* Overall stream a composition of behaviors of each filter
* Supports reuse
* Extensible
* Evolvable
* Verifiable
* Concurrency

Disadvantages:

* Propagation delay
* Batch sequential processing
* Components cannot interact with their environment


Uniform Pipe and Filter
***********************

Adds the constraint that all filters must have the same interface.

Example: Unix processes (stdin, stdout, stderr)

Advantages:

* Mix and match at will for new functionality

Disadvantages:

* May reduce network performance if data conversion needs to be performed

Replication Styles
++++++++++++++++++

Replicated Repository
*********************

More than one process provide the same service, while providing the illusion
there is only one centralized service.

Examples:

* Distributed filesystems
* CVS

Advantages:

* Improved user-perceived performance

Disadvantages:

* Difficult to maintain consistency

Cache
*****

Replication of the result of an individual request so it may be reused
by later requests

Can be lazy (replicated upon a request being made) or active (replicated
in advance).

Advantages:

* Simpler to implement than `replicated repository`_

Disadvantages:

* Less improvement than replicated repository, since cache misses are
more likely (only holding recently used data)

Hierarchical Styles
+++++++++++++++++++

Client-Server
*************

A server component waits for and responds to requests from client component(s).

Advantages:

* Separation of concerns
* Scalability

Layered-Client-Server
*********************

A variation of the Layered-System style, where each layer of a system provides
services to the layer above it and uses the services of the layer below it.
Layered client-server adds proxy and gateway components to `client-server`_.
Proxies are shared servers for multiple client components, forwarding
requests to server components. Gateways appear to be normal servers,
but forward requests to inner servers.

Examples:

* TCP/IP stack
* Hardware interface libraries

Advantages:

* Reduced coupling, since only adjacent layers interact
* Allows knowledge of a limited suite of components where knowledge of
all components would be too expensive

Disadvantages:

* Add overhead and latency to data processing

Client-Stateless-Server
***********************

Adds the constraint to `client-server`_ that no session state is allowed on
the server component.

Advantages:

* Visibility
* Reliability
* Scalability

Disadvantages:

* Increased per-interaction overhead

Client-Cache-Stateless-Server
*****************************

Adds a cache component to `client-stateless-server`_.

Examples:

* NFS

Advantages:

* Can partially or completely eliminate some interactions


Layered-Client-Cache-Stateless-Server
*************************************

Combination of `layered-client-server`_ and `client-cache-stateless-server`_.

Examples:

* DNS

Advantages and disadvantages a combination of `layered-client-server`_
and `client-cache-stateless-server`_

Remote Session
**************

Variant of `client-server`_ where application state kept entirely on the
server to maximize reuse of client components.

Examples:

* TELNET
* FTP

Advantages:

* Central maintenance of server interface
* Improved efficiency if clients make use of session context

Disadvantages:

* Reduces scalability
* Reduces visibility

Remote Data Access
******************

Variant of `client-server`_ where application state is spread across client
and server.

Example:

    A client sends a database query in a standard format, such as SQL, to a
    remote server. The server allocates a workspace and performs the query,
    which may result in a very large data set. The client can then make
    further operations upon the result set (such as table joins) or retrieve
    the result one piece at a time. The client must know about the data
    structure of the service to build structure-dependent queries.

Advantages:

* Allow large data sets to be iteratively reduced on the server side without
transmitting it across the network
* Visibility improved by using a standard query language

Disadvantages:

* Client must understand same data manipulation concepts as the server (reduced
simplicity)
* Reduced scalability
* Reduced reliability (unknown state on failure)

Mobile Code Styles
++++++++++++++++++

Change the distance between processing and source of data.

Virtual Machine
***************

Advantages:

* Separation between instruction and implementation (portability)
* Extensible

Disadvantages:

* Reduced visibility
* Reduced simplicity

Remote Evaluation
*****************

Derived from `client-server`_ and `virtual machine`_. Client sends know-how
on how to perform a service, server uses its resources to do it and returns
the result.

Advantages:

* Customization of server component's services (extensibility and customizability)
* Efficiency

Disadvantages:

* Reduced simplicity due to need to manage evaluation environment
* Reduced scalability
* Reduced visibility


Code on Demand
**************

Client has access to resources, but not the know-how of how to process them.
Sends request to remote server for code representing the know-how, which it
executes locally.

Advantages:

* Ability to add features to already-deployed client (extensibility and
configurability)
* Better user-perceived performance if the code can adapt to the client
environment
* Improved scalability

Disadvantages:

* Reduced simplicity
* Reduced visibility

Layered-Code-on-Demand-Client-Cache-Stateless-Server
****************************************************

Since code is another data element, it can be used with the
`layered-client-cache-stateless-server`_ style.

Mobile Agent
************

Entire computational component moved to a remote site, with state, necessary
code, and data.

Combination of `remote evaluation`_ and `code on demand`_.

Peer-to-Peer Styles
+++++++++++++++++++

Event-based Integration
***********************

A component can announce one or more events. Other components can register as
listeners for event types. When an event is triggered, the system invokes
the registered components.

Advantages:

* Removes need for identity on connector interface
* Extensible
* Reusable
* Evolvable
* Can improve efficiency for systems dominated by data monitoring rather than
retrieval (no polling)

Disadvantages:

* Poor understandability (hard to know what will happen in response to a given
event)
* Not suitable for exchanging large-grain data
* Reliability (cannot recover from partial failure)

C2
***

Combines `event-based integration`_ with `layered-client-server`_. Components
communicate by asynchronous notifications going down, and asynchronous
requests going up. Notifications are an announcement of state change.

Advantages:

* Enforces loose coupling
* Layered filtering allows evolvability, scalability, and reliability

Distributed Objects
*******************

Organizes a system of components acting as peers. State is distributed
among the objects. Operations may cause a chain of action between objects.

Advantages:

* State can be kept where it is most likely to be up-to-date.

Disadvantages:

* Visibility (hard to see state when spread among objects)
* All connected objects must be changed when an object's identity changes
* Must be a controller object

Brokered Distributed Objects
****************************

Introduces name resolver components whose purpose is to answer client
object requests for general service names with the specific name of an object
which will satisfy the request.

Advantages:

* Reusability
* Evolvability

Disadvantages:

* Requires additional network interactions
