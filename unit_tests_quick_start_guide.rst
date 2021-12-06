******************************
Quick-start unit testing guide
******************************

# TODO: re-read Ansible unit testing docs once more
# TODO: mention collection requirements here
# TODO: mention that even if a collection has integration tests, it's not a requirement but a good idea
        to have things covered by unit tests and vice versa
# TODO: briefly explain why they are important
# TODO: Add refs to Ansible unit testing doc pages to the end of this doc

This guide describes all of the steps needed to add unit tests to a collection and how to run them locally using the ``ansible-test`` command.

.. contents:: Topics

Basics
======

.. note::

  If you find any inconsistencies or places in this document that can be improved / clarified, please raise an issue or pull request to fix it.

.. note::

  Some collections do not have unit tests but it does not mean they are not needed.

.. note::

  If there are any difficulties with writing / running unit tests or you are not sure if the case can be covered, feel free to submit your pull request without the tests. Other contributors can help you with them later if needed.

This section provides only a brief explanation of what unit tests are. The following sections will provide details and examples.

Unit tests are tests written to ensure that a section of code (known as ``unit``) meets its design and behaves as intended.

When we say ``unit``, we usually imply a function or method of a class used in a module or plugin.

With unit testing, we check if a function when it gets a certain input, returns an output that we expect.

If a function raises / handles exceptions, this should also be checked.

Ansible uses `pytest <https://docs.pytest.org/en/latest/>`_ as a testing framework.

.. _Prepare-local-environment:

Prepare local environment
=========================

Before starting on the unit tests themselves, in order to run them locally, you will need to prepare your environment.

To learn how to prepare your environment quickly, refer to the `Quick-start development guide <https://github.com/ansible/community-docs/blob/main/create_pr_quick_start_guide.rst#prepare-your-environment>`_.

.. _Determine-if-unit-tests-exists:

Determine if unit tests exist
=============================

# Point to where they live.

.. _Run-unit-tests:

Example of unit tests
=====================

# Add note that this is not a full guide but just a couple of examples.

# It should cover
# - @pytest.mark_parametrized
# - simple example of using monkey patching
# - check exceptions

# This mustn't be a novel. We should just show how it works.

# Add a reference to pytest official doc here.

Run unit tests
==============

.. _Recommendations-on-writing-code:

Recommendations on writing code
===============================

.. _Recommendations-on-coverage:

Recommendations on coverage
===========================

Going deeper
============

# Add refs to Ansible docs here
