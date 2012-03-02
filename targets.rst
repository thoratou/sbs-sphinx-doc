Target List
===========

All SBS command are design in the same way :

* A target, that basically represents the action(s) to perform.
* A list of mandatory parameters.
* A list of optional parameters.

.. code-block:: console

   > sbs <target> [mandatory parameters] [optional parameters]
   
.. _target-build:

""""

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
   
Build component in debug mode :

.. code-block:: console

   > sbs build . -d
   
Build a component using a specific component file :

.. code-block:: console

   > sbs build . -i sbs-linux.xml

""""

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

* mandatory
   * *<component-path>* : path to component (i.e that contains a sbs.xml file)
* optional
   * *-i <sbs-file>* : select specific sbs xml file
   * *-t* : target test
   * *-b* : target both main and test
   * *-v* : verbose mode

Examples
~~~~~~~~

Clean a component :

.. code-block:: console

   > sbs clean .
   
Clean component tests :

.. code-block:: console

   > sbs clean . -t

Clean both component and component tests :

.. code-block:: console

   > sbs clean . -b   
   
Clean a component using a specific component file :

.. code-block:: console

   > sbs clean . -i sbs-linux.xml

""""

.. _target-check:

check
-----

| Verifiy XML component description file.
| Need global or component specific configuration.
| Need a component description file (default : sbs.xml).

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

Check a component :

.. code-block:: console

   > sbs check .
   
Check component tests :

.. code-block:: console

   > sbs check . -t

Check both component and component tests :

.. code-block:: console

   > sbs check . -b
   
Check component in debug mode :

.. code-block:: console

   > sbs check . -d
   
Check a component using a specific component file :

.. code-block:: console

   > sbs check . -i sbs-linux.xml

""""

.. _target-compile:

compile
-------

| Compile componenet without regenrating CMake files.
| Need global or component specific configuration.
| Need a valid component description file (default : sbs.xml).

Parameters
~~~~~~~~~~

* mandatory
   * *<component-path>* : path to component (i.e that contains a sbs.xml file)
* optional
   * *-t* : target test
   * *-b* : target both main and test
   * *-v* : verbose mode

Examples
~~~~~~~~

Compile a component :

.. code-block:: console

   > sbs compile .
   
Compile component tests :

.. code-block:: console

   > sbs compile . -t

Compile both component and component tests :

.. code-block:: console

   > sbs compile . -b
    
""""
  
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

""""

.. _target-create-component:

create-component
----------------

| Create a component from scratch.

Parameters
~~~~~~~~~~

* mandatory :
   * *<component-path>* : path to component to create
   * *<component-name>* : the component name
   * *<component-version>* : the component version
   * *<component-buildtype>* : the component build type (executable, static, shared)
* optional :
   *-o <sbs-file>* : select specific sbs xml file
   *-v* : verbose mode
   
Examples
~~~~~~~~

""""

.. _target-flags:

flags
-----

| Add/modify/remove compile flag(s) to component description.

Parameters
~~~~~~~~~~

Examples
~~~~~~~~

""""

.. _target-generate:

generate
--------

| Generate component and/or test CMake files in release or debug mode.
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

Generate CMake files for a component :

.. code-block:: console

   > sbs generate .
   
Generate CMake files for component tests :

.. code-block:: console

   > sbs generate . -t

Generate CMake files for both component and component tests :

.. code-block:: console

   > sbs generate . -b
   
Generate CMake files for component in debug mode :

.. code-block:: console

   > sbs generate . -d
   
Generate CMake files for a component using a specific component file :

.. code-block:: console

   > sbs generate . -i sbs-linux.xml

""""

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

""""

.. _target-repository:

repository
----------

| Generic target to handle repositories.
| Need global or component specific configuration.

Parameters
~~~~~~~~~~

Examples
~~~~~~~~

""""

.. _target-run:

run
---

| Run the component executable
| Need global or component specific configuration.
| Need a valid component description file (default : sbs.xml).

Parameters
~~~~~~~~~~

* mandatory
   * *<component-path>* : path to component (i.e that contains a sbs.xml file)
* optional
   * *-i <sbs-file>* : select specific sbs xml file
   * *-d* : debug build
   * *-v* : verbose mode

Examples
~~~~~~~~

Run an executable component :

.. code-block:: console

   > sbs run .
   
Run an executable component in debug mode :

.. code-block:: console

   > sbs run . -d
   
Run an executable component using a specific component file :

.. code-block:: console

   > sbs run . -i sbs-linux.xml

""""

.. _target-runtime-display:

runtime-display
---------------

| Display all library and executable dependency paths.

Parameters
~~~~~~~~~~

Examples
~~~~~~~~

""""

.. _target-test:

test
----

| Run the component tests
| Need global or component specific configuration.
| Need a valid component description file (default : sbs.xml).

Parameters
~~~~~~~~~~

* mandatory
   * *<component-path>* : path to component (i.e that contains a sbs.xml file)
* optional
   * *-i <sbs-file>* : select specific sbs xml file
   * *-d* : debug build
   * *-v* : verbose mode

Examples
~~~~~~~~

Run component tests :

.. code-block:: console

   > sbs test .
   
Run component tests in debug mode :

.. code-block:: console

   > sbs test . -d
   
Run component tests using a specific component file :

.. code-block:: console

   > sbs test . -i sbs-linux.xml
