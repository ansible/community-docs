**************************
Contributing to a codebase
**************************

We follow the `Ansible Code of Conduct <https://docs.ansible.com/ansible/latest/community/code_of_conduct.html>`_ in all our contributions and interactions within the project.

This document explains how to contribute to a codebase. If you are interested to know all ways how you can help the project, refer to the Ansible's `Contribution guidelines <contribution_to_project.rst>`_.

If you find any inconsistencies or places in this document which can be improved, please raise an issue or pull request to fix it.

If you are a committer, also refer to the `Ansible committer guidelines <https://docs.ansible.com/ansible/devel/community/committer_guidelines.html>`_.

Feel free to link to this document from your ``CONTRIBUTING.md`` file.

Issue tracker
=============

Whether you are looking for an opportunity to contribute or you found a bug and already know how to solve it, please go to the collection's issue tracker first (the ``Issues`` tab).
There you can find feature ideas to implement, reports about bugs to solve, or submit an issue to discuss your idea before implementing it which can help choose a right direction at the beginning of your work and potentially save a lot of time and effort.
Also somebody may already have started discussing or working on implementing the same or a similar idea,
so you can cooperate to create a better solution together.

Many collections use ``easyfix`` or a similarly named label to indicate issues that are a good starting point for beginners (you might also look at the `newbie pinboard <https://github.com/ansible/community/issues/437>`_ if you do not know which collection to start with). Also ``waiting_on_contributor`` or similarly named labels often indicate that this is a feature that is deemed (potentially) useful, but none of the maintainers can invest time to actually implement it.

Open pull requests
==================

Look through the currently open pull requests in the collection repository (the ``Pull requests`` tab).
You can help by reviewing them. Reviews help move pull requests to merge state. Some good pull requests cannot be merged only due to a lack of reviews. For more information how to provide a good review, refer to the `review checklist <review_checklist.rst>`_. Also if you want to test a pull request, refer to the `test PR locally guide <test_pr_locally_guide.rst>`_.
And it is always worth saying that good reviews are often more valuable than pull requests themselves.

Also, consider taking up a valuable, reviewed, but abandoned pull request which you could politely ask the original authors to complete yourself.

Discussions
===========

For open questions, broad suggestions, and other comments that will not typically fit in the scope of an issue or pull request, GitHub discussions are available. Check if this feature is enabled in the repository (if enabled, there is the ``Discussions`` tab next to the ``Pull requests`` tab).

That section provides a place to have a more open and informal conversation about any and all things related to the collection, included but not limited to future development plans, functionality explanations and feature proposals that are not yet fleshed out enough for an issue of their own.

Looking for an idea to implement
================================

First, see the paragraphs above.

If you came up with a new feature, it is always worth creating an issue
to discuss the idea with the community first, before writing code.
If you are going to implement the feature yourself, say it in the issue explicitly to avoid working in parallel with somebody else.

Create your first pull request
==============================

When working on your patch, please take into consideration the following points:

- Try committing your changes with an informative but short commit message.
- Do not squash your commits and force-push to your branch if not needed. Reviews of your pull request are much easier with individual commits to comprehend the pull request history. All commits of your pull request branch will be squashed into one commit by GitHub upon merge.
- Do not add merge commits. You will have to `rebase <https://docs.ansible.com/ansible/latest/dev_guide/developing_rebasing.html>`_ your pull request to remove them before your work can be merged. To avoid that git automatically does merges during pulls, you can configure it to do rebases instead by running ``git config pull.rebase true`` inside the respository checkout.
- Make sure your pull request includes a `changelog fragment <https://docs.ansible.com/ansible/devel/community/development_process.html#changelogs-how-to>`_. You must not include a fragment for new modules or new plugins, except for test and filter plugins. Also you should not include one for docs-only changes. If you are not sure, simply do not include a fragment, we will tell you whether this is needed or not.
- Avoid reformatting unrelated parts of the codebase in your pull request. These types of changes will likely be requested for reversion, create additional work for reviewers, and may cause approval to be delayed.
- Please do not add more than one plugin/module in one pull request. That makes it easier for reviewers and increases the chance that your pull request will get merged.

To learn how to quickly create your first patch and submit a pull request, refer to the `Quick-start guide <create_pr_quick_start_guide.rst>`_
