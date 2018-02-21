#####################################
Data Elements - Representations
#####################################

    A representation is a sequence of bytes, plus representation metadata to
    describe those bytes

**Representations capture the current or intended state of a resource.**

Metadata may include representation metadata, resource metadata, and control
data.

**************************************
Megan from Engineering
**************************************

Request-Response One
====================

Request
-------

Control Metadata:

* Host: stuffaboutfolk.com
* Path: /folks/bob
* Method: GET (I want to know about Megan)
* Accept: application/json (I want info about Megan in JSON format)

Response
--------

Control Metadata:

* Cache-Control: max-age=3600 (Megan's info is not a time-sensitive resource,
  so feel free to cache it for an hour)

Representation Metadata:

* Content-Type: application/json (this document is JSON, like you asked)

Resource Metadata:

* Link: <stuffaboutfolk.com/folks/megan>; rel=alternate; type="image/png";
  title="profile picture" (I've got another representation of Megan)

Representation:

.. code-block:: json

    {
      "first_name": "Megan",
      "last_name": "Fink",
      "department": "engineering",
      "favorite_color": "green"
    }

Request-Response Two
====================

Request
-------

Control Metadata:

* Host: stuffaboutfolk.com
* Path: /folks/megan
* Method: GET (I want to know about Megan)
* Accept: image/png (I want Megan's PNG representation)

Response
--------

Control Metadata:

* Cache-Control: max-age=3600 (we don't update information about Bob that often)

Representation Metadata:

* Content-Type: image/png (this document is JSON, like you asked)

Resource Metadata:

* Link: <stuffaboutfolk.com/folks/megan>; rel=alternate; type="application/json";
  title="info" (I've got another representation of Megan)

Representation:

.. image:: img/picasso_head_of_a_woman.jpg
   :width: 50%
   :align: center

Picasso, *Head of a Woman* [*]_


.. [*] retrieved from the `Metropolitan Museum of Art <https://www.metmuseum.org/toah/works-of-art/1990.192/>`_, 2018-02-20

....

`previous <data_elements_resources.rst>`_ | `next <>
