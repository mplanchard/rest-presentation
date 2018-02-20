#######################################
Summary of the REST Style
#######################################

The REST architectural style specifies a:

**Layered-Client-Cache-Stateless-Server with a Uniform Interface,
optionally providing Code on Demand**

... which is why it has a shorter name

***********************
REST Benefits
***********************

The benefits of REST are the summed benefits of its composite architectural
styles:

* Separation of concerns (client-server, code on demand)
* Portability of UI (client-server)
* Scalability (client-server, stateless, cache)
* Evolvability (client-server, uniform interface, code on demand)
* Visibility (stateless, uniform interface)
* Reliability (stateless)
* Simple servers (stateless, layered system)
* Loose coupling (uniform interface, layered system)
* Efficient for large-grain data transfer (uniform interface)

***********************
REST Drawbacks
***********************

The drawbacks of REST are also the summed benefits of its composite architectural
styles:

* Decreased efficiency (uniform interface, layered system, stateless)
* Reduced visibility (code on demand)
* Reduced server-side control (stateless)
* Possible decreased reliability (cache)

....

`previous <rest_additions.rst>`_ | `next <rest_elements.rst>`_
