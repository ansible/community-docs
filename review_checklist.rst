****************
Review Checklist
****************

When reviewing, keep in mind that we follow the `Ansible Code of Conduct <https://docs.ansible.com/ansible/latest/community/code_of_conduct.html>`_ in all our contributions and interactions within this repository.

If you are a committer, also refer to the `Ansible committer guidelines <https://docs.ansible.com/ansible/devel/community/committer_guidelines.html>`_.

General tips
============

* Try to create a culture of collaboration when reviewing.
* Welcome the author and thank them for the pull request.
* When suggesting changes, try to use questions, not statements.
* When suggesting mandatory changes, do it as politely as possible providing documentation references.
* If your suggestion is optional or a matter of personal preferences, please say it explicitly.
* When asking for adding tests or for complex code refactoring, say that the author is welcome to ask for clarifications and help if they need.
* If somebody suggests a good idea, mention it or put a thumbs up.
* After merging, thank the author and reviewers for their time and effort.

Standards and documentation
===========================

* [ ] if the pull request is not a documentation fix, it must include a `changelog fragment <https://docs.ansible.com/ansible/devel/community/development_process.html#creating-a-changelog-fragment>`_ - please check the format carefully

  * the only exception are new modules and plugins (that are not jinja2 filter and test plugins)
  * for jinja2 filter and test plugins, check out the `special syntax for changelog fragments <https://github.com/ansible-community/antsibull-changelog/blob/main/docs/changelogs.rst#adding-new-roles-playbooks-test-and-filter-plugins>`_
* [ ] if new files are added with the pull request, they follow the `licensing rules <https://github.com/ansible-collections/overview/blob/main/collection_requirements.rst#licensing>`_
* [ ] the changes follow the `Ansible documentation standards <https://docs.ansible.com/ansible/devel/dev_guide/developing_modules_documenting.html>`_ and the `Style guide <https://docs.ansible.com/ansible/devel/dev_guide/style_guide/index.html#style-guide>`_
* [ ] the changes follow the `Development conventions <https://docs.ansible.com/ansible/devel/dev_guide/developing_modules_best_practices.html>`_
* [ ] if a new plugin is added, it is one of the `allowed plugin types <https://github.com/ansible-collections/overview/blob/main/collection_requirements.rst#modules-plugins>`_
* [ ] documentation, examples, and return sections use FQCNs for the ``M(..)`` `format macros <https://docs.ansible.com/ansible/latest/dev_guide/developing_modules_documenting.html#linking-and-other-format-macros-within-module-documentation>`_ when referring to modules
* [ ] modules and plugins from ansible-core use ``ansible.builtin.`` as an FQCN prefix when mentioned
* [ ] when a new option, module, plugin, or return value is added, the corresponding documentation or return sections use ``version_added:`` containing the *collection* version which they will be first released in

  * this usually is the next minor release, sometimes the next major release (example: if 2.7.5 is the current release, the next minor release will be 2.8.0, and the next major release will be 3.0.0)
* [ ] FQCNs are used for ``extends_documentation_fragment:``, unless the author is referring to doc_fragments from ansible-core

Tests (if applicable and technically possible to implement)
===========================================================

* [ ] the pull request has `integration tests <https://docs.ansible.com/ansible/devel/dev_guide/testing_integration.html>`_
* [ ] the pull request has `unit tests <https://docs.ansible.com/ansible/devel/dev_guide/testing_units.html>`_
* [ ] all changes are covered
* [ ] integration tests also cover ``check_mode`` (if it is supported)
* [ ] integration tests check an actual state of the system, not only what the module reports (for example, if the module changes a file, check that the file was actually changed by using the ``ansible.builtin.stat`` module)

Merge commits and breaking changes
==================================

* [ ] the pull request does not contain merge commits (see GitHub warnings at the bottom of the pull request) - in this case, ask the author to rebase the pull request branch
* [ ] if the pull request contains breaking changes, ask the author and the collection maintainers if it is really needed and there is no way not to introduce them. If breaking changes are in there, they must only appear in the next major release (and **not** in a minor or patch release - the only exception are breaking changes caused by security fixes that are absolutely necessary to fix the security issue)
