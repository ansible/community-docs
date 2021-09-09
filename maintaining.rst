***********************
Maintaining collections
***********************

Thank you for being / your interest to become a community collection maintainer.

This guide offers an overview of maintenance-related tasks, criteria for becoming a maintainer along with recommendations how to build healthy and active community around your collection.

The Ansible community hopes that you will find that maintaining a collection is as rewarding for you as having the collection content is for the wider community.

.. contents:: Topics:

Collection maintainership
=========================

What is the collection maintenance
----------------------------------

Ansible collections community can be logically divided into four major groups:

1. Steering committee members (make decisions in scope of all the collections included in Ansible package and related areas).
2. Maintainers.
3. Contributors.
4. Users.

Maintainers are people who are responsible for collection maintenance.

The collection maintenance consists of the regular activities listed in these guidelines.

In particular, collection maintainers:

- keep README, development guidelines, and other general collection :ref:`documentation<Documentation>` relevant,
- :ref:`review<Reviewing>` and :ref:`commit<Committing>` changes made by other contributors,
- :ref:`backport<Backporting>` changes to stable branches,
- address issues discovered to appropriate contributors,
- :ref:`release<Releasing>` collections,
- watch that collections adhere the `Collection Requirements <https://github.com/ansible-collections/overview/blob/main/collection_requirements.rst>`_,
- keep tracking changes announced in ``Changes impacting collection contributors and maintainers`` `GitHub issue <https://github.com/ansible-collections/overview/issues/45>`_ and timely update a collection in accordance with them,
- increase a number of active contributors and maintainers by :ref:`building healthy community<Expanding community>` around collections,
- revise this document regularly for updates and sharing their experience through changing it.

Who is a collection maintainer
------------------------------

A collection maintainer is a contributor trusted by the community who makes significant and regular contributions to the project and showed themselves as a specialist in the related area.

Collection maintainers have :ref:`extended permissions<Collection maintainers>` in the collection scope.

Collection maintainers satisfy the :ref:`requirements<Requirements for maintainers>`.

.. _Requirements for maintainers:

Requirements for maintainers
----------------------------

Maintainers act in accordance with `Ansible Code of Conduct <https://docs.ansible.com/ansible/latest/community/code_of_conduct.html>`_.

Maintainers (including candidates) have:

- History of multiple contributions to a collection.
- Excellent technical judgement in collection-related areas.
- Responsiveness to mentions in issues and pull requests.
- Responsiveness to issues and pull requests assigned to them.
- Read these guidelines and the linked documents.
- Subscribed to:

  + the collection repository they maintain (the ``Watch`` button → ``All activity``),
  + the `"Changes impacting collection contributors and maintainers" GitHub issue <https://github.com/ansible-collections/overview/issues/45>`_,
  + the `Bullhorn newsletter <https://github.com/ansible/community/wiki/News#the-bullhorn>`_.
- Knowledge and intention to manage a collection performing the tasks listed in these guidelines. Maintainers can divide responsibilities between each other.

How to become a maintainer
--------------------------

A person who is interested in becoming a maintainer and satisfies the :ref:`requirements<Requirements for maintainers>` may either self-nominate or be nominated by another maintainer.

To nominate a candidate, please create a GitHub issue in the relevant collection repository. If there is no response, the repository is not actively maintained, or the current maintainers do not have permissions to add the candidate, please create the issue under `ansible/community <https://github.com/ansible/community>`_ repository.

.. _Communication:

Communication
=============

We follow the `Ansible Code of Conduct <https://docs.ansible.com/ansible/latest/community/code_of_conduct.html>`_ in all interactions within the project.

Be informed
-----------

Good communication is vital for prosperity of the project.

Moreover, collection maintainers must be informed about important changes that impact all or many of the collections (for example, CI related) and act correspondingly to keep them up to date.

It is required for collection maintainers to be subscribed to the `"Changes impacting collection contributors and maintainers" GitHub issue <https://github.com/ansible-collections/overview/issues/45>`_ and the `Bullhorn newsletter <https://github.com/ansible/community/wiki/News#the-bullhorn>`_.

Communication channels
----------------------

Collection contributors and maintainers communicate through:

* the Bullhorn newsletter:

  + use the link in this `issue <https://github.com/ansible/community/issues/546>`_ to subscribe to the newsletter
  + if you have something important to announce (for example, releases made recently), put a comment in the issue
* IRC channels such as ``#ansible-community``, ``#ansible-devel``, and dedicated ones
* mailing lists such as `ansible-announce <https://groups.google.com/d/forum/ansible-announce>`_ and `ansible-devel <https://groups.google.com/d/forum/ansible-devel>`_
* collection pinboards, issues, and GitHub discussions in corresponding repositories
* quarterly Contributor Summits
* Ansible fests and local meetups

For more information about available IRC channels and mailing lists, refer to the `Ansible community documentation <https://docs.ansible.com/ansible/devel/community/communication.html>`_.

Contributor Summits
-------------------

Because our project is a community of individuals collaborating on making the world better through developing automation software, the social aspect is vital for the project's prosperity as for any community.

The quarterly Ansible Contributor Summit is a global event that provides our contributors a great opportunity to meet each other, communicate, share ideas, and see that there are other real persons behind the messages on IRC or GitHub. In other words, it gives a sense of community.

To make the community more robust, keep tracking the `Bullhorn newsletter <https://github.com/ansible/community/wiki/News#the-bullhorn>`_ for information when the next contributor summit will happen, invite contributors you know, and take part in the event together.

Weekly community IRC meetings
-----------------------------

The important project-scale decisions are made by the community and the Steering Committee at weekly IRC meetings in the ``#ansible-community`` IRC channel. See the `meeting schedule <https://github.com/ansible/community/blob/main/meetings/README.md#schedule>`_.

If you want to see what is on the agenda, refer to the issues in the `community-topics repository <https://github.com/ansible-community/community-topics>`_. If you want to submit a topic, create an issue in the repository.

.. _Committing:

Committing
==========

Maintainers review and merge pull requests following the `Ansible Code of Conduct <https://docs.ansible.com/ansible/latest/community/code_of_conduct.html>`_, `Review checklist <review_checklist.rst>`_, and the `Committer guidelines <https://docs.ansible.com/ansible/devel/community/committer_guidelines.html#general-rules>`_.

There can be two kinds of maintainers: :ref:`collection maintainers<Collection maintainers>` and :ref:`module maintainers<Module maintainers>`.

For the both kinds it is worth keeping in mind that “with great power comes great responsibility”.

.. _Collection maintainers:

Collection maintainers
----------------------

Collection-scope maintainers are contributors who have the ``write`` or higher access level in a collection.

They have the commit right and can merge pull requests among other permissions.

If applicable, the collection maintainers expand a pull of module maintainers.

.. _Module maintainers:

Module maintainers
------------------

Module-scope maintainers exist in collections that have the `collection bot <https://github.com/ansible-community/collection_bot>`_,
for example `community.general <https://github.com/ansible-collections/community.general>`_
and `community.network <https://github.com/ansible-collections/community.network>`_.

Being a module maintainer is the stage prior to becoming a collection maintainer.

Module maintainers are contributors who are listed in ``.github/BOTMETA.yml``.

The scope can be any file (for example, a module or plugin), directory, or repository.

Because in most cases the scope is a module or group of modules, we call these contributors as module maintainers.

The collection bot notifies module maintainers when issues / pull requests related to files they maintain are created.

Module maintainers have indirect commit rights implemented through the `collection bot <https://github.com/ansible-community/collection_bot>`_.
When two module maintainers comment with the keywords ``shipit``, ``LGTM``, or ``+1`` on a pull request
which changes a module they maintain, the collection bot will merge the pull request automatically.

For more information about the collection bot and its interface,
refer to the `Collection bot overview <https://github.com/ansible-community/collection_bot/blob/main/ISSUE_HELP.md>`_.

When a collection maintainer considers a contribution to a file significant enough
(it can be, for example, fixing a complex bug, adding a feature, providing regular reviews, and so on),
they can offer the author to become a module maintainer, in other words, to add their GitHub account to ``.github/BOTMETA.yml``.

Module maintainers, as well as collection ones, act in accordance to the `Ansible Code of Conduct <https://docs.ansible.com/ansible/latest/community/code_of_conduct.html>`_, the `Review checklist <review_checklist.rst>`_, and the `Committer guidelines <https://docs.ansible.com/ansible/devel/community/committer_guidelines.html>`_.

.. _Backporting:

Backporting
===========

Collection maintainers backport merged pull requests to stable branches
following the `semantic versioning <https://semver.org/>`_ and release policies of the collections.

For more information about the process, refer to the `Backporting guidelines <https://docs.ansible.com/ansible/devel/community/development_process.html#backporting-merged-prs-in-ansible-core>`_.

For convenience, backporting can be implemented automatically using GitHub bots (for example, with the `Patchback app <https://github.com/apps/patchback>`_) and labeling like it is done in `community.general <https://github.com/ansible-collections/community.general>`_ and `community.network <https://github.com/ansible-collections/community.network>`_.

.. _Releasing:

Releasing
=========

Collection maintainers release all supported stable versions of the collections regularly,
provided that there have been enough changes merged to release.

Generally, releasing in the collections consists of:

1. Planning and announcement.
2. Generating a changelog.
3. Creating a release git tag and pushing it.
4. Automatic publishing the release tarball on `Ansible Galaxy <https://galaxy.ansible.com/>`_ by `Zuul <https://dashboard.zuul.ansible.com/t/ansible/builds?pipeline=release>`_.
5. Final announcement.

For more information about the process, refer to the `Releasing guidelines <releasing_collections.rst>`_.

.. _Expanding community:

Expanding community
===================

.. note::

  If you discover good ways how to expand a community or make it more robust, please share them with other maintainers through changing this document.


Increasing a number of active contributors and maintainers
----------------------------------------------------------

Maintainers are interested in increasing a number of active long-term contributors for a collection they maintain.

Put a note in your ``README`` that the project is actively accepting new contributors.

Contributors are reviewers, issue or pull request authors, testers, maintainers, and all other people who help develop the project.

Every regular contributor was once a newcomer. Make the first experience as positive as possible to encourage the new people coming back.

Good development documentation makes contributors life much easier. Get feedback from new contributors if there were things they struggled with when working on their proposals and improve the documentation correspondingly.

Create the ``CONTRIBUTING`` file in your repository. In there, add a link to the `Quick-start guide <create_pr_quick_start_guide.rst>`_ as well as to other guidelines describing things specific to your collection.

Make contributors feel welcome. Greet and thank contributors impersonally in ``README`` and individually in their proposals.
Thank all participants after merging or closing a proposal.

Be responsive. Respond as quickly as possible. Even if you cannot review a proposal right now, greet and thank the author.

If your collection is not huge, add and keep updated the ``CONTRIBUTORS`` file listing all the contributors including issue reporters and refer to it from your ``README``. You can ask contributors to do it themselves or add a note about this to the development documentation of the collection.

Do not fix trivial non-critical bugs yourself. Instead, mentor a person who would like to contribute.
Mark issues with labels like ``easyfix``, ``waiting_on_contributor``, and ``docs``.
They will let newcomers know where they can find easy wins.

When reviewing an issue, if applicable, ask the author whether they want to fix the issue themselves providing the link to the `Quick-start guide <create_pr_quick_start_guide.rst>`_.

Conduct pull request days regularly. You could plan PR days, for example, in the last Friday of every month when you and other maintainers go through all open issues and pull requests focusing on old ones, asking people if you can help, and so on. If there are pull requests that look abandoned (for example, there is no response on your help offers since the previous PR day), announce that anyone else interested can complete the pull request.

Adopt a zero-tolerance policy towards behavior violating `Ansible Code of Conduct <https://docs.ansible.com/ansible/latest/community/code_of_conduct.html>`_. Add information to ``README`` how people can complain referring to the `"Policy violations" Code of Conduct section <https://docs.ansible.com/ansible/latest/community/code_of_conduct.html#policy-violations>`_.

Announce that the project needs new contributors and maintainers through available communication channels.

Promote active contributors satisfying :ref:`requirements<Requirements for maintainers>` to maintainers. Revise contributors activity regularly.

If your collection found new maintainers, announce that fact in the `Bullhorn newsletter <https://github.com/ansible/community/wiki/News#the-bullhorn>`_ and during the next Contributor Summit congratulating and thanking them for the work done. You can mention all the people promoted since the previous summit. Remember to invite the other maintainers to the Summit in advance.

Create the ``MAINTAINERS`` file and keep it updated.

Create a pinned issue which announces that the collection needs new maintainers and contributors providing links to the collection's CONTRIBUTING file and other documentation describing how to contribute to and maintain the collection (for example, it could contain a link to these guidelines).

If your collection is a part of Ansible (is shipped with Ansible package), highlight that fact at the top of the collection's README.

.. _Checklist:

Checklist
---------

In addition to the paragraph above, here is a checklist:

* Give newcomers first positive experience.
* Have good documentation containing sections / guidelines for newbies. 
* Make people feel welcome impersonally and individually.
* Use labels to show easy wins.
* Leave non-critical easy fixes to newcomers. Mentor them.
* Be quickly responsive.
* Conduct PR days regularly.
* Zero-tolerance policy towards behavior violating `Ansible Code of Conduct <https://docs.ansible.com/ansible/latest/community/code_of_conduct.html>`_.
* Put information how people can complain in your ``README`` and ``CONTRIBUTING`` file.
* Links to the `contributing.rst <contributing.rst>`_ and `Quick-start guide <create_pr_quick_start_guide.rst>`_, and other documentation in ``README``.
* Add and keep updated the ``CONTRIBUTORS`` and ``MAINTAINERS`` files.
* If the collection is a part of Ansible, mention it in ``README``.
* Create a pinned issue that the collection needs new maintainers and contributors.
* Look for new maintainers among active contributors.
* Announce that your collection needs maintainers.
* Take part and congratulate new maintainers in Contributor Summits.

Documentation
=============

Maintainers look after the collection documentation.

In particular, they are watching that documents of the collection scope, like ``README.md``, are relevant and timely updated and that modules / plugins documentation adheres the `Ansible documentation format <https://docs.ansible.com/ansible/devel/dev_guide/developing_modules_documenting.html>`_ and the `Style guide <https://docs.ansible.com/ansible/devel/dev_guide/style_guide/index.html#style-guide>`_.

.. _Reviewing:

Reviewing
=========

Maintainers can accept or reject proposed changes.

Maintainers review code proposals as well as reported issues following the `review checklist <review_checklist.rst>`_ in applicable parts and the recommendations mentioned in the :ref:`Expanding community<Expanding community>` paragraph.

Inclusion in Ansible
====================

If a collection is not included in Ansible (not shipped with Ansible package), maintainers can submit the collection for inclusion by creating a discussion under `ansible-collections/ansible-inclusion repository <https://github.com/ansible-collections/ansible-inclusion>`_. For more information, refer to the `repository's README <https://github.com/ansible-collections/ansible-inclusion/blob/main/README.md>`_.

Stepping down
=============

Maintainers should not step down silently. This is especially important when the collection has one or few active maintainer.

If you feel you don't have time to maintain your collection any more or for a long period of time, to prevent negative consequences for the collection and its community:

- Inform other maintainers about it.
- If the collection is under the ``ansible-collections`` organization, also inform the community team in the ``ansible-community`` `Libera.Chat IRC channel <https://docs.ansible.com/ansible/devel/community/communication.html#irc-channels>`_ or by email ``ansible-community@redhat.com``.
- Look at active contributors in the collection to find new maintainers among them. Discuss the potential candidates with other maintainers or with the community team.
- If you failed to find a replacement, create a pinned issue in the collection which announces that the collection needs new maintainers.
- Make the same announcement through the `Bullhorn newsletter <https://github.com/ansible/community/wiki/News#the-bullhorn>`_.
- Please be around to discuss potential candidates found by other maintainers or by the community team.

You can come back at any moment.
