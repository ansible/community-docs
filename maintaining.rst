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

(Maybe it's worth putting this section content
to contributing.rst and a reference to it here?
Because it's relevant for all contributors, not only for maintainers)

Describe importance of being informed

Describe importance of communication in general (ref to CoC)

Ways:

  * Highly recommended:

    - changes impacting collection contributors and maintainers issue
    - Bullhorn newsletter:

      + subscription
      +  use the issue (ref here) to announce important changes / releases of the collection
    - contributor summits
    - community pinboards
    - IRC channels (#ansible-community, #ansible-devel, and dedicated ones if exist)
  * Optional:

    - weekly community IRC meetings
    - mailing lists

Committing
==========

Maintainers merge pull requests following the `Review checklist <review_checklist.rst>`_ and
the `Committer guidelines <https://docs.ansible.com/ansible/devel/community/committer_guidelines.html>`_.

There can be two kinds of maintainers: collection-scope maintainers and module-scope maintainers.

Collection-scope maintainers
----------------------------

Collection-scope maintainers are contributors who have the ``write`` or higher access level in a collection.

They have the commit right and can merge pull requests among other permissions.

If applicable, the collection-scope maintainers expand a pull of module-scope maintainers.

Module-scope maintainers
------------------------

This kind of maintainers exists in collections that have the `collection bot <https://github.com/ansible-community/collection_bot>`_,
for example `community.general <https://github.com/ansible-collections/community.general>`_
and `community.network <https://github.com/ansible-collections/community.network>`_.

Module-scope maintainers are contributors who are listed in ``.github/BOTMETA.yml``.

The scope can be a file (for example, a module or plugin), directory, or repository.

Because in most cases the scope is a module or group of modules, we call these contributors module-scope maintainers.

The collection bot notifies module-scope maintainers when issues / pull requests related to files they maintain are created.

Module-scope maintainers have the indirect commit right implemented through
the `collection bot <https://github.com/ansible-community/collection_bot>`_.
When two module maintainers comment with the keywords ``shipit``, ``LGTM``, or ``+1`` a pull request
which changes a module they maintain, the collection bot will merge the pull request automatically.

For more information about the collection bot and its interface,
refer to the `Collection bot overview <https://github.com/ansible-community/collection_bot/blob/main/ISSUE_HELP.md>`_.

When a collection-scope maintainer considers a contribution to a file significant enough
(it can be, for example, fixing a complex bug, adding a feature, providing regular reviews, and so on),
they can offer the author to become a maintainer, in other words to add their GitHub login to ``.github/BOTMETA.yml``.

The wording of the offer can be::

  Thank you @... for the contribution!

  Would you like to be added to a corresponding team in `.github/BOTMETA.yml` as a maintainer of the module?

  We have a bot in this collection which is tracking the issues/pull requests including for keywords
  such as `shipit`; the full list is [here](https://github.com/ansible-community/collection_bot/blob/main/ISSUE_HELP.md).

  If your GitHub login is listed in `.github/BOTMETA.yml` as a maintainer of a module and
  you'll put `shipit`, `LGTM`, or `+1` in a pull request that touches the module, the bot will count your `shipit`.
  If another maintainer also puts `shipit` (so we need two), the pull request will be merged by the bot automatically.
  So being a maintainer in `github/BOTMETA.yml` is the indirect commit privilege.

  The bot also notifies module maintainers when related issues and pull requests are created.

  Module-scope maintainers who are active and provide regular significant contributions (reviews and code contributions)
  in a collection scope can be granted the `write` access to the repository.
  In other words, they become collection-scope maintainers and can merge others' pull requests, release the collection, and so on.

  We have the [review checklist](https://github.com/ansible/community-docs/blob/main/review_checklist.rst) and
  the [contributing guidelines](https://github.com/ansible/community-docs/blob/main/contributing.rst)
  to help maintainers on their journey.

  What do you think?

  Thank you!

Backporting
===========

Explain, add a ref after writing a guide

Nuances in c.g. / c.n

=========
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
