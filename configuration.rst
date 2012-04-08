.. _configuration:

Configuration
=============

Overview
--------

SBS configuration is based on a set of configuration files.
Actually, we need to use 2 kinds of configuration files :

* The user configuration. The default *user* configuration is enough in most of the cases
* The toolchain configuration. It indicates which compiler and environment you want to use.

Several preconfigured :ref:`toolchain configurations <available-toolchain>` are available on SBS.

You can also :ref:`create your own toolchain configurations <create-a-toolchain>`.

.. _available-toolchain:

Available toolchain configurations
----------------------------------

Here you can find a list of current officially supported toolchain configurations :

+--------------------+--------------------+--------------------+--------------------+
| Configuration file | Operating System   | Environments       | Toolchain          |
+====================+====================+====================+====================+
| linux              | Linux              | all (emacs, vim,   | gcc                |
|                    |                    | Eclipse C++,       |                    |
|                    |                    | QtCreator, ... )   |                    |
+--------------------+--------------------+--------------------+--------------------+
| mingw              | Windows            | QtCreator          | MingW              |
+--------------------+--------------------+--------------------+--------------------+
| msys               | Windows            | MSYS               | MingW              |
+--------------------+--------------------+--------------------+--------------------+
| msv8               | Windows            | Visual C++ 8       | Visual C++         |
+--------------------+--------------------+--------------------+--------------------+
| wascana            | Windows            | Wascana and        | MingW              |
|                    |                    | Eclipse C++        |                    |
+--------------------+--------------------+--------------------+--------------------+

Configure target
----------------

There is a unique target to choose configuration files with SBS, named *configure*.
Basically, you will use it as follows :

.. code-block:: console

   > sbs configure -g -e user -e <toolchain-configuration>

For example :

.. code-block:: console

   > sbs configure -g -e user -e linux
   [INFO] ------------ begin SBS ------------
   [INFO] ------------- end SBS -------------
   [INFO]
   [INFO] -----------------------------------
   [INFO] COMMAND SUCCESSFUL
   [INFO] -----------------------------------
   
The *-g* option indicates we create global configuration (i.e common to all components).

You can define configurations for a specific project using *-p <component-path>* instead.

The *-e <configuration>* indicates which configuration files will be used by SBS.

For complete configuration usage, look at :ref:`configure target <target-configure>`.
