****************
Contributor path
****************

..

  "There is no favorable wind for the sailor who doesn’t know where to go."

  -- Seneca

This guide describes a contributor path in scope of the Ansible project from the early beginning, through all the stages, to becoming a leader shaping the project's future and the future of automation in the IT world in general.

This path is not a policy but rather a suite of recommendations based on experience of successful contributors.

The goal of the path, first of all, is to make your activity more determined and efficient through understanding of what you can achieve and how. You can use this path as a roadmap for your long-term participation.

Any contribution to the project, even a small one, is very welcome and valuable. When you contribute regularly, your proficiency and judgement in the related area are increasing fast and, along with this, the importance of your presence in the project.

Regular contribution makes you a member of the community and leads to respect of other community members.

Be persistent and act gradually. Great result is just a product of time and effort. Here's how to get started.

.. note::

   If you have any questions, feel free to reach out to the community in the ``#ansible-community`` `Libera.Chat <https://libera.chat/>`_ IRC channel. If you have ideas on how this document can be improved, please, share them through creating an issue or a pull request.

.. contents::

What is a contribution to an Open Source project
================================================

First, we should understand what a contribution to an Open Source project is.

The contribution to an Open Source project is any positive addition, change or feedback given by an individual (or company) to the project. It includes increasing its functionality, improving the codebase as well as developer experience and user experience, promoting the project and participating in the community, providing infrastructure, and any kind of active social or material support.

Note that, according to the classification given in the `Contribution to an Open Source project guide <contribution_to_project.rst>`_, most types of contribution do not require programming skills.

Determine areas of your interests
=================================

First, determine areas that are interesting to you taking into consideration your current experience and experience you'd like to gain.
There are some ideas about how you can contribute to the project listed in the `Contribution guide <contribution_to_project.rst>`_.

Determine the project
=====================

These are some of the community projects in the Ansible ecosystem you could contribute to:

  - `Ansible Core <https://docs.ansible.com/ansible-core/devel/index.html>`_
  - `Collections <https://docs.ansible.com/ansible/latest/user_guide/collections_using.html>`_
  - `AWX <https://github.com/ansible/awx>`_
  - `Galaxy <https://galaxy.ansible.com/>`_
  - `Lint <https://ansible-lint.readthedocs.io/en/latest/>`_
  - `Molecule <https://molecule.readthedocs.io/en/latest/>`_

Learn
=====

The required skillset depends on the area of interest and the project you'll be working on.

Knowledge required for programming
----------------------------------

The area that requires technical knowledge the most is programming. Let's sort out what an Ansible programmer should learn.

Fundamentals
~~~~~~~~~~~~

If you'd like to write code for the Ansible project, it would be good to understand at least *basics* of the following tools:

  - `Python programming language <https://docs.python.org/3/tutorial/>`_.
  - `Git <https://git-scm.com/docs/gittutorial>`_.
  - `GitHub collaborative development model through forks and pull requests <https://docs.github.com/en/github/collaborating-with-pull-requests/getting-started/about-collaborative-development-models>`_.

Project-specific guidelines
~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. note::

  You don't have to read the documentation mentioned below from cover to cover and memorize everything. It would be good to have general understanding of the workflow and what the documentation consists of to find information you need later when needed.

If you feel confident with the fundamentals above, you should also be familiar with the guidelines specific to the project you choose.

For example, for Ansible Core it is `Ansible development guidelines <https://docs.ansible.com/ansible/latest/dev_guide/index.html>`_.

If you'd like to develop a collection, you should be also familiar with the `Ansible collection development guidelines <https://docs.ansible.com/ansible/latest/dev_guide/developing_collections.html>`_ and development documentation for a particular collection (references can usually be found in the ``README`` or ``CONTRIBUTING`` files in the `collection's repository <https://github.com/ansible-collections/>`_).

Doing your first contribution
=============================


You can find some ideas how you can contribute in the `Contribution guide <contribution_to_project.rst>` and the ``README`` / ``CONTRIBUTING`` files of `corresponding repositories <https://github.com/ansible-collections/>`_.

If the contribution you'd like to give implies technical skills, there can be also quick-start guides which can help.

For example, for collections, you can use the `Quick-start development guide <create_pr_quick_start_guide.rst>`_ to learn how to set up everything you need quickly, test your changes, and submit a pull request.

To make your first experience as smooth as possible, read the repository documentation carefully, then ask the repository maintainers for guidance if you have any questions.

Looking for issues labeled with the ``easyfix``, ``good_first_issue``, and ``docs`` labels can help find good issues to start with.

Continue to contribute
======================

When you contribute regularly, your proficiency and judgment in the related area will improve quickly and, along with this, the importance of your presence in the project.

Communicate
===========

Join the channels
-----------------

Interact and share your ideas with other folks from the community following `Ansible Code of Conduct <https://docs.ansible.com/ansible/latest/community/code_of_conduct.html>`_.

You can find available communication channels in the `Communication guide <https://docs.ansible.com/ansible/devel/community/communication.html>`_.

The most interactive one is on Libera.Chat IRC where many Ansible projects and working groups have dedicated `channels <https://docs.ansible.com/ansible/devel/community/communication.html#irc-channels>`.

IRC meetings
------------

The important project-scale decisions are made by the community and the Steering Committee at weekly IRC meetings in the ``#ansible-community`` Libera.Chat IRC channel.

If you want to see what is on the agenda, refer to the issues in the `community-topics repository <https://github.com/ansible-community/community-topics>`_. If you want to submit a topic, create an issue in the repository.

The other important Libera.Chat IRC meetings impacting the whole project which you can join are:

  - the Ansible Core IRC meeting in the ``ansible-core`` channel.
  - the Documentation working group IRC meeting in the ``ansible-docs`` channel.

See the `meeting schedule <https://github.com/ansible/community/blob/main/meetings/README.md#schedule>`_.

The Bullhorn newsletter
-----------------------

Subscribe to `The Bullhorn newsletter <https://docs.ansible.com/ansible/devel/community/communication.html#the-bullhorn>`_ which is released biweekly and contains brief news important for the Ansible developer community.

Contributor summit
------------------

Take part and meet other contributors in the global quarterly `Ansible Contributor Summit <https://github.com/ansible/community/wiki/Contributor-Summit>`_ virtually or in-person.

Teach others
============

Share your experience with other contributors through `improving documentation <https://docs.ansible.com/ansible/latest/community/documentation_contributions.html>`_ on the doc site and in repositories, answering question from them on IRC, giving advice in issues and pull requests, and discussing the `community meeting topics <https://github.com/ansible-community/community-topics>`_.

Become a maintainer
===================

If you are a code contributor, you can get extended permissions in the repository and become a maintainer.

For more information about the collection maintenance, requirements, and nomination process, refer to the `Maintainer guidelines <maintaining.rst>`_.

Become a file maintainer
------------------------

.. note::

  This is applicable only for collections that have the `collection bot <https://github.com/ansible-community/collection_bot>`_ running there like `community.general <https://github.com/ansible-collections/community.general>`_ and `community.network <https://github.com/ansible-collections/community.network>`_.

Being a file maintainer is the stage prior to becoming a collection maintainer.

The file is usually a module or plugin. File maintainers have indirect commit rights implemented through the `collection bot <https://github.com/ansible-community/collection_bot>`_.

For more information about the file-scope maintenance, refer to the `"Module maintainers" <https://github.com/ansible/community-docs/blob/main/maintaining.rst#module-maintainers>`_ section of the `Maintainer guidelines <maintaining.rst>`_.

Get the supershipit permission
------------------------------

.. note::

  This is applicable only for collections that have the `collection bot <https://github.com/ansible-community/collection_bot>`_ running there like `community.general <https://github.com/ansible-collections/community.general>`_ and `community.network <https://github.com/ansible-collections/community.network>`_.

This is similar to being a file maintainer but the scope where a maintainer has the indirect commit is the whole repository.

Get the triage access
---------------------

Get the ``triage`` access to the repository that allows contributors manage issues and pull requests.

Get the write access
--------------------

Get the ``write`` access to the repository also known as ``commit``. In other words, become a committer.

This access level allows contributors to merge pull requests to the development branch as well as perform all the other activities listed in the `Maintainer guidelines <maintaining.rst>`_.

For information about permission levels, refer to the `GitHub official documentation <https://docs.github.com/en/organizations/managing-access-to-your-organizations-repositories/repository-permission-levels-for-an-organization>`_.

Become a steering committee member
==================================

.. note::

  You do NOT have to be a programmer to become a steering committee member.

The steering committee member status reflects the highest level of trust which allows contributors to lead the project through making very important `decisions <https://github.com/ansible-community/community-topics/issues>`_ of the Ansible project scope.

The committee members are the community leaders who shape the project's future and the future of automation in the IT world in general.

For more information about the steering committee, its mission, responsibilities, members, agenda, and meeting schedule, refer to the `Steering committee declaration <https://hackmd.io/nAHJNmBbSYm90KZM1RPK6w>`_.

To reach the status, as the current committee members did before getting it, along with the things mentioned in this document before:

  - Become a regular attendee in the `community meetings <https://github.com/ansible/community/blob/main/meetings/README.md#schedule>`_.
  - Track the `community topics <https://github.com/ansible-community/community-topics/issues>`_.
  - Try to think out and give a good judgement on the topics in comments and during the meetings.
  - Vote on the topics. Even if only members votes are counted to make final decisions, your voice is very important and appreciated for the committee.
  - Feel free to propose your topics.

Good judgement and regularity is all that you need.

If you have any questions, feel free to reach out to the current members directly in the ``ansible-community`` `Libera.Chat IRC channel <https://docs.ansible.com/ansible/devel/community/communication.html#irc-channels>`_.
