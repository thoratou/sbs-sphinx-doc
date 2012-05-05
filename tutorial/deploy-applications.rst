.. _tutorial-deploy-applications:

Deploy your applications
========================

Deploy components
-----------------

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

To use the *deploy.xml* file, just launch the following command :

.. code-block:: console

   > sbs deploy .
   
Deploy ressources
-----------------

