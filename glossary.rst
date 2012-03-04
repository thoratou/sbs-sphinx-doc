.. _glossary:

Glossary
========

.. glossary::

   configuration file
      Configuration files are unit files placed into SBS_HOME folder and with `.config` extension.
      
      Their goal is to configure SBS by setting several variables. 
   
   component
      A component is a set of libraries and/or executables, described by a file that contains all component properties.
      
      The component file could contain :
      
      * The basic component properties : name, version and component type (i.e executable, static or dynamic library).
      * Its dependency list.
      * Its compilation flags.

   SBS_HOME
      Folder that contains all configuration files, reposiroties and additional files needed by SBS
      
      Default values :
      
      * Under Linux : `$HOME/.sbs/` (example : `/home/user/.sbs/`)
      * Under Windows Vista/7 : `%USERPROFILE%/.sbs/` (example : `C:/Users/User/.sbs/`)
      * Under Windows XP : `%USERPROFILE%/.sbs/` (example : `C:/Documents and Settings/User/.sbs/`)
      
   SBS_ROOT
      Folder that contains all executables needed by SBS
      
   repository
      A repository is a component container. It contains "compiled" component descriptions, executable and libraries.
      
   sbs.xml
      This is the common user-side component descrption file.

   target
      The target is the first argument given into a sbs command.
      
      It indicate the kind of action that will be performed by SBS.
      
      For details on how to use targets, see :ref:`targets`.

   toolchain
      In SBS world, a toolchain is a set of tools that products executable(s)/library(ies) from source(s).
      
      The toolchain configuration is used by SBS to give the toochain information to CMake files.