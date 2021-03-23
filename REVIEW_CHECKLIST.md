# Review Checklist

When reviewing, keep in mind that we follow [Ansible Code of Conduct](https://docs.ansible.com/ansible/latest/community/code_of_conduct.html) in all our contributions and interactions within this repository.

**General tips**
- Try to create a culture of collaboration when reviewing
- Welcome the author and thank them for the pull request
- When suggesting changes, try to use questions, not statements
- When suggesting mandatory changes, do it as politely as possible providing documentation references
- If your suggestion is optional or a matter of personal preferences, please say it explicitly
- When asking for adding tests or for complex code refactoring, say that the author is welcome to ask for clarifications and help if they need
- If somebody suggests a good idea, say about it or put a thumbs up
- After merging, thank the author and reviewers for their time and effort

**Standards and documentation**
- [ ] if the pull request is not a documentation fix, it must include a [changelog fragment](https://docs.ansible.com/ansible/devel/community/development_process.html#creating-a-changelog-fragment) - please check the format carefully
- [ ] if new files are added with the pull request, they follow the [licensing rules](https://github.com/ansible-collections/overview/blob/main/collection_requirements.rst#licensing)
- [ ] the changes follow the [Ansible documentation standards](https://docs.ansible.com/ansible/devel/dev_guide/developing_modules_documenting.html) and the [style guide](https://docs.ansible.com/ansible/devel/dev_guide/style_guide/index.html#style-guide)
- [ ] the changes follow the [development conventions](https://docs.ansible.com/ansible/devel/dev_guide/developing_modules_best_practices.html)
- [ ] if a new plugin is added, it is one of the [allowed plugin types](https://github.com/ansible-collections/overview/blob/main/collection_requirements.rst#modules-plugins)
- [ ] documentation, examples, and return sections use FQCNs for `M(..)` when referring to modules
- [ ] modules and plugins from ansible-core use `ansible.builtin.` as a FQCN prefix when mentioned
- [ ] when a new option, module, plugin, or return value is added, the corresponding documentation or return sections use `version_added:` containing the *collection* version for which they were added
- [ ] FQCNs is used for `extends_documentation_fragment:`, unless the author is referring to doc_fragments from ansible-core

**Tests (if applicable and technically possible to implement):** 
- [ ] the pull request has integration tests 
- [ ] the pull request has unit tests
- [ ] all changes are covered
- [ ] integration tests also cover `check_mode` (if it is supported)
- [ ] integration tests check an actual state of the system, not only what the module reports (for example, if the module change a file, check that the file was actually changed by using the `ansible.builtin.stat` module)

**Other**
- [ ] the pull request does not contain merge commits (see GitHub warnings at the bottom of the pull request) - in this case, ask the author to rebase the pull request branch
- [ ] if the pull request contains breaking changes, ask the author and the collection maintainers if it is really needed and there is no way not to introduce them
