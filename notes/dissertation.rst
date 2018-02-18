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

.. _`uniform interface`:

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

.. _`layered system`:

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

.. _stateless:

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

Chapter 4 - Designing the Web Architecture: Problems and Insights
-----------------------------------------------------------------

This chapter describes some of the particular problems presented by the
web in trying to establish the most effective architectural system, due
to its structure and purpose.

WWW Application Domain Requirements
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This section defines some of the required and desired characteristics of
the web domain in terms of the desired nature of the world wide web, as
originally defined by Berners Lee.

Low Entry-barrier
+++++++++++++++++

Hypermedia is the web interface due to its simplicity and generality.

* Allows for unlimited structuring
* Allows the definition of complex relationships
* Generic query interface

Availability of overall system does not affect authoring of content.

* Simple format usable whether connected to the internet or not
* Ability to specify a reference to information before the target is
  available
* Ease of communicating references

Simplicity of Development

* Text-based protocols to allow viewing and interactive testing
* Allowed early adoption in spite of lack of standards

Extensibility
+++++++++++++

Allows the web to evolve to match the evolving needs of users. The web
must be prepared for change.

Distributed Hypermedia
++++++++++++++++++++++

    Hypermedia is defined by **the presence of application control information
    embedded within, or as a layer above, the presentation information.**

* Allows the presentation and control information to be stored at remote locations
* Requires the transfer of large amounts of data from where it is stored to where
  it is used (**large-grain data transfer**)

Usability is highly sensitive to user-perceived latency. Architecture
therefore needs to minimize network interactions.

Internet-scale
++++++++++++++

    The web is intended to be an *Internet-scale* distributed hypermedia system

Must be abel to interconnect information across multiple organizational
boundaries, as well as geographic dispersement. Anarchic scalability and
independent deployment of components are required.

Anarchic Scalability
********************

A system open to the Internet does not have the benefit of all entities
within the system acting towards a common goal or under the control of any
one entity.

The architecture must account for **unanticipated load** and **malicious actors**.
This requires visibility and scalability.

Therefore:

* Clients cannot be expected to maintain knowledge of all servers
* Servers cannot be expected to retain knowledge of state across requests
* Hypermedia data cannot contain back-pointers

Security is also a significant concern.

* Multiple trust boundaries may be present in any communication
* Intermediary applications (e.g. firewalls) must be able to inspect interactions
  and prevent certain of them from being acted upon
* Participants must assume that information is untrusted or require additional
  authentication before giving trust.

  + This requires ability of communicating authentication data and authorization
    controls
  + Because authentication degrades stability, the default operation should be
    limited to actions not requiring trust data

Independent Deployment
**********************

* Multiple organizational boundaries require gradual and fragmented change.
* Old and new implementations must be able to co-exist without preventing
  new implementations from taking advantage of extended capabilities.
* Existing elements must be designed expecting that features will be added.
* Older implementations need to be easily identified to allow legacy interactions.
* Deployment must be enabled in an iterative, partial fashion, since no
  orderly transition is possible.

Problem
~~~~~~~

The rapid growth in the adoption of the web caused concerns about a general
collapse due both to the increased traffic and poor network characteristics
of early HTTP.

As adoption grew, the use cases changed from a primarily textual representation
of information to one utilizing inline images and other rich media. These
challenged the single request-response oriented architecture of the early
web. A variety of conflicting standards were proposed by several organizations.

The Internet Engineering Taskforce formed working groups to refine and/or
define the three primary standards of the web: URI, HTTP, and HTML. Their
goal was to:

* Define the subset of existing architectural communication in the early web
* Identify problems with that architecture
* Specify a set of standards to solve the problem

Approach
~~~~~~~~

The early web was based on principles of separation of concerns, simplicity,
and generality, but lacked an architectural description and rationale.

    An `architectural style <styles>`_ is a named set of constraints on
    architectural elements that induces the set of properties of the
    desired architecture.

Hypothesis 1
++++++++++++

    The design rational behind the WWW architecture can be described by
    an architectural style consisting of the set of constraints applied
    to the elements within web architecture.

Hypothesis 2
++++++++++++

    Constraints can be added to the WWW architectural style to derive a new
    hybrid style that better reflects the desired properties of a modern
    web architecture.

Hypothesis 3
++++++++++++

    Proposals to modify the Web architecture can be compared to the updated
    WWW architectural style and analyzed for conflicts prior to deployment


Chapter 5: Representational State Transfer (REST)
-------------------------------------------------

Deriving REST
~~~~~~~~~~~~~

REST is a combination of the constraints from the following architectural styles:

1. The null style

**Early architecture**

2. `Client-Server`_
3. `Stateless`_
4. `Cache`_

**REST Additions**

5. `Uniform Interface`_
6. `Layered System`_
7. `Code on Demand`_

REST - Client-Server
++++++++++++++++++++

Clients and servers must be separate components.

* Separation of concerns
* Portability of UI across multiple platforms
* Scalability
* Independent evolution

REST - Stateless
++++++++++++++++

All REST interactions are stateless.

* Visibility
* Reliability
* Scalability
* Simplifies server-side implementation
* May increase per-interaction overhead
* Reduces server-side control over client behavior

REST - Cache
++++++++++++

Responses must be implicitly or explicitly labeled as cacheable or non-cacheable.

* Efficiency
* Partially or completely eliminate some interactions
* Can decrease reliability of data if cache differs from data that would be
  sent by the server

REST - Uniform Interface
++++++++++++++++++++++++

The following constraints provide a uniform interface between components:

* Identification of resources
* Manipulation of resources through representations
* Self-descriptive messages
* Hypermedia as the engine of application state

This provides:

* Simplification of overall system architecture
* Visibility of interactions improved
* Decoupling of implementations from provided services
* Independent evolvability
* Degrades efficiency, because of need to transform information into the
  standard form
* Designed to be efficient for **large-grain** hypermedia data transfer,
  the common use-case of the web.

REST - Layered System
+++++++++++++++++++++

Each component cannot "see" beyond the immediate layer with which they are
interacting.

* Places a bound on overall system complexity
* Promotes substrate independence
* Add overhead and latency
* When combined with `uniform interface`_, creates similar architectural
  properties to `pipe and filter`_

For example:

* Encapsulation of legacy services
* Protection of new services from legacy clients
* Load balancing
* Firewalling

REST - Code on Demand
+++++++++++++++++++++

**(Optional constraint)**

Allows client functionality to be extended by downloading and executing
code in the form of applets or scripts.

* Simplifies clients by reducing number of required features
* Reduces visibility

REST Architectural Elements
~~~~~~~~~~~~~~~~~~~~~~~~~~~

    REST is an abstraction of architectural elements within a distributed
    hypermedia system.

Data Elements
+++++++++++++

Information on the web must be moved from where it is stored to where it will
be consumed.

Components communicate by transferring a **representation** of a resource
in a format selected *dynamically* based on the capabilities or desires of the
recipient and the nature of the resource. Shared understanding of data types
is provided via metadata.

======================= =======================================================
Data Element            Examples
======================= =======================================================
resource                the intended conceptual target of a hypertext reference
resource identifier     URL, URI
representation          HTML document, JSON blob, PNG image, MP4 movie
representation metadata Content-Type, Last-Modified
resource metadata       Content-Location, Vary
control data            If-Modified-Since, Cache-Control
======================= =======================================================

.. _resources:
.. _`resource identifiers`:

Resources and Resource Identifiers
**********************************

    Any information that can be named can be a resource: a document or image,
    a temporal service (e.g. "today's weather in Los Angeles"), a collection
    of other resources, a non-virtual object (e.g. a person), and so on. In
    other words, any concept that might be the target of an author's hypertext
    reference must fit within the definition of a resource. A resource is a
    conceptual mapping to a set of entities, not the entity that corresponds
    to the mapping at any particular point in time.

    More precisely, a resource R is a temporally varying membership function
    MsubR(t), which for time t maps to a set of entities, or values, which are
    equivalent.

* values in the set may be *resource identifiers* or *resource representations*
* resource can map to the empty set
* resources may be static or variable (only the identification must be static)

Provides:

* generality (many sources of information without distinguishing them by type
  or implementation)
* allows late binding of a reference to a representation, enabling content
  negotiation based on the request
* allows reference to a concept rather than a singular representation of the concept
* identification of a resource involved in inter-component interaction

Representations
***************

    REST components perform actions on a resource by using a representation to
    capture the current or intended state of that resource and transferring
    that representation between components. A representation is a sequence of
    bytes, plus representation metadata to describe those bytes

"Data, metadata describing the data, and, on occasion, metadata to describe
the metadata."

Metadata is name-value pairs

Responses may include both representation metadata and resource metadata.
Resource metadata is information about the resource not specific to the supplied
representation.

Control data provides:

* action being requested (e.g. HTTP GET)
* meaning of a response (e.g. response code)
* parametrize requests (e.g. query parameters)
* override default behavior of connectors (e.g. cache-control)

A representation may indicate the current state, the desired state, or the
value of another resource.

Media type indicates the data format of a representation. **Composite media
types may be used to enclose multiple representations in a single message.**

Connectors
**********

Encapsulate the activity of accessing resources and transferring representations.

Connectors present an abstract interface for component communication.

Allows:

* Simplicity (separation of concerns, hiding implementation)
* Substitutability

Examples:

Connector         Examples
client            requests, curl, libwww
server            nginx, apache
cache             browser cache, Akamai
resolver          DNS
tunnel            SSL, Sockets

Each request **must** contain all of the information necessary for a connector
to understand the request, independent of any requests that may have preceded it.

* Removes need for connectors to retain application state (reduces consumption
  of physical resources and improves scalability)
* allows interactions to be processed in parallel
* allows intermediary to view and understand a request in isolation
* forces all information that might factor in to reusability o a cached response
  to be present in each request

In parameters:

* request control data
* resource identifier
* optional representation

Out parameters:

* response control data
* resource metadata
* optional representation

Components
**********

=============   ======================
Component       Examples
=============   ======================
origin server   WSGI server, httpd
gateway         CGI, reverse proxy
proxy           Netscape proxy
user agent      Firefox, Chrome
=============   ======================

User agents use client connectors to initiate a request and become the
recipient of a response.

Origin servers use server connectors to govern the namespace for a requested
resource. They are the definitive source for representations and must be
the ultimate recipient of requests intended to modify resource values.

Proxies are intermediaries selected by a client to provide interface
encapsulation, data translation, performance enhancement, or security
protection.

Gateways provide interface encapsulation of other services, data translation,
performance enhancement, or security enforcement.

REST Architectural Views
~~~~~~~~~~~~~~~~~~~~~~~~

This section provides examples of the interaction between REST architectural
elements from various perspectives.

