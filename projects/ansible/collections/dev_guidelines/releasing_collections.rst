
.. _releasing_collections:

*********************
Releasing collections
*********************

The collections under the `ansible-collections organization <https://github.com/ansible-collections>`_ follow the `semantic versioning <https://semver.org/>`_ when releasing. For details, refer to the :ref:`versioning_and_deprecation` section.

The collections have:

* publicly available policy of releasing, versioning and deprecation (for example, written in its README or in a dedicated pinned issue).
* a pinned issue when its release managers inform the community about planned / completed releases (can be combined with the release policy issue mentioned above)
* changelog; for details, refer to the :ref:`changelogs` section.
* releases of the collection tagged in the collection's repository
* CI pipelines up and running (can be implemented by using GitHub Actions, Azure Pipelines, ZUUL)
* all CI tests running against a commit that releases the collection; if they do not pass, the collection will NOT be released

.. _versioning_and_deprecation:

Versioning and deprecation
==========================

* Collections MUST adhere to `semantic versioning <https://semver.org/>`_.
* To preserve backward compatibility for users, every Ansible minor version series (3.1.x, 3.2.x, and so on) will keep the major version of a collection constant. If ansible 3.0.0 includes ``community.general`` 2.2.0, then each 3.X.x release will include the latest ``community.general`` 2.y.z release available at build time. Ansible 3.x.x will **never** include a ``community.general`` 3.y.x release, even if it is available. Major collection version changes will be included in the next Ansible major release (4.0.0 in this case).
* Therefore, please make sure that the current major release of your collection included in 3.0.0 receives at least bugfixes as long new 3.X.X releases are produced.
* Since new minor releases are included, you can include new features, modules and plugins. You must make sure that you do not break backwards compatibility! (See `semantic versioning <https://semver.org/>`_.) This means in particular:

  * You can fix bugs in **patch** releases but not add new features or deprecate things.
  * You can add new features and deprecate things in **minor** releases, but not remove things or change behavior of existing features.
  * You can only remove things or make breaking changes in **major** releases.
* Make sure that if a deprecation is added in a collection version that is included in 3.x.x, the removal itself will only happen in a collection version included in 5.0.0 or later.
* Make sure that the policy of releasing, versioning and deprecation is announced to contributors and users in some way. For an example of how to do this, see `the announcement in community.general <https://github.com/ansible-collections/community.general/issues/582>`_. You could also do this in the README.


.. _changelogs:

Changelogs
----------

Collections are required to include a changelog. To give a consistent feel for changelogs across collections and ensure changelogs exist for collections included in the ``ansible`` package we suggest using `antsibull-changelog <https://github.com/ansible-community/antsibull-changelog>`_ to maintain and generate this.

Before releasing, check:

* all merged pull requests since the last release (except ones related to documentation and new modules/plugins), have `changelog fragments <https://docs.ansible.com/ansible/devel/community/development_process.html#creating-a-changelog-fragment>`_
* all the fragments follow the `changelog entry format <https://docs.ansible.com/ansible/devel/community/development_process.html#changelog-fragment-entry-format>`_


# References to (when the docs are added):

# 1. releasing without branches

# 2. releasing with stable branches

# 3. ...
