.. _tutorial-dependencies:

Dependencies
============

Dependencies are an easy way to use external libraries in your projects.
Just by giving the name and the version of the component that contains the library,
you can use it without knowing all this specificities (include and library paths, full library name, used flags, etc ...).

In this, part, you will not create a complete library (you will see it in the next page), 
but you will use a library component taken from an SBS server.
You will not see in details how works SBS servers, repositories and components in this page,
but only the way to declare and retrieve components.

For this tutorial purpose, the **glm** library is used.

Retrieve component from remote SBS server
-----------------------------------------

Today you are lucky, I give you all you need to retrieve the component from the SBS server.
To declare all the components you can retrieve from an SBS server, you will use a *crumble* file.

*crumble* stands for *Component and Repository Unified Manifest BundLE*. It contains :

* The server information that are needed by SBS it call its services.
* For each server, the repository information.
* For each repository, the component information.

First, you just need to download the *crumble* file for this tutorial (**link to add here**).
You should have those data into the *crumble* file :

.. code-block:: xml

   <?xml version="1.0" encoding="UTF-8"?>
   <crumble>
      <server name="screenlib3d" path="screenlib3d.com" port="58553">
         <repository name="tutorial" location-type="remote" delivery="release">
            <component name="glm" version="0.9.2.3" toolchain="x86-32_mingw" buildmode="release" />
            <component name="glm" version="0.9.2.3" toolchain="x86-32_mingw" buildmode="debug" />
         </repository>
      </server>
   </crumble>

Then, give it to SBS by using the command :

.. code-block:: console

   > sbs feed dependency-tuto.crumble
   ...

That's it, the *glm* component is registered, now, let's see how to use it.

Use a library component
-----------------------

First of all, in a new folder, create a component named *Hello/GLM* :

.. code-block:: console

   > sbs create-component . HelloWorld 1.0.0 executable

Then write the code into the *main.cpp* file :


.. code-block:: cpp

   #include <iostream>
   #include <cstdlib>
   #include <glm/glm.hpp>
   
   int main(){
      glm::vec3 aOrigin(0.0f, 0.0f, 0.0f);
      std::cout << aOrigin[0] << std::endl;
      return EXIT_SUCCESS;
   }

If you try to compile it, you'll see *glm/glm.hpp* and *glm::vec3* don't exist.

To fix it, the *glm* component needs to be declared into the *sbs.xml* file :

.. code-block:: xml

   <?xml version="1.0" encoding="UTF-8"?>
   <pack>
      <properties>
         <name>Hello/GLM</name>
         <version>1.0.0</version>
         <type>executable</type>
      </properties>
      <main>
         <dependencies>
            <dependency name="glm" version="0.9.2.3"/>
         </dependencies>
         <build>
            <files path="src" filter="*.cpp,*.cc,*.c,*.hpp,*.h,*.i" recursive="true"/>
            <output path="exe"/>
         </build>
         <delivery>
            <files path="exe"/>
         </delivery>
      </main>
   </pack>

Now compile and run.
