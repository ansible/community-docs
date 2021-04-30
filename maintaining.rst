***********************
Maintaining collections
***********************

.. contents:: Topics

What is maintenance and what it includes?

  * point 1 (ref to the paragraph)
  * point 2 (ref to the paragraph)
  * point 3 (ref to the paragraph)

How to become a maintainer
==========================

Describe how

Communication
=============

We follow the `Ansible Code of Conduct <https://docs.ansible.com/ansible/latest/community/code_of_conduct.html>`_
in all interactions within the project.

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

The important project-scale decisions are made by the community and the streeting committee at weekly IRC meetings in the ``#ansible-community`` IRC channel. If you want to see what is on the agenda, refer to issues in the `community-topics repository <https://github.com/ansible-community/community-topics>`_. If you want to submit a topic, create an issue there.

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

Explain, add a ref after writing a guide

Nuances in c.g. / c.n

Releasing
=========

(ref to releasing guidelines when merged)

Expanding contributors pool
===========================

Ways to expand a contributors pool:

  * Looking for potential maintainer among current active contributors
  * Announcements
  * ...

Reviewing
=========

What:

  * issues

    - review issues yourself first (use the review guide) as they can request
      breaking changes, non-idempotent modules, etc
    - ask if the author wants to implement / solve the issue themselves
    - point to the quick start guide offering the author / other contributors
      to implement / solve the issue
  * PRs

    - first review quickly patches yourself if they don't contain breaking changes, etc.
    - first response is important, mention maintainers / authors / people
      who already contributed to the code

Solving
=======

What:

  * issues (contributing guidelines when merged)
  * abandoned PRs (ask their author about difficulties, offer help, etc.)
