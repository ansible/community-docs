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
    git push upstream stable-X

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

19. In the stable-X branch, update the version in galaxy.yml to the next **expected** version, for example, X.1.0. Add, commit and push to the **upstream** repository.

20. Wait until the new version is published on the collection's `Ansible Galaxy <https://galaxy.ansible.com/>`_ page (it will appear in a list of tarballs available to download).

21. Put a note about the release in the `Bullhorn Newsletter issue <https://github.com/ansible/community/issues/546>`_ to have it published later.

22. Announce that the release has been made in the pinned release issue / community pinboard of the collection mentioned in step 3 and in the ``#ansible-community`` IRC channel. Additionally, you can announce it using GitHub's Releases system.


Releasing minor versions
========================


Releasing patch versions
========================


More minor versions are expected
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


No more minor versions are expected
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
