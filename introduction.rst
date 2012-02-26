Introduction
============

What is SBS ?
-------------

SBS is an acronym for Screen Build System.
It is a build tool for C/C++ applications designed for Screen uses.
Thanks to its generic design, it could be used most C/C++ applications.

Aims
----

SBS was developed with some strict requirements in mind in order to follow Screen needs and evolutions :

* **Portability** :
   * SBS must work on Windows and Linux platforms (a Mac port could be done) and must be able to generate lots of kinds of makefiles and environment settings (Unix makefiles, Visual Studio projects, Wascana projects, etc...). SBS itself must be easily deployable on those platforms,
* **Simplicity** : 
   * Project descriptions must be easy to read and write, and must describe a minimum sort of items (include files, library names, compile flags, …),
   * External libraries, i.e that hasn't been compiled with SBS, must be easily integrated into SBS projects,
   * We could easily switch between environments,
* **Extensibility** : 
   * It could manage lots of projects at the same time. Screen is separated into many shared libraries, and new libraries are created all the time. SBS must handle these kinds of issues,
   * SBS must be able to integrate some specific user requirements (for example, generate code from Flex/Bison files directly with an SBS command).
   
Technologic choices
-------------------

Some technological choice had been made to develop SBS.

We chose Java as base language to develop SBS. There are several for this choice :

* Java is supported by lots of systems,
* the JRE contains some libraries very useful for SBS needs (XML parsing, external command calls, …),
* It possesses a very large community,
* Java helps us to avoid memory management issues,
* Java is free.

The other choice we made was to reuse existing toots as bases for SBS implementation.

The most improtant choice was to choose CMake as internal makefile and project generator.
The goal is to keep full CMake capabilities and to provide a simpler user interface. 

User interface
--------------

Files used by SBS must be user-friendly and extensible. 

SBS uses XML files to write project descriptions for several reasons :
XML files are easy to read and write for a developer,
project description format is extensible just by adding new tags or tag attributes,
XML files are easy to parse with Java

For configuration files, SBS uses propreties file confine with a JSON syntax or additional files.
