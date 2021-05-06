***********************
Maintaining collections
***********************

.. contents:: Topics

What is the collection maintenance
==================================

A collection is an Open Source project.

If a community of any Open Source project can be logically divided into three groups: core members, contributors, and users, the collection maintainers are the core members of the collection.

The collection maintenance consists of the regular activities listed in this document.

Maintainers can divide the activities between each other, for example, someone can be a release manager and someone can be responsible for the collection documentation.

Besides that, collection maintainers are watching that their collections adhear the `Collection Requirements <https://github.com/ansible-collections/overview/blob/main/collection_requirements.rst>`_.

Who is a collection maintainer
==============================

A collection maintainer is a contributor trusted by the community who made significant and regular contributions to the project and showed themselves as a specialist in the related area and is able to manage the collection performing the tasks listed in this document.

A collection maintainer has extended permissions in the collection scope. For details, refer to :ref:`_collection-maintainers`.

How to become a maintainer
==========================

[DRAFT] Describe how, basically:
1. Contribute
2. Communicate
3. Stay persistent
4. Learn
5. Submit an application (maybe an issue under https://github.com/ansible/community ?)

Communication
=============

We follow the `Ansible Code of Conduct <https://docs.ansible.com/ansible/latest/community/code_of_conduct.html>`_ in all interactions within the project.

Be informed
-----------

Good communication is vital for prosperity of the project.

Moreover, collection maintainers should be informed about important changes that impact all or many
of the collections (for example, CI related) and act correspondingly to keep them up to date.

It is highly recommended to subscribe to the "Changes impacting collection contributors and maintainers" `GitHub issue <https://github.com/ansible-collections/overview/issues/45>`_ and the `Bullhorn newsletter <https://github.com/ansible/community/issues/546>`_.

Communication channels
----------------------

Collection contributors and maintainers communicate by:

  * the "Changes impacting collection contributors and maintainers" `GitHub issue <https://github.com/ansible-collections/overview/issues/45>`_
  * the Bullhorn newsletter:

    + use the link in this `issue <https://github.com/ansible/community/issues/546>`_ to subscribe to the newsletter
    + if you have something important to announce (for example, releases made recently), put a comment in the issue
  * IRC channels such as ``#ansible-community``, ``#ansible-devel``, and specific ones
  * Mailing lists
  * Collection pinboards, issues, and GitHub discussions in corresponding repositories
  * quarterly contributor summits
  * Ansible fests and local meetups

For more information about available IRC channels and mailing lists, refer to the `Ansible community documentation <https://docs.ansible.com/ansible/devel/community/communication.html>`_.

Weekly community IRC meetings
-----------------------------

The important project-scale decisions are made by the community and the streeting committee at weekly IRC meetings in the ``#ansible-community`` IRC channel. See the `meeting schedule <>https://github.com/ansible/community/blob/main/meetings/README.md#schedule>`_.

If you want to see what is on the agenda, refer to issues in the `community-topics repository <https://github.com/ansible-community/community-topics>`_. If you want to submit a topic, create an issue there.

Committing
==========

Maintainers review and merge pull requests following
the `Ansible Code of Conduct <https://docs.ansible.com/ansible/latest/community/code_of_conduct.html>`_,
`Review checklist <review_checklist.rst>`_, and the `Committer guidelines <https://docs.ansible.com/ansible/devel/community/committer_guidelines.html>`_.

There can be two kinds of maintainers: :ref:`_collection-maintainers` and :ref:`_module-maintainers`.

.. _collection-maintainers:

Collection maintainers
----------------------

Collection-scope maintainers are contributors who have the ``write`` or higher access level in a collection.

They have the commit right and can merge pull requests among other permissions.

If applicable, the collection maintainers expand a pull of module maintainers.

.. _module-maintainers:

Module maintainers
------------------

Module-scope maintainers exist in collections that have the `collection bot <https://github.com/ansible-community/collection_bot>`_,
for example `community.general <https://github.com/ansible-collections/community.general>`_
and `community.network <https://github.com/ansible-collections/community.network>`_.

Being a module maintainer is the stage prior to becoming a collection maintainer.

Module maintainers are contributors who are listed in ``.github/BOTMETA.yml``.

The scope can be any file (for example, a module or plugin), directory, or repository.

Because in most cases the scope is a module or group of modules, we call these contributors module maintainers.

The collection bot notifies module maintainers when issues / pull requests related to files they maintain are created.

Module maintainers have the indirect commit right implemented through
the `collection bot <https://github.com/ansible-community/collection_bot>`_.
When two module maintainers comment with the keywords ``shipit``, ``LGTM``, or ``+1`` a pull request
which changes a module they maintain, the collection bot will merge the pull request automatically.

For more information about the collection bot and its interface,
refer to the `Collection bot overview <https://github.com/ansible-community/collection_bot/blob/main/ISSUE_HELP.md>`_.

When a collection maintainer considers a contribution to a file significant enough
(it can be, for example, fixing a complex bug, adding a feature, providing regular reviews, and so on),
they can offer the author to become a module maintainer, in other words to add their GitHub login to ``.github/BOTMETA.yml``.

Module maintainers, as well as collection ones, act in accordance to the `Ansible Code of Conduct <https://docs.ansible.com/ansible/latest/community/code_of_conduct.html>`_, the `Review checklist <review_checklist.rst>`_, and the `Committer guidelines <https://docs.ansible.com/ansible/devel/community/committer_guidelines.html>`_.

Backporting
===========

Collection maintainers backport merged pull requests to stable branches
following the `semantic versioning <https://semver.org/>`_ and release policies of the collections.

For more information about the process, refer to the `Backporting guidelines <https://docs.ansible.com/ansible/devel/community/development_process.html#backporting-merged-prs-in-ansible-core>`_.

Backporting can be implemented automatically using GitHub bots (for example, with the `Patchback app <https://github.com/apps/patchback>`_) and labeling like it is done in `community.general <https://github.com/ansible-collections/community.general>`_ and `community.network <https://github.com/ansible-collections/community.network>`_.

Releasing
=========

Collection maintainers release all supported stable versions of the collections regularly,
provided that there have been enough changes to release.

Generally, releasing in the collections consists of:
1. Planning and announcement.
2. Generating a changelog.
3. Creating a release git tag and pushing it.
4. Automatic publishing the release tarball on `Ansible Galaxy <https://galaxy.ansible.com/>`_ by Zuul.
5. Final announcement.

For more information about the process, refer to the `Releasing guidelines <releasing.rst>`_.

Expanding contributors pool
===========================

[Draft] Ways to expand a contributors pool:
  * Looking for potential maintainer among current active contributors
  * Announcements
  * Training

Documentation
=============

Maintainers look after the collection documentation.

In particular, they are watching that documents of the collection scope, like ``README.md``, are relevant and timely updated and that modules / plugins documentation adhears the `Ansible documentation format <https://docs.ansible.com/ansible/devel/dev_guide/developing_modules_documenting.html>`_ and the `Style guide <https://docs.ansible.com/ansible/devel/dev_guide/style_guide/index.html#style-guide>`_.

Reviewing
=========

[Draft] What:
  * issues (including bug report analysis, proposal analysis)

    - review issues yourself first (use the review guide) as they can request
      breaking changes, non-idempotent modules, etc
    - ask if the author wants to implement / solve the issue themselves
    - point to the quick start guide offering the author / other contributors
      to implement / solve the issue
  * PRs (proposal analysis)

    - first review quickly patches yourself if they don't contain breaking changes, etc.
    - first response is important, mention maintainers / authors / people
      who already contributed to the code

They can accept or reject the proposed features / code changes

Solving
=======

[Draft] What:

  * issues (contributing guidelines when merged)
  * abandoned PRs (ask their author about difficulties, offer help, etc.)
