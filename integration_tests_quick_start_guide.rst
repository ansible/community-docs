*************************************
Quick-start integration testing guide
*************************************

This guide describes all steps needed to add integration tests for your changes to a collection.

.. contents:: Topics

Basics
======

.. note::

  If you find any inconsistencies or places in this document which can be improved / clarified, please raise an issue or pull request to fix it.

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

The test tasks are stored in the ``tests/integration/targets/<target_name>/tasks`` directory.

The ``main.yml`` file holds test tasks and includes other test files.
Look for a suitable test file to integrate your tests or create and include / import a separate test file.
You can use one of the existing test files as a draft.

When fixing a bug
-----------------

When fixing a bug, the process of adding tests looks basically like the following:

1. `Determine if integration tests for the module exists<Determine if integration tests exist>`_.
2. Add a task which reproduces it to an appropriate file within the ``tests/integration/targets/<target_name>/tasks`` directory.
3. `Run the tests<Run-integration-tests>`_, they should fail.
4. If they do not fail, re-check if your environment / test task satisfies the steps-to-reproduce section of the issue.
5. If you reproduce the bug and tests fail, change the code. 
6. `Run the tests<Run-integration-tests>`_ again.
7. Repeat steps 5-6 until the tests pass.

Here's an example.

Let's say we got an issue in the ``community.postgresql`` collection. When users pass a name containing underscores to the ``postgresql_user`` module, the module fails.

We cloned the collection repository to ``~/ansible_collections/community/postgresql``. Being there, we run ``ansible-test integration --list-targets`` and it shows a target called ``postgresql_user``. It means that we already have tests for the module.

We start with reproducing the bug.

First, we look into ``tests/integration/targets/<target_name>/tasks/main.yml``. In case of the ``community.postgresql``, it imports other files from the ``tasks`` directory. We looked through the files - ``postgresql_user_general.yml`` looks like an appropriate one to add our tests.

.. yaml::

  # General tests:
  - import_tasks: postgresql_user_general.yml
    when: postgres_version_resp.stdout is version('9.4', '>=')

We will add the following code to the file.

.. bash::

  # https://github.com/ansible-collections/community.postgresql/issues/NUM
  - name: Test user name containing underscore
    postgresql_user:
      name: underscored_user
    register: result

  - name: Check the module returns what we expect
    assert:
      that:
        - result is changed

  - name: Query the database if the user exists
    postgresql_query:
      query: SELECT * FROM pg_authid WHERE rolename = 'underscored_user'
    register: result

  - name: Check the database returns one row
    assert:
      that:
        - query_result.rowcount == 1

When we `run the tests<Run-integration-tests>`_ passing ``postgresql_user`` as a test target, this task must fail.

Then we will fix the bug and run the same test again. If they pass, we will consider the bug fixed and will submit a pull request.

When adding a new feature
-------------------------

.. note::

  The process described in this section is also applicable when the feature already exists but does not have integration tests and you want to cover it.

.. note::

  If you don not implement the feature you want yet, you can start with writing integration tests for it. Of course they will not work as the code does not exist at the moment but it can help you design better implementation before writing the code.

When adding new features, the process of adding tests consists of the following steps:

1. `Determine if integration tests for the module exists<Determine if integration tests exist>`_.
2. Find an appropriate file for your tests within the ``tests/integration/targets/<target_name>/tasks`` directory.
3. Cover your option. Refer to the `Cover properly<Cover-properly>`_ section for details.
4. `Run the tests<Run-integration-tests>`_.
5. If they fail, see the test output for details. Fix your code or tests and run the tests again.
6. Repeat steps 4-5 until the tests pass.

Here's an example.

Let's say we decided to add a new option called ``add_attribute`` to the ``postgresql_user`` module of the ``community.postgresql`` collection.

The option is boolean. If set to ``yes``, it adds an additional attribute to a database user.

We cloned the collection repository to ``~/ansible_collections/community/postgresql``. Being there, we run ``ansible-test integration --list-targets`` and it shows a target called ``postgresql_user``. It means that we already have tests for the module.

First, we look into ``tests/integration/targets/<target_name>/tasks/main.yml``. In case of the ``community.postgresql``, it imports other files from the ``tasks`` directory. We looked through the files - ``postgresql_user_general.yml`` looks like an appropriate one to add our tests.

.. yaml::

  # General tests:
  - import_tasks: postgresql_user_general.yml
    when: postgres_version_resp.stdout is version('9.4', '>=')

We will add the following code to the file.

.. bash::

  # https://github.com/ansible-collections/community.postgresql/issues/NUM
  - name: Test for new_option, create new user WITHOUT the attribute
    postgresql_user:
      name: test
      add_attribute: no
    register: result

  - name: Check the module returns what we expect
    assert:
      that:
        - result is changed

  - name: Query the database if the user does not have the attribute (it is NULL)
    postgresql_query:
      query: SELECT * FROM pg_authid WHERE rolename = 'underscored_user' AND attribute = NULL
    register: result

  - name: Check the database returns one row
    assert:
      that:
        - query_result.rowcount == 1

  - name: Test for new_option, create new user WITH the attribute
    postgresql_user:
      name: test
      add_attribute: yes
    register: result

  - name: Check the module returns what we expect
    assert:
      that:
        - result is changed

  - name: Query the database if the user has the attribute (it is TRUE)
    postgresql_query:
      query: SELECT * FROM pg_authid WHERE rolename = 'underscored_user' AND attribute = 't'
    register: result

  - name: Check the database returns one row
    assert:
      that:
        - query_result.rowcount == 1

When we `run the tests<Run-integration-tests>`_ passing ``postgresql_user`` as a test target.

We also put the same tasks with the ``check_mode: yes`` option to be sure our option works as expected in check mode as well.

If we expect a task to fail, we use the ``ignore_errors: yes`` option and check that the task actually failed and the message like below:

.. yaml::

  - name: Test for fail_when_true option
    postgresql_user:
      name: test
      fail_when_true: yes
    register: result
    ignore_errors: yes

  - name: Check the module fails and returns message we expect
    assert:
      that:
        - result is failed
        - result.msg == 'The message we expect'

.. _Writing-tests-from-scratch:

Writing tests from scratch
==========================

This section covers cases when:

- There are no integration tests for a collection / group of modules in a collection at all.
- You are adding a new module and you want to cover it.
- You want to cover a module that already exists but integration tests for the module are missed.

In other words, there are currently no tests for a module regardless of whether the module exists or not.

If the module already has tests, refer to the `Adding test to existing ones<Adding-tests-to-existing-ones>`_ section.

Here is a simplified example.

Let's say we are going to cover a new module in the ``community.abstract`` collection which interacts with some service.

We `checked<Determine if integration tests exist>`_ and figure out that there are no integration tests at all.

We should basically do the following:

1. Install and run the service.
2. `Cover our module with tests<Cover-properly>`_.
3. Create a test target.
4. `Run the tests<Run-integration-tests>`_.
5. Fix the code / tests if needed, run the tests again, and repeat the cycle until they pass.

If we expect that there are several targets that will require the service, we will create a special ``setup`` target that will be used by all the targets where needed.

[DRAFT maybe change it to a real example?]
1. Clone the collection to the ``~/ansble_collections/community.abstract`` directory on our local machine.

2. Being in ``~/ansble_collections/community.abstract``, create directories for the ``setup_`` target:

.. bash::

  mkdir -p tests/integration/targets/setup_abstract_service/tasks

3. Write all the tasks needed to prepare the environment, install, and run the service.

For simplicity, let's imagine that the service is available in the native distribution repositories and no sophisticated environment configuration is required.

Add the following tasks to the ``tests/integration/targets/setup_abstract_service/tasks/main.yml`` file to install and run the service:

.. yaml::

  - name: Install abstract service
    package:
      name: abstract_service

  - name: Run the service
    systemd:
      name: abstract_service
      state: started

This is a very simplified example. In real world, use all the best practices available to write this role.

4. Add the target for the module you test.

Let's say the module is called ``abstact_service_info``. Create a directory structure for the module:

.. bash::

  mkdir -p tests/integration/targets/abstract_service_info/tasks
  mkdir -p tests/integration/targets/abstract_service_info/meta

Add all subdirectories needed. For example, if you are going to use defaults and files, add the ``defaults`` and ``files`` directories, and so on. The approach is the same as you are creating a role.

5. To make the ``setup_abstract_service`` target running before the module's target, add the following lines to the ``tests/integration/targets/abstract_service_info/meta/main.yml`` file.

.. yaml::

  dependencies:
    - setup_abstract_service

6. Start with writing a single standalone task to check that your module can interact with the service.

We assume that the ``anstract_service_info`` module fetches some information from the ``abstract_service`` and it has two connection parameters.

Among other fields, it returns a field called ``version`` containing a service version.

Add the following to ``tests/integration/targets/abstract_service_info/tasks/main.yml``:

.. yaml::

  - name: Fetch info from abstract service
    anstract_service_info:
      host: 127.0.0.1  # We assume the service accepts local connection by default
      port: 1234       # We assume that the service is listening this port by default
    register: result   # This variable will contain the returned JSON including the server version

  - name: Test the output
    assert:
      that:
        - result.version == '1.0.0'  # Check version field contains what we expect

7. `Run the tests<Run-integration-tests>`_ with the ``-vvv`` argument.

If there are any issues with connectivity (for example, the service does not listening / accepting connections or anything else) or with the code, the play will fail.

Examine the output to see at which step the failure occurred. Investigate why, fix, and run again. Repeat the cycle until the test passes.

8. If the test succeeds, write more tests covering as many possible scenarios as possible. Refer to the `Cover properly<Cover-properly>`_ section for details.

.. _Cover-properly:

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
