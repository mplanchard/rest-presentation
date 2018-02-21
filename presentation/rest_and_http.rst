################################
REST and HTTP
################################

HTTP was designed to comply with the REST style, so a **huge** portion
of web infrastructure works seamlessly with REST architecture.

Discoverability
===============

By adding ``Link`` headers to your documents:

* Browsers will automatically prefetch any ``link`` headers marked as
  ``rel=next`` or ``rel=prefetch``
* `Client-side libraries <https://www.npmjs.com/package/parse-link-header>`_ can
  automatically parse the header and extract paging information

Caching
=======

* ``Cache-Control`` headers allow fine-grained tuning of data caching
  from both the client and server side. Some points of control:

  + ``max-age``, ``max-stale``, ``min-fresh``, ``no-cache``, ``no-store``,
    ``no-transform``, ``only-if-cached``, ``must-revalidate``, ``public``,
    ``private``, ``proxy-revalidate``

* Caching is **automatically implemented** by web browsers and most CDNs
  if ``Cache-Control`` headers are present
* Automatic HTTP caching libraries are available for non-browser clients, including
  Python's `requests <https://pypi.python.org/pypi/requests-cache>`_, and
  `react native <https://www.npmjs.com/package/react-native-http-cache>`_,
* ``ETag`` headers allow custom hashing of representations, allowing clients
  to request an update only if the hash hasn't changed

Layering
========

Assuming a layered interface allows programs like nginx and haproxy to:

* Act as a reverse proxy
* Terminate SSL at the load balancer and redirect requests to local HTTP
  servers, decreasing server load
* Add arbitrary headers
* Reroute traffic depending on its origin, path, method, etc.
* Log metadata about all requests and responses

It also enables middleware apps, such as:

* An authentication layer that uses an ``Authorization`` token to look
  up a user in an IAM database, and adds information about their roles
  to the request
* A compression layer that automatically gzips all response bodies and
  adds a ``Content-Encoding`` header to the response, so that clients
  can automatically unzip them

....

`previous <data_elements_representations.rst>`_ | `next <statelessness.rst>`_
