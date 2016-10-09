.. PyPubSub documentation master file, created by
   sphinx-quickstart on Mon May 20 21:24:10 2013.

Welcome to PyPubSub's Home Page!
====================================

.. note:: The latest API is v3.3.0, released February 2014

.. note:: This site was updated for v3.3.0. The home page for the previous release 
   v3.2.0 is at `this v3.2 URL <v3.2/index.html>`_. The home page for the release 
   before that, v3.1.2, is at `this v3.1 URL <v3.1/index.html>`_.

The Pubsub package provides a publish - subscribe Python API that facilitates 
event-based programming. Using the publish - subscribe pattern in your application 
can dramatically simplify its design and improve testability. Robin Dunn, the 
creator of wxPython where the pubsub package was born, summerizes Pubsub nicely:

    Basically you just have some part(s) of your program 
    subscribe to a particular topic and have some other part(s) 
    of your program publish messages with that topic.  All the 
    plumbing is taken care of by pubsub.  -- *Robin Dunn, Jun 2007*

The Publish - Subscribe pattern, as implemented by pubsub, provides the following 
contract between sender and receiver: 

1. Message Sending: A message can be sent (aka broadcast) from any code that can 
   import pubsub's `pub` module
2. Message Topic: 
   a. Every message has a "type": it corresponds to its "topic", a string name
   b. Topics form a hierarchy. A parent topic is more generic than a child topic. 
3. Message Handling: All message handlers must register with pubsub in order to 
   receive messages of a given topic
4. Message Delivery: 

   a. Messages sent will be delivered to all registered handlders (aka listeners, also 
      receivers) for a given topic
   b. Sequence of delivery is unknown: can change at any time; no logic should depend on it
   c. Messages are delivered synchronously: a handler must return or throw an exception 
      before the message is delivered to the next handler
   d. A message sent will be delivered immediately and control will be returned to the sender 
      only once message has been delivered to all handlers
   e. There is no relationship between order of registration vs order of delivery
   f. Additionally occurs to all listeners of more generic, ie parent topics, up to the 
      root topic which is a "catch all" topic
      
5. Message Constness: message contents will be left unchanged by any handlers
6. Message Direction: a message is one-way from sender to receiver; it cannot be used by 
   the handler to transmit data back to the sender
7. Message Source: Pubsub does not provide any information to the handlers regarding the 
   origin (aka source, or provenance) of a message

In this documentation, a *sender* is any part of the application that asks Pubsub to send 
a message of a given topic with a given payload (data, or content). The handler, aka 
receiver, is a callable object (function etc) referred to as a *listener*. 

Here is a schematic representation of the role of pubsub during message sending and delivery:

.. image:: pubsub_concept.png
   :alt: Sketch showing how pubsub fits into a Python application
   :align: center
   :width: 450px

..
   
Contents:

.. toctree::
   :maxdepth: 2

   about
   installation
   usage/index
   development/dev_index

   
Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`
