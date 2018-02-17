#######################################################################
Blog Posts
#######################################################################

Cataloging relevant blog posts.

************************************************************************
Fielding
************************************************************************

`It is okay to use POST <http://roy.gbiv.com/untangled/2009/it-is-okay-to-use-post>`_

* Some good discussion on HTTP methods and REST

`REST APIs must be hypertext-driven <http://roy.gbiv.com/untangled/2008/rest-apis-must-be-hypertext-driven>`_

* Good set of rules for what is **not** REST

`Paper tigers and hidden dragons <http://roy.gbiv.com/untangled/2008/paper-tigers-and-hidden-dragons>`_

* Thought experiment on making a REST interface rather than a PubSub

    Web architects must understand that resources are just consistent mappings
    from an identifier to some set of views on server-side state. If one view
    doesn’t suit your needs, then feel free to create a different resource that
    provides a better view (for any definition of “better”). These views need
    not have anything to do with how the information is stored on the server,
    or even what kind of state it ultimately reflects. It just needs to be
    understandable (and actionable) by the recipient.

* Involves interesting ideas on dynamic resource creation

`On software architecture <http://roy.gbiv.com/untangled/2008/on-software-architecture>`_

* Discussion of how REST is an architectural style, not an architecture

    They work better because REST induces the architectural properties that
    the Web needs most — reusability, anarchic scalability, evolvability, and
    synergistic growth — and thus the Web architecture has been updated over
    time to promote RESTful styles over all others, by design.


************************************************************************
Fowler
************************************************************************

`Richardson Maturity Model <https://www.martinfowler.com/articles/richardsonMaturityModel.html>`_

* Discussion on "levels" of REST implementation and the benefits of each
* Resources -> HTTP verbs -> hypermedia controls
* Important to note that only level 3 is properly REST

`Enterprise Integration Using REST <https://www.martinfowler.com/articles/enterpriseREST.html>`_

(Note: not by Fowler, but rather Brandon Byars, although on the Fowler blog)

* Interesting discussion on implementing internal (intra-enterprise)
REST APIs
