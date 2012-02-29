Target List
===========

All SBS command are design in the same way :

* a target, that basically represents the action(s) to perform
* a list of mandatory parameters
* a list of optional parameters

.. code-block:: console

   > sbs <target> [mandatory parameters] [optional parameters]

build
-----

Parameters
~~~~~~~~~~

* mandatory
   * *<component-path>* : path to component (i.e that contains a sbs.xml file)
* optional
   * *-i <sbs-file>* : select specific sbs xml file
   * *-t* : target test
   * *-b* : target both main and test
   * *-d* : debug build
   * *-v* : verbose mode

Examples
~~~~~~~~

Build a component :

.. code-block:: console

   > sbs build .
   
Build component tests :

.. code-block:: console

   > sbs build . -t

Build both component and component tests :

.. code-block:: console

   > sbs build . -b
   
Build both component in debug mode :

.. code-block:: console

   > sbs build . -d
   
Build a component issuing a specific compoenent file :

.. code-block:: console

   > sbs build . -i sbs-linux.xml


clean
-----

check
-----

compile
-------

configure
---------

create-component
----------------

flags
-----

generate
--------

help
----

repository
----------

run
---

runtime-display
---------------

test
----
