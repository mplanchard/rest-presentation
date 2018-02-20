###################################
Elements of the REST Style
###################################

***********************************
Data Elements
***********************************

The stuff transferred from component to component via connectors.

======================= =======================================================
Data Element            Examples
======================= =======================================================
resource                the intended conceptual target of a hypertext reference
resource identifier     URL, URI
representation          HTML document, JSON blob, PNG image, MP4 movie
representation metadata Content-Type, Last-Modified
resource metadata       Content-Location, Vary
control data            If-Modified-Since, Cache-Control, Method
======================= =======================================================

***********************************
Connectors
***********************************

Provide an abstract interface for transferring stuff from component to component

================  ==============================
Connector         Examples
================  ==============================
client            requests, curl, libwww
server            nginx, apache
cache             browser cache, Akamai
resolver          DNS
tunnel            SSL, Sockets
================  ==============================

***********************************
Components
***********************************

Initiate, route, and respond to requests.

=============   ========================
Component       Examples
=============   ========================
origin server   Flask, NodeJS, httpd
gateway         FastCGI, reverse proxy
proxy           Cisco Umbrella, WinGate
user agent      Firefox, Chrome
=============   ========================

....

`previous <style_summary.rst>`_ | `next <data_elements_resources.rst>`_
