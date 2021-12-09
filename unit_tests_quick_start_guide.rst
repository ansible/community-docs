******************************
Quick-start unit testing guide
******************************

This guide describes all of the steps needed to add unit tests to a collection and how to run them locally using the ``ansible-test`` command.

After getting started with this guide, refer to the `Unit testing Ansible modules <https://docs.ansible.com/ansible/devel/dev_guide/testing_units_modules.html>`_ documentation page to learn details.

.. contents:: Topics

Basics
======

.. note::

  If you find any inconsistencies or places in this document that can be improved / clarified, please raise an issue or pull request to fix it.

.. note::

  Some collections do not have unit tests but it does not mean they are not needed.

.. note::

  If there are any difficulties with writing / running unit tests or you are not sure if the case can be covered, feel free to submit your pull request without the tests. Other contributors can help you with them later if needed.

Unit tests are tests written to ensure that a section of code (known as ``unit``) meets its design and behaves as intended.

When we say ``unit``, we usually imply a function or method of a class used in a module or plugin.

With unit testing, we check if a function when it gets a certain input, returns an output that we expect.

If a function raises / handles exceptions, this should also be checked.

Ansible uses `pytest <https://docs.pytest.org/en/latest/>`_ as a testing framework.

To learn why use unit tests, refer to the `Unit testing Ansible modules <https://docs.ansible.com/ansible/devel/dev_guide/testing_units_modules.html#why-use-unit-tests>`_ documentation page.

It is a `requirement <https://github.com/ansible-collections/overview/blob/main/collection_requirements.rst#requirements-for-collections-to-be-included-in-the-ansible-package>`_ for inclusion of a collection to the Ansible package to have integration and / or unit tests. However, even if your collection already has / is going to have integration tests, it will probably make your code more reliable and bug-introduction sensitive if your modules are also covered by unit tests and vice versa. To learn how to get started with integration tests, see the `Quick-start integration testing guide <integration_tests_quick_start_guide.rst>`_.

.. _Prepare-local-environment:

Prepare local environment
=========================

Before starting on the unit tests themselves, in order to run them locally, you will need to prepare your environment. To learn how to do it quickly, refer to the `Quick-start development guide <https://github.com/ansible/community-docs/blob/main/create_pr_quick_start_guide.rst#prepare-your-environment>`_.

.. _Determine-if-unit-tests-exists:

Determine if unit tests exist
=============================

Ansible collection unit tests are located in the ``tests/units`` directory.

The structure of the unit tests matches the structure of the code base, so the tests can reside in the ``tests/units/plugins/modules/`` and ``tests/units/plugins/module_utils`` directories. There can be sub-directories, if, for example, modules are organized by module groups.

When you are thinking of adding unit tests for the module called, say, ``my_module``, to check if they already exist, see if there is a file in the collection's source tree with the path ``tests/units/plugins/modules/test_my_module.py``.

Example of unit tests
=====================

Let's assume that there is the following function in ``my_module``:

.. code:: python

  def convert_to_supported(val):
      """Convert unsupported types to appropriate."""
      if isinstance(val, decimal.Decimal):
          return float(val)

      if isinstance(val, datetime.timedelta):
          return str(val)

    if val == 42:
        raise ValueError("This number is just too cool for us ;)")

      return val

To test this function, we should, at least, check:

* If the function gets a ``Decimal`` argument, it returns a corresponding ``float`` value.
* If the function gets a ``timedelta`` argument, it returns a corresponding ``str`` value.
* If the function gets an argument of any other type, it does nothing and returns the same value.

Let's write a simple test.

Assuming that our collection is called ``community.mycollection``:

1. If you already have your local environment `prepared <https://github.com/ansible/community-docs/blob/main/create_pr_quick_start_guide.rst#prepare-your-environment>`_, go to the collection's root directory:

.. code:: bash

   cd ~/ansible_collection/community/mycollection

2. Create a test file for ``my_module`` (if the following path does not exist, create it):

.. code:: bash

    touch tests/units/plugins/modules/test_my_module.py

3. Add the following code to the file:

.. code:: python

  # -*- coding: utf-8 -*-

  from __future__ import (absolute_import, division, print_function)
  __metaclass__ = type

  from datetime import timedelta
  from decimal import Decimal

  import pytest

  from ansible_collections.community.mycollection.plugins.modules.my_module import (
      convert_to_supported,
  )

  # We use the @pytest.mark.parametrize decorator to parametrize the function
  # https://docs.pytest.org/en/latest/how-to/parametrize.html
  # Simply put, the first element of each tuple will be passed to
  # the test_convert_to_supported function as the test_input argument
  # and the second element of each tuple will be passed as
  # the expected argument.
  # In the function's body, we use the assert statement to check
  # if the convert_to_supported function given the test_input,
  # returns what we expect.
  @pytest.mark.parametrize('test_input, expected', [
      (timedelta(0, 43200), '12:00:00'),
      (Decimal('1.01'), 1.01),
      ('string', 'string'),
      (None, None),
      (1, 1),
  ])
  def test_convert_to_supported(test_input, expected):
      assert convert_to_supported(test_input) == expected

You can find examples of how to mock ``AnsibleModule`` objects, monkeypatch methods (``module.fail_json``, ``module.exit_json``), emulate API responses, and more on the `Unit testing Ansible modules <https://docs.ansible.com/ansible/devel/dev_guide/testing_units_modules.html>`_ documentation page.

4. Run the tests using docker:

.. code:: bash

  ansible-test units tests/unit/plugins/modules/test_my_module.py --docker

.. _Recommendations-on-coverage:

Recommendations on coverage
===========================

There are several tips related to organizing your code and test coverage:

* Small, doing one thing functions with no or minimum side effects are easier to test, so try to make your functions simple.
* Test all possible behaviors of a function including exception related ones like raising, catching and handling exceptions.
* When a function invokes the ``module.fail_json`` method, passed messages should also be checked.

Going deeper
============

For further review, refer to the following documents:

- `Unit testing Ansible modules <https://docs.ansible.com/ansible/devel/dev_guide/testing_units_modules.html>`_.
- `Pytest framework documentation <https://docs.pytest.org/en/latest/>`_.
- `Testing guide <https://docs.ansible.com/ansible/latest/dev_guide/testing.html>`_.
- `Quick-start integration testing guide <https://github.com/ansible/community-docs/blob/main/integration_tests_quick_start_guide.rst>`_.
- `Integration tests guide <https://docs.ansible.com/ansible/latest/dev_guide/testing_integration.html>`_.
- `Testing collections <https://docs.ansible.com/ansible/latest/dev_guide/developing_collections_testing.html#testing-collections>`_.
- `Resource module integration tests <https://docs.ansible.com/ansible/latest/network/dev_guide/developing_resource_modules_network.html#resource-module-integration-tests>`_.
- `How to test a pull request locally <https://github.com/ansible/community-docs/blob/main/test_pr_locally_guide.rst>`_.
