.. _index:

.. SBS documentation master file, created by
   sphinx-quickstart on Sat Feb 25 11:04:07 2012.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.
   
Welcome to SBS's documentation!
===============================

SBS (Screen Build System) gives you an easy, component based way to create makefiles and configuration files for C/C++ project :

* Simple component decription with XML files
* Easy configuration
* *Maven-like* repository based strategy for easy dependency handling
* Support for multiple compilers toolchains and environments

How it works !!
---------------

Create your component file :

.. code-block:: xml

   <?xml version="1.0" encoding="UTF-8"?>
   <component>
      <properties>
         <name>HelloWorld</name>
         <version>1.0.0</version>
      </properties>
      <target name="main">
         <build type="cpp-executable">
            <include>
               <path path="src"/>
            </include>
            <source>
               <files path="src" filter="**/*.cpp,**/*.cc,**/*.c"/>
            </source>
            <output path="bin"/>
         </build>
         <public>
            <executable path="bin"/>
         </public>
      </target>
   </component>
   
Write your code :

.. code-block:: cpp

   #include <iostream>
   #include <cstdlib>
   
   int main(){
      std::cout << "Hello world !!" << std::endl;
      return EXIT_SUCCESS;
   }

Compile and run with SBS :

.. code-block:: console

   > sbs build .
   ...
   > sbs run .
   [INFO] ------------ begin SBS ------------
   [INFO] /home/user/.sbs/repositories/HelloWorld/1.0.0/exe/Linux/Release/./HelloWorld
   [INFO] Hello world !!
   [INFO] ------------- end SBS -------------
   [INFO] 
   [INFO] -----------------------------------
   [INFO]         COMMAND SUCCESSFUL         
   [INFO] -----------------------------------
