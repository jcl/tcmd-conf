==================================
 My Total Commander configuration
==================================


This repository contains my configuration for the `Total Commander`_ Windows
application.

The configuration does not include any file system paths specific to my
environment(s), which means you should be able to use it as-is without any
surprises (outside of my preferences).

.. _`Total Commander`: https://www.ghisler.com/


How to use
==========

Deploy for the currently logged in user:

#. Clone this git repository into the ``%APPDATA%\`` directory
   (usually will be something like: ``C:\Users\username\AppData\Roaming\``),
   and name the clone directory ``tcmd`` .

#. Add configuration to ``HKEY_CURRENT_USER`` registry hive:

   To import `.bootstrap/set_up_HKEY_CURRENT_USER_reg4.reg`_
   execute this in a cmd.exe shell::

       reg.exe import .bootstrap\set_up_HKEY_CURRENT_USER_reg4.reg

.. TODO add how to deploy for the default user template?

.. _`.bootstrap/set_up_HKEY_CURRENT_USER_reg4.reg`:
   .bootstrap/set_up_HKEY_CURRENT_USER_reg4.reg


Tested on
=========

All configuration/code in this repository tested on the following:

* Total Commander 10.52 x64, installed on Windows 10 Enterprise version 21H2

It will likely work on earlier/newer versions/OS'es as well.


Background and extras
=====================

* `Background [.doc/background.rst]`_
* `Installing Total Commander [.doc/installing-tcmd.rst]`_

.. _`Background [.doc/background.rst]`: .doc/background.rst
.. _`Installing Total Commander [.doc/installing-tcmd.rst]`: .doc/installing-tcmd.rst
