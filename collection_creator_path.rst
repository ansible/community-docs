*******************************
Ansible Collection Creator Path
*******************************

The guide's purpose and overview
================================

.. note::

  If you are totally unfamiliar with the collection technology,
  first take a look at the `Using Ansible collections guide <https://docs.ansible.com/ansible/latest/collections_guide/index.html>`_.

Ansible collections are a distribution format for Ansible content that
can include playbooks, roles, modules, and plugins.
You can install collections made by others or share yours with
the community through a distribution server such as Ansible Galaxy.

Creating and sharing collections is a great way of contribution to the Ansible project.

The Ansible community package consists of ``ansible-core``, which, among other core components,
includes the ``ansible.builtin`` collection maintained by the Core team,
and a set of collections maintained by the community.

The purpose of this guide is to give your as a (potential) content creator
a consistent overview of the Ansible collection creator journey from
an idea for the first module/role to having your collection included in
the Ansible community package.

Each of the following guide sections will reflect one step in the path.

.. _examine_existing_content:

Examine currently available solutions
=====================================

If you have an idea for a new role or module/plugin,
there is no need to reinvent the wheel if there is already a sufficient solution
that solve your automation issue.

Therefore, first examine the currently available content on the Internet including:

* `Ansible Galaxy <https://galaxy.ansible.com/>`_
* `Ansible builtin modules and plugins <https://docs.ansible.com/ansible/latest/collections/ansible/builtin/index.html>`_
* `Ansible package collection index <https://docs.ansible.com/ansible/latest/collections/index.html>`_

In case the solutions you found are not fully sufficient or have flaws,
consider improving them rather than creating your own.

If you already have your content written and used in your workflows,
you could think of integrating it to the existing solutions.

However, if they have significant flaws, licensing or major design issues,
or their corresponding projects are unmaintained, you are encouraged
to create and/or share your own one.

.. _create_content:

Create your content
===================

You :ref:`tried <examine_existing_content>` but have not found any sufficient solution for your automation issue.

Use one of the following guides:

* `Roles guide <https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_reuse_roles.html#>`_: if you want to create a role.
* `Developer guide <https://docs.ansible.com/ansible/latest/dev_guide/index.html>`_: if you want to create a new Ansible module or plugin.

Put your content in a collection
================================

You :ref:`created <create_content>` new content.

Now it is time to create a collection to share your shiny work with the community.

Use the `Developing collections guide <https://docs.ansible.com/ansible/latest/dev_guide/developing_collections.html>`_ to learn how.

We recommend you to use the `collection_template repository <https://github.com/ansible-collections/collection_template>`_ as a basis.

Write good user collection documentation
========================================

Your collection's ``README.md`` file contains a quick-start installation and usage guides.
You can use the `community.general collection README file <https://github.com/ansible-collections/community.general/blob/main/README.md>`_ as an example.

If your collection contains modules or plugins, make sure their documentation is comprehensive.
Use the `Module format and documentation guide <https://docs.ansible.com/ansible/latest/dev_guide/developing_modules_documenting.html>`_ and `Ansible documentation style guide <https://docs.ansible.com/ansible/latest/dev_guide/style_guide/index.html>`_ to learn more.

Publish your collection on GitHub
=================================

Publish your collection on a platform for software development and version control such as `GitHub <https://github.com/>`_.

It can be your personal repository or your organization one.
You can also `request <https://github.com/ansible-collections/overview/issues>`_ a repository under the `ansible-collections <https://github.com/ansible-collections/>`_ organization.

Make sure your collection contains exhaustive license information.
Ansible is an open source project, so we encourage you to license it under one of open source licenses.
If you plan to submit your collection for inclusion in the Ansible community package, your collection must satisfy the `licensing requirements <https://docs.ansible.com/ansible/devel/community/collection_contributors/collection_requirements.html#collection-licensing-requirements>`_.

If you have used the `collection_template repository <https://github.com/ansible-collections/collection_template>`_ we recommended earlier as a skeleton for your collection, it already contains the ``GNU GPL v3`` license.

Understand and implement testing and CI
=======================================

Add tests
---------

TBD

Implement CI
------------

GHA + AZP explained

Write good contributor & maintainer documentation
=================================================

TBD

Publish your collection on Galaxy
=================================

TBD

Follow the Collection requirements
==================================

Link to the requirements and a very brief explanation

Submit for inclusion
====================

Links

Maintain
========

Links to the Maintainer guidelines

Communication
=============

Maybe as a separate paragraph
