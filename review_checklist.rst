****************
Review Checklist
****************

When reviewing, keep in mind that we follow the `Ansible Code of Conduct <https://docs.ansible.com/ansible/latest/community/code_of_conduct.html>`_ in all our contributions and interactions within this repository.

Social aspects:

  - Try to create a culture of collaboration when reviewing.
  - Welcome the author and thank them for the issue or pull request.
  - If there is a non-crucial easy-fix bug reported, politely ask the author to fix it themselves providing a link to the `Quick-start guide <create_pr_quick_start_guide.rst>`_.
  - When suggesting changes, try to use questions, not statements.
  - When suggesting mandatory changes, do it as politely as possible providing documentation references.
  - If your suggestion is optional or a matter of personal preferences, please say it explicitly.
  - When asking for adding tests or for complex code refactoring, say that the author is welcome to ask for clarifications and help if they need.
  - If somebody suggests a good idea, mention it or put a thumbs up.
  - After merging, thank the author and reviewers for their time and effort.

If you are a committer, also refer to the `Ansible committer guidelines <https://docs.ansible.com/ansible/devel/community/committer_guidelines.html>`_.

Reviewing bug reports
=====================

When users report bugs, the first thing that is needed is to verify the behaviour.

* [ ] Verify if the user made an obvious mistake in the example code. We often see user errors reported as bugs.
* [ ] The user does not expect an unexpected behavior. The related documentation is clear.
* [ ] There is a minimal reproducer. If not, ask the reporter to reduce the complexity to help pinpoint the issue.
* [ ] The issue is not a consequence of wrong-configured environment.
* [ ] If it looks a real bug, does the behaviour still exist in the most recent release or the development branch?
* [ ] You reproduced the bug.
* [ ] If you do not have a suitable infrastructure, other contributors have reproduced the bug.

What the suggested changes MUST NOT do
======================================

When reviewing, first, try to figure out that the suggested changes (including made through feature requests):

* [ ] Do NOT unnecessarily break backwards compatibility.
* [ ] Do NOT bring more harm than value.
* [ ] Do NOT introduce not idempotent solutions.
* [ ] Do NOT duplicate already existing features (inside or outside the collection).
* [ ] Do NOT violate the `Ansible development conventions <https://docs.ansible.com/ansible/devel/dev_guide/developing_modules_best_practices.html#following-ansible-conventions>`_.

Standards and documentation
===========================

* [ ] If the pull request is not a documentation fix, it must include a `changelog fragment <https://docs.ansible.com/ansible/devel/community/development_process.html#creating-a-changelog-fragment>`_ - please check the format carefully.

  * The only exception are new modules and plugins (that are not jinja2 filter and test plugins).
  * For jinja2 filter and test plugins, check out the `special syntax for changelog fragments <https://github.com/ansible-community/antsibull-changelog/blob/main/docs/changelogs.rst#adding-new-roles-playbooks-test-and-filter-plugins>`_.
* [ ] If new files are added with the pull request, they follow the `licensing rules <https://github.com/ansible-collections/overview/blob/main/collection_requirements.rst#licensing>`_.
* [ ] The changes follow the `Ansible documentation standards <https://docs.ansible.com/ansible/devel/dev_guide/developing_modules_documenting.html>`_ and the `Style guide <https://docs.ansible.com/ansible/devel/dev_guide/style_guide/index.html#style-guide>`_.
* [ ] The changes follow the `Development conventions <https://docs.ansible.com/ansible/devel/dev_guide/developing_modules_best_practices.html>`_.
* [ ] If a new plugin is added, it is one of the `allowed plugin types <https://github.com/ansible-collections/overview/blob/main/collection_requirements.rst#modules-plugins>`_.
* [ ] Documentation, examples, and return sections use FQCNs for the ``M(..)`` `format macros <https://docs.ansible.com/ansible/latest/dev_guide/developing_modules_documenting.html#linking-and-other-format-macros-within-module-documentation>`_ when referring to modules.
* [ ] Modules and plugins from ansible-core use ``ansible.builtin.`` as an FQCN prefix when mentioned.
* [ ] When a new option, module, plugin, or return value is added, the corresponding documentation or return sections use ``version_added:`` containing the *collection* version which they will be first released in.

  * This usually is the next minor release, sometimes the next major release (example: if 2.7.5 is the current release, the next minor release will be 2.8.0, and the next major release will be 3.0.0).
* [ ] FQCNs are used for ``extends_documentation_fragment:``, unless the author is referring to doc_fragments from ansible-core.

Tests (if applicable and technically possible to implement)
===========================================================

* [ ] The pull request has `integration tests <https://docs.ansible.com/ansible/devel/dev_guide/testing_integration.html>`_ and / or `unit tests <https://docs.ansible.com/ansible/devel/dev_guide/testing_units.html>`_.
* [ ] All changes are covered (for example, a bug case or a new option separately and in sensible combinations with other options).
* [ ] Integration tests cover ``check_mode`` (if it is supported).
* [ ] Integration tests check an actual state of the system, not only what the module reports (for example, if the module changes a file, check that the file was actually changed by using the ``ansible.builtin.stat`` module).
* [ ] Integration tests check return values (if applicable).

Merge commits and breaking changes
==================================

* [ ] The pull request does not contain merge commits (see GitHub warnings at the bottom of the pull request) - in this case, ask the author to rebase the pull request branch.
* [ ] If the pull request contains breaking changes, ask the author and the collection maintainers if it is really needed and there is no way not to introduce them. If breaking changes are in there, they must only appear in the next major release (and **not** in a minor or patch release - the only exception are breaking changes caused by security fixes that are absolutely necessary to fix the security issue).
