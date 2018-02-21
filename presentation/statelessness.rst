##################################
Statelessness
##################################

This is the one that always gives people trouble. To recap,
**a REST server is stateless**.

According to Roy Fielding:

    Each request contains all of the information necessary for a connector to
    understand the request, independent of any requests that may have preceded it.

and:

    The application state is controlled and stored by the user agent and can be
    composed of representations from multiple servers.

and:

    Session state is kept entirely on the client.


********************************
So how do I do sessions?
********************************

There are several options here that do not violate the REST style. They
are not mutually exclusive:

Option One - State on the Client
================================

Store session state on the client.

If the client is filling up their shopping cart, keep a record in local storage
of the items to be sent during the checkout request to the server.

But, what if you want to be able to retain their cart even if they lose
power, clear their cache, delete their web browser, and buy a new computer?

Option Two - State is just a Resource
=====================================

**Anything that can be named can be a resource.**

If you need to persist state in a resilient way, you can just store it in your
database or redis store and provide a resource for the client to store and
retrieve the state for a logged in user.

For example:

``/users/<user_id>/cart``

If a user can only store one shopping cart at a time, this is all you need.
Send ``PATCH`` requests to the resource ID as the user adds items to the cart.
When they checkout, clear the data.

Option Three - Cookies
======================

There is no reason to use cookies and session IDs when users are authenticated,
because user authentication data should already be being sent with each request.

If you need to track sessions for anonymous users, you should first ask yourself
why, and whether it's necessary, due to increased server-side complexity and
privacy concerns.

Cookies should be viewed as untrusted until verified, like all authentication data.

   For historical reasons, cookies contain a number of security and
   privacy infelicities.  For example, a server can indicate that a
   given cookie is intended for "secure" connections, but the Secure
   attribute does not provide integrity in the presence of an active
   network attacker.  Similarly, cookies for a given host are shared
   across all the ports on that host, even though the usual "same-origin
   policy" used by web browsers isolates content retrieved via different
   ports.

   - RFC 6265

For expiring cookies, consider using a signed JWT, which can be validated
to have not been tampered with and programmed to expire.

....

`previous <rest_and_http.rst>`_ | `next <resources.rst>`_
