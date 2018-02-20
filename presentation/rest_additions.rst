###################################
Additional Constraints of REST
###################################

***********************************
Uniform Interface
***********************************

Components must interact through a uniform interface, which specifies:

* Identification of resources
* Manipulation of resources through representation
* Self-descriptive messages
* "Hypermedia as the engine of application state"

Provides:

* Simplification of system architecture
* Improved visibility of interactions
* Decoupling of implementations from provided services
* Independent evolvability

Drawbacks:

* Decreases efficiency, because data must be transformed into the standard form
* Most efficient for **large-grain** hypermedia transfer, which is the common
  use-case of the web

***********************************
Layered System
***********************************

Each component cannot "see" beyond the immediate layer with which it is interacting.

Provides:

* A bound on overall system complexity
* Improved component independence
* Similar architectural properties as the "pipe and filter" style when combined
  with `uniform interface`_

Drawbacks:

* Overhead and latency

Allows:

* Encapsulation of legacy or beta services
* Protection of new services from legacy clients
* Load balancing
* Firewalling


***********************************
Code on Demand
***********************************

**This constraint is optional.**

The client's functionality may be extended by allowing it to download and
execute code in the form of applets or scripts.

Provides:

* Reduces number of required features in clients

Drawbacks:

* Reduces visibility of the overall system

....


`previous <existing_architecture.rst>`_ | `next <style_summary.rst>`_
