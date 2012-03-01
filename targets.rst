Target List
===========

All SBS command are design in the same way :

* A target, that basically represents the action(s) to perform.
* A list of mandatory parameters.
* A list of optional parameters.

.. code-block:: console

   > sbs <target> [mandatory parameters] [optional parameters]

.. _target-build:

build
-----

| Build a component and/or tests in release or debug mode.
| Need global or component specific configuration.
| Need a valid component description file (default : sbs.xml).

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

| Clean a component and/or tests.
| Remove all object/libraries/executables.
| Remove CMake files/Makefiles/Environment files.
| Need global or component specific configuration.
| Need a valid component description file (default : sbs.xml).

Parameters
~~~~~~~~~~

Examples
~~~~~~~~

.. _target-check:

check
-----

| Verifiy XML component description file.
| Need global or component specific configuration.
| Need a component description file (default : sbs.xml).

Parameters
~~~~~~~~~~

Examples
~~~~~~~~

.. _target-compile:

compile
-------

| Compile componenet without regenrating CMake files.
| Need global or component specific configuration.
| Need a valid component description file (default : sbs.xml).

Parameters
~~~~~~~~~~

Examples
~~~~~~~~

.. _target-configure:

configure
---------

| Configure global or component specific configuration.

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
   
Clean up global configuration :

.. code-block:: console

   > sbs configure -g -c

.. _target-create-component:

create-component
----------------

| Create a component from scratch.
| Need a valid component description file (default : sbs.xml).

Parameters
~~~~~~~~~~

Examples
~~~~~~~~

.. _target-flags:

flags
-----

| Add/modify/remove compile flag(s) to component description.

Parameters
~~~~~~~~~~

Examples
~~~~~~~~

.. _target-generate:

generate
--------

| Generate component and/or test CMake files in release or debug mode.
| Need global or component specific configuration.
| Need a valid component description file (default : sbs.xml).

Parameters
~~~~~~~~~~

Examples
~~~~~~~~

.. _target-help:

help
----

| Help target.
| If no target specified, print target list.
| Else, print target help.

Parameters
~~~~~~~~~~

Examples
~~~~~~~~

.. _target-repository:

repository
----------

| Generic target to handle repositories.
| Need global or component specific configuration.

Parameters
~~~~~~~~~~

Examples
~~~~~~~~

.. _target-run:

run
---

| Run the component executable
| Need global or component specific configuration.
| Need a valid component description file (default : sbs.xml).

Parameters
~~~~~~~~~~

Examples
~~~~~~~~

.. _target-runtime-display:

runtime-display
---------------

| Display all library and executable dependency paths.

Parameters
~~~~~~~~~~

Examples
~~~~~~~~

.. _target-test:

test
----

| Run the component tests
| Need global or component specific configuration.
| Need a valid component description file (default : sbs.xml).

Parameters
~~~~~~~~~~

Examples
~~~~~~~~
