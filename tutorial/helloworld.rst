.. _tutorial-helloworld:

Basic Example
=============

In this tutorial, we will create a basic C++ *Hello world* example.

Configuration
-------------

First of all, you need to indicate to sbs which user configuration and toolchain you want to use.

Follow the :ref:`configuration page <configuration>` tutorial to prepare a basic configuration.

Component overview
------------------

A component is a basic unit description to declare your executable or library.
It contains most of the information needed by SBS to compile your component, such as dependencies, compilation flags, ...

Basically, a component contains :

* a *sbs.xml* file, that describes all the properties, dependencies and flags.
* an *include* folder, that contains all public header files (your *.h* or *.hpp* files).
* a *src* folder, that contains your source files (*.c*, *.cpp*, ...).

Each component needs at least 3 data into the *sbs.xml* file to be able to compile it :

* Its **name**, (for example *boost*, *cppunit*, *SFML*, *Screen/Utils*, ...). By convention, if your component name is composed of several names, seperate them with a */* (slash).
* The **version**, (for example *1.42*). By convention, seperate major/minor/patch/... numbers with a *.* (point).
* The component **type**. Supported : *executable*, *static* (for static library), *shared* (for shared library), *component* (for generic components).

Component creation
------------------

In the previous part, we saw all needed information to create the basic *Hello world* example.
SBS provides a simple target to create this basic component : :ref:`create-component <target-create-component>`.
It can simply be used as follow :

.. code-block:: console

   > sbs create-component <component-path> <component-name> <component-version> <component-type>

For this tutorial, we set the name to *HelloWorld* and the version to *1.0.0* :

.. code-block:: console

   > sbs create-component . HelloWorld 1.0.0 executable
   [INFO] ------------ begin SBS ------------
   [INFO] ------------- end SBS -------------
   [INFO]
   [INFO] -----------------------------------
   [INFO] COMMAND SUCCESSFUL
   [INFO] -----------------------------------
   

you have now generated your component. You should see the *sbs.xml* file and the *include* and *src* folders.
open the generated *sbs.xml* file to verify its data :

.. code-block:: xml

   <?xml version="1.0" encoding="UTF-8"?>
   <pack>
      <properties>
         <name>HelloWorld</name>
         <version>1.0.0</version>
         <buildtype>executable</buildtype>
      </properties>
   </pack>
   
Now, you need to code your executable. To do this, create the *src/main.cpp* file and write the code :

.. code-block:: cpp

   #include <iostream>
   #include <cstdlib>
   
   int main(){
      std::cout << "Hello world !!" << std::endl;
      return EXIT_SUCCESS;
   }

Your component is now ready to be compiled and run.

Component build and run
-----------------------

As your component is ready, you can now generate CMake files and compile it by using the :ref:`build target<target-build>` :

.. code-block:: console

   > sbs build .
   [INFO] ------------ begin SBS ------------
   [INFO] cmake . -G Unix Makefiles --no-warn-unused-cli
   [INFO] Not searching for unused variables given on the command line.
   [INFO] -- The C compiler identification is GNU
   [INFO] -- The CXX compiler identification is GNU
   [INFO] -- Check for working C compiler: /usr/bin/gcc
   [INFO] -- Check for working C compiler: /usr/bin/gcc -- works
   [INFO] -- Detecting C compiler ABI info
   [INFO] -- Detecting C compiler ABI info - done
   [INFO] -- Check for working CXX compiler: /usr/bin/c++
   [INFO] -- Check for working CXX compiler: /usr/bin/c++ -- works
   [INFO] -- Detecting CXX compiler ABI info
   [INFO] -- Detecting CXX compiler ABI info - done
   [INFO] -- Configuring done
   [INFO] -- Generating done
   [INFO] -- Build files have been written to: /home/thoratou/tmp
   [INFO] make -j 2 all
   [INFO] Scanning dependencies of target HelloWorld
   [INFO] [100%] Building CXX object CMakeFiles/HelloWorld.dir/src/main.cpp.o
   [INFO] Linking CXX executable /home/thoratou/.sbs/repositories/HelloWorld/1.0.0/exe/Linux/Release/HelloWorld
   [INFO] [100%] Built target HelloWorld
   [INFO] ------------- end SBS -------------
   [INFO] 
   [INFO] -----------------------------------
   [INFO]         COMMAND SUCCESSFUL         
   [INFO] -----------------------------------

As you can see, before component compilation, CMake will verify your toolchain configuration.

If CMake toolchain checks fail, please refer to the :ref:`toubleshooting page<toubleshooting>`.

As your component is biult now, you can run it by using the :ref:`run target<target-run>` :

.. code-block:: console

   > sbs run .
   [INFO] ------------ begin SBS ------------
   [INFO] /home/thoratou/.sbs/repositories/HelloWorld/1.0.0/exe/Linux/Release/./HelloWorld
   [INFO] Hello world !!
   [INFO] ------------- end SBS -------------
   [INFO] 
   [INFO] -----------------------------------
   [INFO]         COMMAND SUCCESSFUL         
   [INFO] -----------------------------------

Clean component build
---------------------

You can clean the component builds and generated CMake files by using the :ref:`clean target<target-clean>` :

.. code-block:: console

   > sbs clean .


Component build and run in debug mode
-------------------------------------

Each component could be compile in both release or debug mode.

The debug mode will allow you to have additional information into debuggers (gdb, ...), and to add specific compilation flags if needed.

In the previous part, we only compiled in release mode.
To handle the debug mode, use the *-d* option on different targets :

.. code-block:: console

   > sbs build . -d
   > sbs run . -d
