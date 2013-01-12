.. _tutorial-improve-helloworld:

Define compilation flags with SBS
=================================

In this part, you will see different approaches in compilation flags handling with SBS.

You will reuse the previous Hello world example.

Use component flags
-------------------

First of all, the source code need to be changed in order to perform our tests. Modify you main.cpp in this way :

.. code-block:: cpp

   #include <iostream>
   #include <cstdlib>
   
   int main(){
      std::cout << HELLO_WORLD_TEXT << std::endl;
      return EXIT_SUCCESS;
   }

The easiest way to define compilation flags is to modify the sbs.xml file. For example :

.. code-block:: xml

   <?xml version="1.0" encoding="UTF-8"?>
   <component>
      <properties>
         <name>HelloWorld</name>
         <version>1.0.0</version>
      </properties>
      <target name="main">
         <build type="cpp-executable">
            <flags>
               <flag key="HELLO_WORLD_TEXT" value="Hello you !!" type="string"/>
            </flags>
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
   
Then compile and run it :

.. code-block:: console

   > sbs build .
   ...
   > sbs run .
   [INFO] ------------ begin SBS ------------
   [INFO] /home/user/.sbs/repositories/HelloWorld/1.0.0/exe/Linux/Release/./HelloWorld
   [INFO] Hello you !!
   [INFO] ------------- end SBS -------------
   [INFO] 
   [INFO] -----------------------------------
   [INFO]         COMMAND SUCCESSFUL         
   [INFO] -----------------------------------

Use component flags with different build modes
----------------------------------------------

SBS allow you to define specific definitions depending on the build mode, the toolchain, ...

Let's take the basic flag example fromthe beginning of this page and define different different texts between release and debug mode :

.. code-block:: xml

   <?xml version="1.0" encoding="UTF-8"?>
   <component>
      <properties>
         <name>HelloWorld</name>
         <version>1.0.0</version>
      </properties>
      <target name="main">
         <build type="cpp-executable">
            <flags>
               <flag key="HELLO_WORLD_TEXT" value="Hello release !!" type="string" mode="release"/>
               <flag key="HELLO_WORLD_TEXT" value="Hello debug !!" type="string" mode="debug"/>
            </flags>
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
   
Then compile and run it in release mode :

.. code-block:: console

   > sbs build .
   ...
   > sbs run .
   [INFO] ------------ begin SBS ------------
   [INFO] /home/user/.sbs/repositories/HelloWorld/1.0.0/exe/Linux/Release/./HelloWorld
   [INFO] Hello release !!
   [INFO] ------------- end SBS -------------
   [INFO] 
   [INFO] -----------------------------------
   [INFO]         COMMAND SUCCESSFUL         
   [INFO] -----------------------------------

Now let's try in debug mode :

.. code-block:: console

   > sbs build . -d
   ...
   > sbs run . -d
   [INFO] ------------ begin SBS ------------
   [INFO] /home/user/.sbs/repositories/HelloWorld/1.0.0/exe/Linux/Debug/./HelloWorld
   [INFO] Hello debug !!
   [INFO] ------------- end SBS -------------
   [INFO] 
   [INFO] -----------------------------------
   [INFO]         COMMAND SUCCESSFUL         
   [INFO] -----------------------------------

Use compiler flags
------------------

In the previous examples, only component flags (i.e that are sued by the component code) were used.
In this part, you take care about compiler flags.

There are currently 2 kinds of compiler flags :

* The "compiler" flags itself, that can define for example the level of code warnings used by the compiler (-Wall, ...). The compiler flags can be set with *cflags* and *cppflags* elements (depending if the C or C++ compiler is used).
* The linker flags, that is used by the linker (the *ld* executable for example). The element needed is *linkFLags*.

For example :

.. code-block:: xml

   <?xml version="1.0" encoding="UTF-8"?>
   <component>
      <properties>
         <name>HelloWorld</name>
         <version>1.0.0</version>
      </properties>
      <target name="main">
         <build type="cpp-executable">
            <flags>
               <cppflags text="-Wall -Werror" toolchain="x86-32_mingw"/>
               <linkflags text="-enable-auto-import" toolchain="x86-32_mingw"/>
            </flags>
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

In the same way, than component flags, you can define compiler flags for specific a build mode and/or toolchain.
