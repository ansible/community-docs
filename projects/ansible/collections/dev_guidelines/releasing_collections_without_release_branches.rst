**********************************************
Releasing collections without Release Branches
**********************************************

If you have any question when reading this manual, ask the community in the ``#ansible-community`` IRC channel or create an issue in the `community-docs <https://github.com/ansible/community-docs>`_ repository.

This manual assumes that publishing the collection is done via `Zuul <https://github.com/ansible/project-config>`_ and that `antsibull-changelog <https://github.com/ansible-community/antsibull-changelog>`_ is used for the changelog.

Since no release branches are used, the manual does not distinguish between releasing a major, minor, or patch version.

1. First, examine the collection if there are merged changes to release.

2. According to the changes made, choose an appropriate release version number. Keep in mind that the collections must follow the `semantic versioning <https://semver.org/>`_ rules. Refer to the `Releasing without release branches <releasing_collections_without_release_branches.rst>`_ for details.

3. Announce your intention to release the collection in a corresponding pinned release issue / community pinboard of the collection and in the ``#ansible-community`` IRC channel.

4. Be sure you are in a default branch in your local fork:

.. code:: bash

    git status
    git checkout DEFAULT_BRANCH     # if needed

5. Update your local fork:

.. code:: bash

   git pull --rebase upstream DEFAULT_BRANCH

6. Checkout a new release branch from the default branch:

.. code:: bash

   git checkout -b release_branch

7. Make sure that ``galaxy.yml`` contains the correct release version number. If not, update it!

8. Add a changelog fragment ``changelogs/fragments/X.Y.Z.yml`` with content:

.. code:: yaml

   release_summary: |-
     Write some text here that should appear as the release summary for this version.
     The format is reStructuredText (but not a list as for regular changelog fragments).
     This text will be verbatimly inserted into the changelog.

For example:

.. code:: yaml

   release_summary: |-
     This is the minor release of the ``community.mysql`` collection.
     This changelog contains all changes to the modules and plugins in this collection
     that have been made after the release of ``community.mysql`` 1.2.0.


9. If the content was recently moved from another collection, be sure you have all related changelog fragments in the ``changelogs/fragments`` directory. If not, copy them previously.

10. Run ``antsibull-changelog release`` (should previously be installed with ``pip install antsibull-changelog``).

11. Verify that the ``CHANGELOG.rst`` looks as expected.

12. Commit and push changes to the ``CHANGELOG.rst`` and ``changelogs/changelog.yaml``, and potentially deleted/archived fragments to the ``origin`` repository's ``release_branch``.

.. code:: bash

   git commit -a -m "Release VERSION commit"
   git push origin release_branch

13. Create a pull request in the collection repository. If CI tests pass, merge it.

14. Checkout the default branch and pull the changes:

.. code:: bash

   git checkout DEFAULT_BRANCH
   git pull --rebase upstream DEFAULT_BRANCH

15. Add an annotated tag to the release commit with the collection version. Pushing this tag to the ``upstream`` repository will make Zuul publish the collection on `Ansible Galaxy <https://galaxy.ansible.com/>`_.

.. code:: bash

   git tag -n    # see current tags and their comments
   git tag -a NEW_VERSION -m "comment here"    # the comment can be, for example, "community.postgresql: 1.2.0"
   git push upstream NEW_VERSION

16. Update the version in the ``galaxy.yml`` file to the next **expected** version. Add, commit, and push to the ``upstream``'s default branch.

17. Wait until the new version is published on the collection's `Ansible Galaxy <https://galaxy.ansible.com/>`_ page (it will appear in a list of tarballs available to download).

18. Put a note about the release in the `Bullhorn Newsletter issue <https://github.com/ansible/community/issues/546>`_ to have it published later.

19. Announce that the release has been made in the pinned release issue / community pinboard of the collection mentioned in step 3 and in the ``#ansible-community`` IRC channel.
