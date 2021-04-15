*******************************************
Releasing collections with Release Branches
*******************************************

Keep in mind that the collections must follow the `semantic versioning <https://semver.org/>`_ rules. Refer to the `Releasing collections <releasing_collections.rst>`_ guide for details.

If you have any question when reading this manual, ask the community in the ``#ansible-community`` IRC channel or create an issue in the `community-docs <https://github.com/ansible/community-docs>`_ repository.

This manual assumes that publishing the collection is done via `Zuul <https://github.com/ansible/project-config>`_ and that `antsibull-changelog <https://github.com/ansible-community/antsibull-changelog>`_ is used for the changelog.

.. contents:: Topics

Planning
========

1. Announce your intention to release the collection in a corresponding pinned release issue / community pinboard of the collection and in the ``#ansible-community`` IRC channel (and in other dedicated channels if exist) in advance.

2. Be sure that all the other repository maintainers are informed about the time of the following release.

Releasing major versions
========================

The new version is assumed to be ``X.0.0``.

1. If you are going to release the ``community.general`` and ``community.network`` collections, create new labels ``backport-X`` and ``needs_backport_to_stable_X`` in the corresponding repositories. Copy the styles and descriptions from the corresponding existing labels.

2. Be sure you are in a default branch in your local fork (we use ``main`` in the following examples):

.. code:: bash

    git status
    git checkout main     # if needed

3. Update your local fork:

.. code:: bash

   git pull --rebase upstream main

4. Create a branch ``stable-X`` (replace ``X`` with a proper number) and push it to the **upstream** repository (NOT to the ``origin``):

.. code:: bash

    git branch stable-X main
    git push upstream stable-X

5. Create and checkout to another branch from the ``main`` branch:

.. code:: bash

    git checkout -b update_repo

6. Update the version in ``galaxy.yml`` in the branch to the next **expected** version (for example, ``X.1.0``).


7. Replace ``changelogs/changelog.yml`` with:

.. code:: yaml

    ancestor: X.0.0
    releases: {}

8. Remove all changelog fragments from ``changelogs/fragments/``. This ensures that every major release has a changelog describing changes since the last major release.

9. Add and commit all the changes made. Push the branch to the ``origin`` repository.

10. Create a pull request in the collection repository. If CI tests pass, merge it.

Since that, the ``main`` branch is expecting changes for the next minor/major versions

11. Switch to the ``stable-X`` branch.

12. In the ``stable-X`` branch, make sure that ``galaxy.yml`` contains the correct version number ``X.0.0``. If not, update it!

13. In the ``stable-X`` branch, add a changelog fragment ``changelogs/fragments/X.0.0.yml`` with content:

.. code:: yaml

  release_summary: |-
    Write some text here that should appear as the release summary for this version.
    The format is reStructuredText (but not a list as for regular changelog fragments).
    This text will be inserted into the changelog.

For example:

.. code:: yaml

    release_summary: This is release 2.0.0 of ``community.foo``, released on YYYY-MM-DD.

Add to git and commit.

14. In the stable-X branch, run:

.. code:: bash

    antsibull-changelog release --cummulative-release

15. In the ``stable-X`` branch, verify that the ``CHANGELOG.rst`` looks as expected.

16. In the ``stable-X`` branch, update ``README.md`` so that the changelog link points to ``/tree/stable-X/`` and no longer to ``/tree/main/``, and add ``?branchName=stable-X`` to the AZP CI badge (https://dev.azure.com/ansible/community.xxx/_apis/build/status/CI?branchName=stable-X).

17. In the ``stable-X`` branch, add, commit, and push changes to ``README.md``, ``CHANGELOG.rst`` and ``changelogs/changelog.yaml``, and potentially deleted/archived fragments to the **upstream** repository (NOT to the ``origin``).

18. In the ``stable-X`` branch, add an annotated tag to the last commit with the collection version ``X.0.0``. Pushing this tag to the ``upstream`` repository will make Zuul publish the collection on `Ansible Galaxy <https://galaxy.ansible.com/>`_.

.. code:: bash

   git tag -n    # see current tags and their comments
   git tag -a NEW_VERSION -m "comment here"    # the comment can be, for example, "community.foo: 2.0.0"
   git push upstream NEW_VERSION

19. Wait until the new version is published on the collection's `Ansible Galaxy <https://galaxy.ansible.com/>`_ page (it will appear in a list of tarballs available to download).

20. Add a GitHub release for the new tag. Title should be the version and content ``See https://github.com/ansible-collections/community.xxx/blob/stable-X/CHANGELOG.rst for all changes``.

21. Put a note about the release in the `Bullhorn Newsletter issue <https://github.com/ansible/community/issues/546>`_ to have it published later.

22. Announce that the release has been made in the pinned release issue / community pinboard of the collection and in the ``#ansible-community`` IRC channel.

23. In the stable-X branch, update the version in galaxy.yml to the next **expected** version, for example, ``X.1.0``. Add, commit and push to the **upstream** repository.


Releasing minor versions
========================

The new version is assumed to be ``X.Y.0``. All changes that should go into it are expected to be previously backported from the default branch (we use ``main`` in the following examples) to the ``stable-X`` branch.

1. In the ``stable-X`` branch, make sure that ``galaxy.yml`` contains the correct version number ``X.Y.0``. If not, update it!

2. In the ``stable-X`` branch, add a changelog fragment ``changelogs/fragments/X.Y.0.yml`` with content:

.. code:: yaml

  release_summary: |-
    Write some text here that should appear as the release summary for this version.
    The format is reStructuredText (but not a list as for regular changelog fragments).
    This text will be inserted into the changelog.

3. In the ``stable-X`` branch, run:

.. code:: bash

   antsibull-changelog release

4. In the ``stable-X`` branch, verify that ``CHANGELOG.rst`` looks as expected.

5. In the ``stable-X`` branch, add, commit, and push changes to ``CHANGELOG.rst`` and ``changelogs/changelog.yaml``, and potentially deleted/archived fragments to the **upstream** repository (NOT to the origin).

6. In the ``stable-X`` branch, add an annotated tag to the last commit with the collection version ``X.Y.0``. Pushing this tag to the ``upstream`` repository will make Zuul publish the collection on `Ansible Galaxy <https://galaxy.ansible.com/>`_.

.. code:: bash

   git tag -n    # see current tags and their comments
   git tag -a NEW_VERSION -m "comment here"    # the comment can be, for example, "community.foo: 2.1.0"
   git push upstream NEW_VERSION

7. Wait until the new version is published on the collection's `Ansible Galaxy <https://galaxy.ansible.com/>`_ page (it will appear in a list of tarballs available to download).

8. Add a GitHub release for the new tag. Title should be the version and content ``See https://github.com/ansible-collections/community.xxx/blob/stable-X/CHANGELOG.rst for all changes``.

9. Put a note about the release in the `Bullhorn Newsletter issue <https://github.com/ansible/community/issues/546>`_ to have it published later.

10. Announce that the release has been made in the pinned release issue / community pinboard of the collection and in the ``#ansible-community`` IRC channel. Additionally, you can announce it using GitHub's Releases system.

11. In the stable-X branch, update the version in galaxy.yml to the next **expected** version, for example, if you has released ``X.1.0``, the next expected version could be ``X.2.0``. Add, commit and push to the **upstream** repository.

12. Checkout to the ``main`` branch.

13. In the ``main`` branch:

i. If more minor versions are released before the next major version, update the version in galaxy.yml to ``X.(Y+1).0`` as well. Create a dedicated pull request and merge.

ii. If the next version will be a new major version, create a pull request where you update the version in ``galaxy.yml`` to ``(X+1).0.0``. Note that the sanity tests will most likely fail since there will be deprecations with removal scheduled for ``(X+1).0.0``, which are flagged by the tests.

  For every such deprecation, decide whether to remove them now (makes sense if complete ``modules/plugins`` are removed,
  or redirects are removed), or whether to add ignore entries to the corresponding ``tests/sanity/ignore-*.txt`` file and
  create issues (makes sense for removed features in ``modules/plugins``).
  Once CI passes, merge the pull request. Make sure that this pull request is merged not too much later after the release
  for ``verison_added`` sanity tests not to expect the wrong version for new feature pull request.

.. note::

  It makes sense to already do some removals in the days before the release. These removals must happen in the main branch and must not be backported.


Releasing patch versions
========================

The new version is assumed to be ``X.Y.Z``, and the previous patch version is assumed to be ``X.Y.z`` with ``z < Z`` (probably ``z`` is ``0``, as patch releases should be uncommon).

More minor versions are expected
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. Checkout the ``X.Y.z`` tag.

2. Update ``galaxy.yml`` so that the version is ``X.Y.Z``. Add and commit.

3. Cherry-pick all changes from ``stable-X`` that were added after ``X.Y.z`` and should go into ``X.Y.Z``.

4. Add a changelog fragment ``changelogs/fragments/X.Y.Z.yml`` with content:

.. code:: yaml

  release_summary: |-
    Write some text here that should appear as the release summary for this version.
    The format is reStructuredText (but not a list as for regular changelog fragments).
    This text will be inserted into the changelog.

Add to git and commit.

5.Run:

.. code:: bash

   antsibull-changelog release

6. Verify that ``CHANGELOG.rst`` looks as expected.

7. Add and commit changes to ``CHANGELOG.rst`` and ``changelogs/changelog.yaml``, and potentially deleted/archived fragments.

8. Add an annotated tag to the last commit with the collection version ``X.Y.Z``. Pushing this tag to the ``upstream`` repository will make Zuul publish the collection on `Ansible Galaxy <https://galaxy.ansible.com/>`_.

.. code:: bash

   git tag -n    # see current tags and their comments
   git tag -a NEW_VERSION -m "comment here"    # the comment can be, for example, "community.foo: 2.1.1"
   git push upstream NEW_VERSION

9. Wait until the new version is published on the collection's `Ansible Galaxy <https://galaxy.ansible.com/>`_ page (it will appear in a list of tarballs available to download).

10. Add a GitHub release for the new tag. Title should be the version and content ``See https://github.com/ansible-collections/community.xxx/blob/stable-X/CHANGELOG.rst for all changes``.

.. note::

  The data for this release is only contained in a tag, and not in a branch (in particular not in ``stable-X``).
  This is intended, since the next minor release ``X.(Y+1).0`` already contains the changes for ``X.Y.Z`` as well
  (since these were cherry-picked from ``stable-X``).

11. Put a note about the release in the `Bullhorn Newsletter issue <https://github.com/ansible/community/issues/546>`_ to have it published later.

12. Announce that the release has been made in the pinned release issue / community pinboard of the collection and in the ``#ansible-community`` IRC channel.

No more minor versions are expected
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

1. In the ``stable-X`` branch, make sure that ``galaxy.yml`` contains the correct version number ``X.Y.Z``. If not, update it!

2. In the ``stable-X`` branch, add a changelog fragment ``changelogs/fragments/X.Y.Z.yml`` with content:

.. code:: yaml

  release_summary: |-
    Write some text here that should appear as the release summary for this version.
    The format is reStructuredText (but not a list as for regular changelog fragments).
    This text will be inserted into the changelog.

3. In the ``stable-X`` branch, run:

.. code:: bash

   antsibull-changelog release

4. In the ``stable-X`` branch, verify that ``CHANGELOG.rst`` looks as expected.

5. In the ``stable-X`` branch, add, commit, and push changes to ``CHANGELOG.rst`` and ``changelogs/changelog.yaml``, and potentially deleted/archived fragments to the **upstream** repository (NOT to the origin).

6. In the ``stable-X`` branch, add an annotated tag to the last commit with the collection version ``X.Y.Z``. Pushing this tag to the ``upstream`` repository will make Zuul publish the collection on `Ansible Galaxy <https://galaxy.ansible.com/>`_.

.. code:: bash

   git tag -n    # see current tags and their comments
   git tag -a NEW_VERSION -m "comment here"    # the comment can be, for example, "community.foo: 2.1.1"
   git push upstream NEW_VERSION

7. Wait until the new version is published on the collection's `Ansible Galaxy <https://galaxy.ansible.com/>`_ page (it will appear in a list of tarballs available to download).

8. Add a GitHub release for the new tag. Title should be the version and content ``See https://github.com/ansible-collections/community.xxx/blob/stable-X/CHANGELOG.rst for all changes``.

9. Put a note about the release in the `Bullhorn Newsletter issue <https://github.com/ansible/community/issues/546>`_ to have it published later.

10. Announce that the release has been made in the pinned release issue / community pinboard of the collection and in the ``#ansible-community`` IRC channel.
