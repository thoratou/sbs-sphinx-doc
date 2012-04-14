.. _tutorial-improve-helloworld:

Define compilation flags with SBS
=================================

In this part, we will see different approaches in compilation flags handling with SBS.

We will reuse the previous Hello world example.

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
   <pack>
      <properties>
         <name>HelloWorld</name>
         <version>1.0.0</version>
         <type>executable</type>
      </properties>
      <main>
         <flags>
            <flag key="HELLO_WORLD_TEXT" value="Hello you !!" type="string"/>
         </flags>
         <build>
            <files path="src" filter="*.cpp,*.cc,*.c,*.hpp,*.h,*.i" recursive="true"/>
            <output path="exe"/>
         </build>
         <delivery>
            <output path="exe" public="true"/>
         </delivery>
      </main>
   </pack>
   
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

Use imports
-----------

For big projects (i.e that contains several libraries and executables), 
an other way to define compilation flags is to write them in a common component file, 
and import this common one in other ones.

To do it, create an *import.xml* file in the component root folder and write :

.. code-block:: xml

   <?xml version="1.0" encoding="UTF-8"?>
   <pack>
      <properties>
         <name>HelloWorld/Import</name>
         <version>1.0.0</version>
         <type>component</type>
      </properties>
      <main>
         <flags>
            <flag key="HELLO_WORLD_TEXT" value="Hello from import !!" type="string"/>
         </flags>
      </main>
   </pack>

Then, modify the *sbs.xml* :

.. code-block:: xml

   <?xml version="1.0" encoding="UTF-8"?>
   <pack>
      <properties>
         <name>HelloWorld</name>
         <version>1.0.0</version>
         <type>executable</type>
      </properties>
      <main>
         <imports>
            <import file="import.xml" />
         </imports>
         <build>
            <files path="src" filter="*.cpp,*.cc,*.c,*.hpp,*.h,*.i" recursive="true"/>
            <output path="exe"/>
         </build>
         <delivery>
            <output path="exe" public="true"/>
         </delivery>
      </main>
   </pack>

Then compile and run it :

.. code-block:: console

   > sbs build .
   ...
   > sbs run .
   [INFO] ------------ begin SBS ------------
   [INFO] /home/user/.sbs/repositories/HelloWorld/1.0.0/exe/Linux/Release/./HelloWorld
   [INFO] Hello from import !!
   [INFO] ------------- end SBS -------------
   [INFO] 
   [INFO] -----------------------------------
   [INFO]         COMMAND SUCCESSFUL         
   [INFO] -----------------------------------

