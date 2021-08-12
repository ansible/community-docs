*************************************
Quick-start integration testing guide
*************************************

This guide describes all steps needed to add integration tests for your changes to a collection.

.. contents:: Topics

Basics
======

[DRAFT POINTS NEED TO BE EXPLAINED BRIEFLY:]
- Brief notion of integration tests.
- Mention ``ansible-test``.
- How they basically works within Ansible (e.g. these are roles with tasks checked by assert statement on expected outcome, blah blah).
- Don't put references to the ansible integration testing doc here to NOT distruct and to NOT terrify newbies. 

Note: If there are any difficulties with writing / running integration tests or you are not sure if the case can be covered, feel free to submit your pull request without the tests.
If needed, other contributors can help you with them later.

Note: Some collections do not have integration tests.

Prepare local environment
=========================

Before starting working on integration tests, to be able to run them locally, you need to prepare your environment.

To learn how to do it quickly, refer to the `Quick-start development guide <https://github.com/ansible/community-docs/blob/main/create_pr_quick_start_guide.rst#prepare-your-environment>`_.

Determine if integration tests exist
====================================

Provided that integration tests for a collection exist, they are stored in ``tests/integration/targets`` subdirectories in the collection repository.

[DRAFT] Mention below that you must have your environment prepared and be in the collection root directory.
You can use the following command to list all the available targets:

.. bash::

  ansible-test integration --list-targets

Bash users
If you use ``bash`` and the ``argcomplete`` package is installed on your system, you can also get a full target list by doing: ``ansible-test integration <tab><tab>``.


[DRAFT POINTS NEED TO BE EXPLAINED BRIEFLY:]
- See the module / plugin you're interested in adding tests to in the output.

[DRAFT BELOW]
Go to the subdirectory containing the name of the module you are going to change.
For example, if you are fixing the ``mysql_user`` module in the ``community.mysql`` collection, its tests are in ``tests/integration/targets/test_mysql_user/tasks``.

The ``main.yml`` file holds test tasks and includes other test files.
Look for a suitable test file to integrate your tests or create and include a dedicated test file.
You can use one of the existing test files as a draft.

When fixing a bug, write a task which reproduces the bug from the issue.

Adding your tests to existing ones
==================================

When adding a new module
========================

Writing tests from scratch
==========================

Cover properly
==============

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
