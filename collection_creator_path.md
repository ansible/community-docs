### Ansible Collection Creator Path

#### The guide's purpose and overview

> **_NOTE:_** If you are totally unfamiliar with the collection technology, first take a look at the [Using Ansible collections guide](https://docs.ansible.com/ansible/latest/collections_guide/index.html).

Ansible collections are a distribution format for Ansible content that can include playbooks, roles, modules, and plugins. You can install collections made by others or share yours with the community through a distribution server such as Ansible Galaxy.

Creating and sharing collections is a great way of contribution to the Ansible project.

The Ansible community package consists of `ansible-core`, which, among other core components, includes the `ansible.builtin` collection maintained by the Core team, and a set of collections maintained by the community.

The purpose of this guide is to give your as a (potential) content creator a consistent overview of the Ansible collection creator journey from an idea for the first module/role to having your collection included in the Ansible community package.

Each of the following guide sections will reflect one step in the path.

#### Examine currently available solutions

If you have an idea for a new role or module/plugin, there is no need to reinvent the wheel if there is already a sufficient solution that solve your automation issue.

Therefore, first examine the currently available content on the Internet including:

* [Ansible builtin modules and plugins](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/index.html)
* [Ansible package collection index](https://docs.ansible.com/ansible/latest/collections/index.html)
* [Ansible Galaxy](https://galaxy.ansible.com/)
* [Ansible Automation Hub](https://www.ansible.com/products/automation-hub) if you have the Ansible Automation Platform subscription

In case the solutions you found are not fully sufficient or have flaws, consider improving them rather than creating your own.

If you already have your content written and used in your workflows, you could think of integrating it to the existing solutions.

However, if they have significant flaws, licensing or major design issues, or their corresponding projects are unmaintained, you are encouraged to create and share your own solution.

#### Create your content

You [tried](#examine-currently-available-solutions) but have not found any sufficient solution for your automation issue.

Use one of the following guides:

* [Roles guide](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_reuse_roles.html): if you want to create a role.
* [Developer guide](https://docs.ansible.com/ansible/latest/dev_guide/index.html): if you want to create a new Ansible module or plugin.

#### Put your content in a collection

You [created](#create-your-content) new content.

Now it is time to create a collection to share your work with the community. Use the [Developing collections guide](https://docs.ansible.com/ansible/latest/dev_guide/developing_collections.html) to learn how.

We recommend you to use the [collection_template repository](https://github.com/ansible-collections/collection_template) as a basis for your collection.

#### Write good user collection documentation

Your collection's `README.md` file contains a quick-start installation and usage guides. You can use the [community.general collection README file](https://github.com/ansible-collections/community.general/blob/main/README.md) as an example.

If your collection contains modules or plugins, make sure their documentation is comprehensive. Use the [Module format and documentation guide](https://docs.ansible.com/ansible/latest/dev_guide/developing_modules_documenting.html) and [Ansible documentation style guide](https://docs.ansible.com/ansible/latest/dev_guide/style_guide/index.html) to learn more.

#### Publish your collection source code

Publish your collection on a platform for software development and version control such as [GitHub](https://github.com/).

It can be your personal repository or your organization's one. You can also [request](https://github.com/ansible-collections/overview/issues) a repository under the [ansible-collections](https://github.com/ansible-collections/) organization.

Make sure your collection contains exhaustive license information. Ansible is an open source project, so we encourage you to license it under one of open source licenses. If you plan to submit your collection for inclusion in the Ansible community package, your collection must satisfy the [licensing requirements](https://docs.ansible.com/ansible/devel/community/collection_contributors/collection_requirements.html#collection-licensing-requirements).

If you have used the [collection_template repository](https://github.com/ansible-collections/collection_template) we recommended earlier as a skeleton for your collection, it already contains the `GNU GPL v3` license.

#### Follow a versioning convention

When releasing new versions of your collections, take the following recommended practices into consideration:

* Follow a versioning convention. Using [SemVer](https://semver.org/) is highly recommended.
* Base your releases on [Git tags](https://docs.github.com/en/repositories/releasing-projects-on-github/about-releases).
* If your collection repository is on GitHub, use [GitHub releases](https://docs.github.com/en/repositories/releasing-projects-on-github/managing-releases-in-a-repository).

#### Understand and implement testing and CI

This section is applicable to collections containing modules and plugins.

If you have simple general solutions for role testing, please expand the section.

##### Add tests

Testing your collection ensures that your code works well and integrates with other components such as `ansible-core`.

Take a look at the following documents:

* [Testing Ansible guide](https://docs.ansible.com/ansible/latest/dev_guide/testing.html): provides general information about testing.
* [Testing collections guide](https://docs.ansible.com/ansible/latest/dev_guide/developing_collections_testing.html#testing-collections): contains collection-specific testing information.

##### Implement continuous integration

Now make sure when pull requests are created in your collection repository they are automatically tested using a CI tool such as GitHub Actions or Azure Pipelines.

The [collection_template repository](https://github.com/ansible-collections/collection_template) contains GitHub Actions [templates](https://github.com/ansible-collections/collection_template/tree/main/.github/workflows) you can adjust and use to enable the workflows in your repository.

#### Provide good contributor & maintainer documentation

See the [collection_template/README.md](https://github.com/ansible-collections/collection_template/blob/main/README.md) as an example.

#### Publish your collection on distribution servers

To distribute your collection and allow others to conveniently use it, publish your collection on one or more distribution servers. See the [Distributing collections guide](https://docs.ansible.com/ansible/latest/dev_guide/developing_collections_distributing.html) to learn how.

#### Follow the Collection requirements

Make you collection satisfy the [Ansible community package collections requirements](https://docs.ansible.com/ansible/latest/community/collection_contributors/collection_requirements.html).

#### Submit for inclusion

After making your collection satisfy the collection requirements, you can submit it for inclusion in the Ansible community package. See the [inclusion process description](https://github.com/ansible-collections/ansible-inclusion/blob/main/README.md) to learn how.

#### Maintain

Maintain your collection. See the [Ansible collection maintainer guidelines](https://docs.ansible.com/ansible/latest/community/maintainers.html) for details.

#### Communication

Engage with the community. Take a look at the [Ansible communication guide](https://docs.ansible.com/ansible/devel/community/communication.html) to see available communication options.
