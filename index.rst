.. SBS documentation master file, created by
   sphinx-quickstart on Sat Feb 25 11:04:07 2012.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.
   
Welcome to SBS's documentation!
===============================

SBS gives you an easy, component based way to create makefiles and configuration files for C/C++ project :

* Simple component decription with XMl files
* Easy configuration
* *Maven-like* Repository based strategy for easy dependency handling
* Support for multiple compilers toolchains and environments

Hello world
===========

First of all, indicate to sbs which user configuration and toolchain you want to use.

Here, the default user configuration and gcc+makefile.

.. code-block:: console

   > sbs configure -g -e user -e linux
   [INFO] ------------ begin SBS ------------
   [INFO] ------------- end SBS -------------
   [INFO]
   [INFO] -----------------------------------
   [INFO] COMMAND SUCCESSFUL
   [INFO]-----------------------------------

You can now generate you component description.

*Component generation* :

.. code-block:: console

   > sbs create-component . HelloWorld 1.0.0 executable
   [INFO] ------------ begin SBS ------------
   [INFO] ------------- end SBS -------------
   [INFO]
   [INFO] -----------------------------------
   [INFO] COMMAND SUCCESSFUL
   [INFO]-----------------------------------
   
*Output component file (sbs.xml)* :

.. code-block:: xml

   <?xml version="1.0" encoding="UTF-8"?>
   <pack>
      <properties>
         <name>HelloWorld</name>
         <version>1.0.0</version>
         <buildtype>executable</buildtype>
      </properties>
   </pack>
   
Now, create the src/main.cpp file and write your code :

.. code-block:: cpp

   #include <iostream>
   #include <cstdlib>
   
   int main(){
      std::cout << "Hello world !!" << std::endl;
      return EXIT_SUCCESS;
   }

Compile with SBS :

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

And run the executable :

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

Contents
========

.. toctree::
   :maxdepth: 2

   introduction
   installation
   tutorial


Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`

