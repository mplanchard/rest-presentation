#####################################
Architectural Styles of the 1994 Web
#####################################

*************************************
Client-Server
*************************************

Clients and servers must be separate components

* Separation of concerns
* Portability of UI
* Scalability
* Independent evolution

*************************************
Stateless
*************************************

Interactions should be stateless in order to improve:

* Visibility
* Reliability
* Scalability
* Simplicity of server-side implementation

Drawbacks:

* Per-interaction overhead
* Reduction in server-side control

*************************************
Cache
*************************************

Responses must be implicitly or explicitly labeled as cacheable or not cacheable.

* Efficiency
* Partial or complete elimination of some interactions

However:

* Can decrease reliability if cache-delivered data differs from the source
  of truth

....

`previous <architecture_definitions.rst>`_ | `next <rest_additions.rst>`_
