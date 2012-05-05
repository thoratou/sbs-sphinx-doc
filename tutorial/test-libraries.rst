.. _tutorial-test-libraries:

Test your libraries
===================

In the previous page, you created 2 libraries, *Lib42/Static* and *Lib42/Shared*.
In this tutorial, you will learn how to create unit tests for those libraries.

Create basic tests
------------------

In this part, you will reuse *Lib42/Static*.

To create unit test in a component, you need to use the :ref:`add-test <target-add-test>` target :

.. code-block:: console

   > sbs add-test .

You should have this output :

.. code-block:: xml

   <?xml version="1.0" encoding="UTF-8"?>
   <pack>
      <properties>
         <name>Lib42/Static</name>
         <version>1.0.0</version>
         <type>static</type>
      </properties>
      <main>
         <build>
            <files path="include" filter="*.hpp,*.h,*.i" recursive="true"/>
            <files path="src" filter="*.cpp,*.cc,*.c,*.hpp,*.h,*.i" recursive="true"/>
            <output path="lib"/>
         </build>
         <delivery>
            <files path="include" filter="*.hpp,*.h,*.i" recursive="true"/>
            <output path="lib"/>
         </delivery>
      </main>
      <test>
         <build>
            <files path="." filter="*.cpp,*.cc,*.c,*.hpp,*.h,*.i" recursive="true"/>
            <output path="exe"/>
         </build>
      </test>
   </pack>

The *test* folder has been created.

In this folder, add the *main.cpp* file.

*test/main.cpp* :

.. code-block:: cpp
   
   #include <iostream>
   #include <cstdlib>
   #include "lib42.h"
   
   int main(){
      bool aIsOK = (get42() == 42)
      std::cout << (aIsOK ? "OK" : "KO")  << std::endl;
      return aIsOK ? EXIT_SUCCESS : EXIT_FAILURE;
   }
   
Now you can compile and run the tests by using the build and test targets :

.. code-block:: console

   > sbs build . -b //build both the library and the test
   > sbs build . -t //build only the test
   > sbs test . //run the test

Test with cppunit
-----------------

The goal in this part is to use cppunit to generate unit tests for the *Lib42/Shared* component.

First you must retrieve the *cppunit* component from the remote server by using the *crumble file* (**link to add here**).

.. code-block:: xml

   <?xml version="1.0" encoding="UTF-8"?>
   <crumble>
      <server name="screenlib3d" path="screenlib3d.com" port="58553">
         <repository name="tutorial" location-type="remote" delivery="release">
            <component name="cppunit" version="1.12.1" toolchain="x86-32_mingw" buildmode="release" />
            <component name="cppunit" version="1.12.1" toolchain="x86-32_mingw" buildmode="debug" />
         </repository>
      </server>
   </crumble>

Then, give it to SBS by using the command :

.. code-block:: console

   > sbs feed cppunit-tuto.crumble


Now add the test part to *Lib42/Shared* :

.. code-block:: console

   > sbs add-test .

And modify the *sbs.xml* file to add the *cppunit* dependency :

.. code-block:: xml

   <?xml version="1.0" encoding="UTF-8"?>
   <pack>
      <properties>
         <name>Lib42/Static</name>
         <version>1.0.0</version>
         <type>static</type>
      </properties>
      <main>
         <build>
            <files path="include" filter="*.hpp,*.h,*.i" recursive="true"/>
            <files path="src" filter="*.cpp,*.cc,*.c,*.hpp,*.h,*.i" recursive="true"/>
            <output path="lib"/>
         </build>
         <delivery>
            <files path="include" filter="*.hpp,*.h,*.i" recursive="true"/>
            <output path="lib"/>
         </delivery>
      </main>
      <test>
         <dependencies>
            <dependency name="cppunit" version="1.12.1"/>
         </dependencies>
         <build>
            <files path="." filter="*.cpp,*.cc,*.c,*.hpp,*.h,*.i" recursive="true"/>
            <output path="exe"/>
         </build>
      </test>
   </pack>

Now implement the following test files :

*test/main.cpp* :

.. code-block:: cpp
   
   #include <cppunit/BriefTestProgressListener.h>
   #include <cppunit/CompilerOutputter.h>
   #include <cppunit/extensions/TestFactoryRegistry.h>
   #include <cppunit/TestResult.h>
   #include <cppunit/TestResultCollector.h>
   #include <cppunit/TestRunner.h>
   #include <cppunit/XmlOutputter.h>
   #include <iostream>
   
   int main(){
      // Create the event manager and test controller
      CPPUNIT_NS::TestResult controller;
      
      // Add a listener that collects test result
      CPPUNIT_NS::TestResultCollector result;
      
      controller.addListener(&result);
      
      // Add a listener that print dots as test run.
      CPPUNIT_NS::BriefTestProgressListener progress;
      
      controller.addListener(&progress);
      
      // Add the top suite to the test runner
      CPPUNIT_NS::TestRunner runner;
      runner.addTest(CPPUNIT_NS::TestFactoryRegistry::getRegistry().makeTest());
      runner.run(controller);
      
      // Print test in a compiler compatible format.
      CPPUNIT_NS::CompilerOutputter outputter(&result, CPPUNIT_NS::stdCOut());
      outputter.write();
      
      // Uncomment this for XML output
      std::ofstream file("cppunit-report.xml");
      
      CPPUNIT_NS::XmlOutputter xml(&result, file);
      
      xml.write();
      
      file.close();
      
      return 0;
   }
   
*test/test42.hpp* :

.. code-block:: cpp   

   #ifndef TEST_42_H
   #define TEST_42_H
   
   #include <cppunit/TestFixture.h>
   #include <cppunit/extensions/HelperMacros.h>
   
   class Test : public CppUnit::TestFixture {
      CPPUNIT_TEST_SUITE(Test);
      CPPUNIT_TEST(test42);
      CPPUNIT_TEST_SUITE_END();
   public:      
      void test42();
   };
   
   #endif
   
*test/test42.cpp* :

.. code-block:: cpp   

   #include "test/test42.hpp"
   #include "lib42.h"
   
   CPPUNIT_TEST_SUITE_REGISTRATION(Test);
   
   void Test::test42(){
      CPPUNIT_ASSERT(get42() == 42);
   }
   
Now you can compile and run the tests by using the build and test targets :

.. code-block:: console

   > sbs build . -b
   > sbs test .
