.. _builder_overview:

************************
Ansible Builder Overview
************************

.. contents::
   :local:


The Ansible Builder (``ansible-builder``) is a tool for building
:ref:`Execution Environments<ee_overview>` container images (hereinafter, EE)
which represent :ref:`Ansible control nodes<terminology>`.

In order to build the images, you need to install a few packages as explained
in the :ref:`How to prepare your environment to build and test EEs<how_to_prepare_environment>` guide.

If you want to experiment along the reading, create the following directories where:

* ``test_ee`` is just your work directory
* ``test_ee/demo`` is a container build context directory

.. code-block:: bash

  $ mkdir test_ee && cd test_ee
  $ mkdir demo


Build and test your first EE
============================

If you are eager to see EEs in action, use the :ref:`How To Build and Test Your First EE<how_to_build_and_test_first_ee>` guide and then come back to learn the details.


Basic operations
================

TBD

Ansible Builder provides the following basic operations:

* build
* create
* introspect: TODO READ DOCS IN REPO, FILE ISSUES

ansible-builder create --context demo

Files used by Ansible Builder
=============================

TBD

Definition file
---------------

The ``ansible-builder build``

In case you need only ``ansible-core`` in your EE image, the minimal version of the file is:

.. code-block:: yaml

  ---
  version: 1




Galaxy requirements file
------------------------

TBD

Python requirements file
------------------------

TBD

System-level requirements file
------------------------------

TBD

Section N
---------

TBD
