.. _advanced-server:

Set up an SBS server
====================

Basic SBS server
----------------

The is one simple command to deploy an SBS server :

.. code-block:: console

   > sbs serve

And that all :) .

You don't need to use the :ref:`configure target <target-configure>` as it is a general purpose server
(i.e not linked to any toolchain, build configuration, ...).


Customize server configuration
------------------------------

Well, in fact that's not all. You can customize a little your SBS server environment.

The big advice we could give you if to fully seperate your entirely your SBS server environment by setting the *SBS_HOME* variable.
It will allow you  to deploy all the component into a fully seperate repository.

Server commands
---------------

Create SBS server daemon (Linux)
--------------------------------
