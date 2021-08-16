*************************************
Quick-start integration testing guide
*************************************

This guide describes all steps needed to add integration tests for your changes to a collection.

.. contents:: Topics

Basics
======

.. note::

  Some collections do not have integration tests.

.. note::

  If there are any difficulties with writing / running integration tests or you are not sure if the case can be covered, feel free to submit your pull request without the tests. Other contributors can help you with them later if needed.

This section provides only brief explanation of what integration tests are. You will learn details and will see examples in the following sections.

Integration tests are functional tests of modules and plugins. We will use the word ``module`` throughout the document implying both modules and plugins.

With this kind of tests, we check if a module as a whole satisfies its functional requirements. Simply put, we check that features work and work as expected. In other words, users will get the outcome described in the module's documentation.

We check modules with playbooks that invoke those modules. We pass standalone parameters and their combinations, and check what the module reports with the ``assert`` module and the actual state of the system after each task.

Here's an example.

Let's say we want to test the ``postgresql_user`` module invoked with the ``name`` option. We expect that after its invocation the module will create a user that we are passing through the ``name`` option and will report that the system state has changed. We cannot rely on only what the module reports. To be sure that the user has been actually created, we will query our database with another module to see if the user exists.

.. bash::

  - name: Create PostgreSQL user and store module's output to the result variable
    postgresql_user:
      name: test_user
    register: result

  - name: Check the module returns what we expect
    assert:
      that:
        - result is changed

  - name: Check actual system state with another module, in other words, that the user exists
    postgresql_query:
      query: SELECT * FROM pg_authid WHERE rolename = 'test_user'
    register: query_result

  - name: We expect it returns one row, check it
    assert:
      that:
        - query_result.rowcount == 1

You will learn details in the following sections.

The basic entity of Ansible integration tests is a ``target``.

The target is an `Ansible role <https://docs.ansible.com/ansible/latest/user_guide/playbooks_reuse_roles.html>`_ stored in the ``tests/integration/targets`` directory of a collection repository file tree.

The target role contains all needed to test a module.

Names of targets contain a module name they test.

Target names that start with ``setup_`` are usually run as dependencies before module and plugin targets start execution. We will describe this kind of targets later in detail in the `Writing tests from scratch<Writing-tests-from-scratch>`_ section.

To run integration tests, we use the ``ansible-test`` utility shipped with the ``ansible-core`` and ``ansible`` packages. This is described in the `Run integration tests<Run-integration-tests>`_.

.. _Prepare-local-environment:

Prepare local environment
=========================

Before starting working on integration tests, to be able to run them locally, you need to prepare your environment.

To learn how to do it quickly, refer to the `Quick-start development guide <https://github.com/ansible/community-docs/blob/main/create_pr_quick_start_guide.rst#prepare-your-environment>`_.

Determine if integration tests exist
====================================

Provided that integration tests for a collection exist, they are stored in ``tests/integration/targets`` subdirectories in the collection repository.

If you already have your local environment `prepared<Prepare-local-environment>`_, you can run the following command being in the collection's root directory to list all the available targets:

.. bash::

  ansible-test integration --list-targets

If you use ``bash`` and the ``argcomplete`` package is installed on your system, you can also get a full target list by doing: ``ansible-test integration <tab><tab>``.
Alternatively, you can check if the ``tests/integration/targets`` contains a corresponding directory named as the module.

For example, the tests for the ``postgresql_user`` module of the ``community.postgresql`` collection are stored in the ``tests/integration/targets/postgresql_user`` directory of the collection's source tree.

If there is no corresponding target there, it means that the module does not have integration tests. In this case, think of adding integration tests for the module. Refer to the `Writing tests from scratch<Writing-tests-from-scratch>`_ section for details.

.. _Adding-tests-to-existing-ones:

Adding your tests to existing ones
==================================

[DRAFT]
The test tasks are stored in the ``tests/integration/targets/<target_name>/tasks`` directory.

The ``main.yml`` file holds test tasks and includes other test files.
Look for a suitable test file to integrate your tests or create and include a dedicated test file.
You can use one of the existing test files as a draft.

When fixing a bug, write a task which reproduces the bug from the issue.

[ELABORATE]

.. _Writing-tests-from-scratch:

Writing tests from scratch
==========================

This section covers cases when:

- There are no integration tests for a collection / group of modules in a collection at all.
- You are adding a new module and you want to cover it.
- You want to cover a module that already exists but integration tests for the module are missed.

In other words, there are currently no tests for a module regardless of whether the module exists or not.

If the module already has tests, refer to the `Adding test to existing ones<Adding-tests-to-existing-ones>`_ section.

[ELABORATE]

Cover properly
==============

.. _Run-integration-tests:

Run integration tests
=====================

[DRAFT IS ALL BELOW]
When fixing a bug, write a task which reproduces the bug from the issue.

Put the reported case in the tests, then run integration tests with the following command:

.. code:: bash

  ansible-test integration name_of_test_subdirectory --docker -v

For example, if the tests files you changed are stored in ``tests/integration/targets/test_mysql_user/``, the command will be:

.. code:: bash

  ansible-test integration test_mysql_user --docker -v

You can use the ``-vv`` or ``-vvv`` argument, if you need more detailed output.

In the examples above, the default test image will be automatically downloaded and used to create and run a test container.
Use the default test image for platform independent integration tests such as those for cloud modules.

If you need to run the tests against a specific distribution, see the `list of supported container images <https://docs.ansible.com/ansible/latest/dev_guide/testing_integration.html#container-images>`_. In this case, the command can look like:

Going deeper
============

[DRAFT] Doc references here
