Target List
===========

All SBS command are design in the same way :

* a target, that basically represents the action(s) to perform
* a list of mandatory parameters
* a list of optional parameters

.. code-block:: console

   > sbs <target> [mandatory parameters] [optional parameters]

.. _target-build:

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


.. _target-clean:

clean
-----

Parameters
~~~~~~~~~~

Examples
~~~~~~~~

.. _target-check:

check
-----

Parameters
~~~~~~~~~~

Examples
~~~~~~~~

.. _target-compile:

compile
-------

Parameters
~~~~~~~~~~

Examples
~~~~~~~~

.. _target-configure:

configure
---------

Parameters
~~~~~~~~~~

* optional
   * *-g* : indicate to set up global configuration
   * *-p <component-path>* : set up specific configuration for a given component 
   * *-c* : clean up configuration instead of setting up
   * *-e <configuration>* : configuration file to add to the configuration
   * *-v* : verbose mode

Examples
~~~~~~~~

Set up global configuration for gcc/linux :

.. code-block:: console

   > sbs configure -g -e user -e linux
   
Set up component configuration for Wascana/Windows :

.. code-block:: console

   > sbs configure -p . -e user -e wascana
   
Clean up global configuration

.. code-block:: console

   > sbs configure -g -c

.. _target-create-component:

create-component
----------------

Parameters
~~~~~~~~~~

Examples
~~~~~~~~

.. _target-flags:

flags
-----

Parameters
~~~~~~~~~~

Examples
~~~~~~~~

.. _target-generate:

generate
--------

Parameters
~~~~~~~~~~

Examples
~~~~~~~~

.. _target-help:

help
----

Parameters
~~~~~~~~~~

Examples
~~~~~~~~

.. _target-repository:

repository
----------

Parameters
~~~~~~~~~~

Examples
~~~~~~~~

.. _target-run:

run
---

Parameters
~~~~~~~~~~

Examples
~~~~~~~~

.. _target-runtime-display:

runtime-display
---------------

Parameters
~~~~~~~~~~

Examples
~~~~~~~~

.. _target-test:

test
----

Parameters
~~~~~~~~~~

Examples
~~~~~~~~
