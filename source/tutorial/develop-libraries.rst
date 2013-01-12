.. _tutorial-develop-libraries:

Develop libraries
=================

In this tutorial, you will create two versions of the same library, a static one and a dynamic one.
It consists into a simple library that returns de number 42.

You will also create an executable to call and display the result of the function given by the library.

Create a static library component
---------------------------------

As in previous pages, the component must be created from scratch. To do it, use the :ref:`create-component <target-create-component>` target as follows :

.. code-block:: console

   > sbs create-component . Lib42/Static 1.0.0 static
   
THe *sbs.xml* file should contain those data :

.. code-block:: xml

   <?xml version="1.0" encoding="UTF-8"?>
   <component>
      <properties>
         <name>Lib42/Static</name>
         <version>1.0.0</version>
      </properties>
      <target name="main">
         <build type="cpp-static">
            <include>
               <path path="include"/>
               <path path="src"/>
            </include>
            <source>
               <files path="src" filter="**/*.cpp,**/*.cc,**/*.c"/>
            </source>
            <output path="lib"/>
         </build>
         <public>
            <include>
               <path path="include"/>
            </include>
            <library path="lib"/>
         </public>
      </target>
   </component>

Here the include folder is added in both *build* and *delivery* parts,
as the client executables/libraries need to get explicitly the interface headers.

Now create the following files to implement the library :
   
*include/lib42.h* :

.. code-block:: cpp

   #ifndef LIB_42_H
   #define LIB_42_H

   int get42();
   
   #endif

*src/lib42.cpp* :

.. code-block:: cpp
   
   #include "lib42.h"

   int get42(){
      return 42;
   }

Now compile the library :

.. code-block:: console

   > sbs build .

Use your new static library
---------------------------

To use the previous library, you need to create an executable component :

.. code-block:: console

   > sbs create-component . Hello42 1.0.0 executable   
   
Then, add the dependency *Lib42/Static* in the component as follows :
   
.. code-block:: xml

   <?xml version="1.0" encoding="UTF-8"?>
   <component>
      <properties>
         <name>Hello42</name>
         <version>1.0.0</version>
      </properties>
      <target name="main">
         <build type="cpp-executable">
            <dependencies>
               <dependency name="Lib42/Static" version="1.0.0" target="main"/>
            </dependencies>
            <include>
               <path path="include"/>
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

At last, implement the *main.cpp* file.

*src/main.cpp*

.. code-block:: cpp

   #include <iostream>
   #include <cstdlib>
   #include "lib42.h"
   
   int main(){
      std::cout << "Hello " << get42() << std::endl;
      return EXIT_SUCCESS;
   }

Compile and run the executable.
   
Create a shared library component
---------------------------------

In the same way than the static library, use the :ref:`create-component <target-create-component>` target to create the shared library :

.. code-block:: console

   > sbs create-component . Lib42/Shared 1.0.0 shared

Then, modify the *sbs.xml* file to add the *LIB_42_BUILD_SHARED_LIBRARY* flag (no value needs to be set).
This technical flag you help us to create a fully portable shared library.

.. code-block:: xml

   <?xml version="1.0" encoding="UTF-8"?>
   <component>
      <properties>
         <name>Lib42/Static</name>
         <version>1.0.0</version>
      </properties>
      <target name="main">
         <build type="cpp-static">
            <flags>
               <flag flag="LIB_42_BUILD_SHARED_LIBRARY"/>
            </flags>
            <include>
               <path path="include"/>
               <path path="src"/>
            </include>
            <source>
               <files path="src" filter="**/*.cpp,**/*.cc,**/*.c"/>
            </source>
            <output path="lib"/>
         </build>
         <public>
            <include>
               <path path="include"/>
            </include>
            <library path="lib"/>
         </public>
      </target>
   </component>

Then, implement the library code sources.
   
*include/lib42export.h* :

.. code-block:: cpp

   #ifndef LIB_42_EXPORT_H
   #define LIB_42_EXPORT_H

   #ifdef WIN32
   #  ifdef LIB_42_BUILD_SHARED_LIBRARY
   #     define LIB_42_EXPORT __declspec(dllexport)
   #  else
   #     define LIB_42_EXPORT __declspec(dllimport)
   #  endif
   #else
   #  define LIB_42_EXPORT
   #endif
   
   #endif

*include/lib42.h* :

.. code-block:: cpp

   #ifndef LIB_42_H
   #define LIB_42_H

   #include "lib42export.h"

   LIB_42_EXPORT int get42();
   
   #endif

*src/lib42.cpp* :

.. code-block:: cpp
   
   #include "lib42.h"

   int get42(){
      return 42;
   }
   
Now compile the library :

.. code-block:: console

   > sbs build .
   

Use your new shared library
---------------------------

To use the previously created shared library, you will reuse the Hello42 component.
You need to change the *Lib42/Static* library by the *Lib42/Shared* one.

.. code-block:: xml

   <?xml version="1.0" encoding="UTF-8"?>
   <component>
      <properties>
         <name>Hello42</name>
         <version>1.0.0</version>
      </properties>
      <target name="main">
         <build type="cpp-executable">
            <dependencies>
               <dependency name="Lib42/Shared" version="1.0.0" target="main"/>
            </dependencies>
            <include>
               <path path="include"/>
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

Compile and run the executable.
