.. _tutorial-deploy-applications:

Deploy your components
======================

Deploy applications
-------------------

In previous part, you learned how to create executable and libraries with SBS.
There is one basic thing you need to learn about it : how to easy retrieve your executable/library.

Especially when your projet gets lots of dependencies, you want to automate your application deployment.

SBS will help you in this way, as you can describe all you need in a *deploy.xml* file.
This time, you need to manually create the xml file.

*deploy.xml* :

.. code-block:: xml

   <?xml version="1.0" encoding="UTF-8"?>
   <deploy>
      <dependencies>
         <dependency name="Lib42/Shared" version="1.0.0.0">
            <files path="lib">
               <output path="output"/>
            </files>            
         </dependency>
         <dependency name="Hello42" version="1.0.0.0">
            <files path="exe">
               <output path="output"/>
            </files>            
         </dependency>
      </dependencies>
   </deploy>
   
In this file, you will take the generated file from *Lib42/Shared* and *Hello42*,
i.e the shared library and the executable, and put them in the *output* folder.

To use the *deploy.xml* file, just by using the :ref:`deploy <target-deploy>` target :

.. code-block:: console

   > sbs deploy . .

Deploy libraries
----------------

If you develop an API instead of an application,
you will need to need to provide the library and the header files for this library.

In the same way than deploying an application,
you just have to specify the *include* and *lib* paths into the *deploy.xml* file.

*deploy.xml* :

.. code-block:: xml

   <?xml version="1.0" encoding="UTF-8"?>
   <deploy>
      <dependencies>
         <dependency name="Lib42/Shared" version="1.0.0.0">
            <files path="include" filter="*.hpp,*.h,*.i" recursive="true">
               <output path="output/include"/>
            </files>            
            <files path="lib">
               <output path="output/lib"/>
            </files>            
         </dependency>
      </dependencies>
   </deploy>

As usual, use the :ref:`deploy <target-deploy>` target to deploy your API :

.. code-block:: console

   > sbs deploy . .
   
Deploy resources
----------------

In some cases, you need to deploy other resources than source codes or binary files (images, license files, ...).
Those resources are not part of your components, you need to get outside the dependency scope.

The *deploy.xml* file handles this case without any issue, just by specifying the files as follows.

In this case, just a README file will be added.

*deploy.xml* :

.. code-block:: xml

   <?xml version="1.0" encoding="UTF-8"?>
   <deploy>
      <dependencies>
         <dependency name="Lib42/Shared" version="1.0.0.0">
            <files path="lib">
               <output path="output"/>
            </files>            
         </dependency>
         <dependency name="Hello42" version="1.0.0.0">
            <files path="exe">
               <output path="output"/>
            </files>            
         </dependency>
      </dependencies>
      <files path="resources" filter="README">
         <output path="output"/>
      </files>
   </deploy>
   
*README* :
   
.. code-block:: none

   Lib42 example using SBS

As usual, use the :ref:`deploy <target-deploy>` target.

.. code-block:: console

   > sbs deploy . .
