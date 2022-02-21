**********************************************
Releasing collections without Release Branches
**********************************************

If you have any question when reading this manual, ask the community in the ``#ansible-community`` `Matrix/IRC channel <https://docs.ansible.com/ansible/devel/community/communication.html#real-time-chat>`_ or create an issue in the `community-docs <https://github.com/ansible/community-docs>`_ repository.

This manual assumes that publishing the collection is done via `Zuul <https://github.com/ansible/project-config>`_ and that `antsibull-changelog <https://github.com/ansible-community/antsibull-changelog>`_ is used for the changelog.

Since no release branches are used, the manual does not distinguish between releasing a major, minor, or patch version.

1. First, examine the collection if there are merged changes to release.

2. According to the changes made, choose an appropriate release version number. Keep in mind that the collections must follow the `semantic versioning <https://semver.org/>`_ rules. Refer to the `Releasing collections <releasing_collections.rst>`_ guide for details.

3. Announce your intention to release the collection in a corresponding pinned release issue/community pinboard of the collection and in the ``#ansible-community`` `Matrix/Libera.Chat IRC channel <https://docs.ansible.com/ansible/devel/community/communication.html#real-time-chat>`_.

4. If there are new modules / plugins that will be released and you have a list of modules / plugins in ``README.md``, update ``README.md`` adding them to the list so that they will appear on the collection's Galaxy page after the release.

5. Be sure you are in a default branch in your local fork (we use ``main`` in the following examples):

.. code:: bash

    git status
    git checkout main     # if needed

6. Update your local fork:

.. code:: bash

   git pull --rebase upstream main

7. Checkout a new release branch from the default branch:

.. code:: bash

   git checkout -b release_branch

8. Make sure that ``galaxy.yml`` contains the correct release version number. If not, update it!

9. Add a changelog fragment ``changelogs/fragments/X.Y.Z.yml`` with content:

.. code:: yaml

   release_summary: |-
     Write some text here that should appear as the release summary for this version.
     The format is reStructuredText (but not a list as for regular changelog fragments).
     This text will be inserted into the changelog.

For example:

.. code:: yaml

   release_summary: |-
     This is the minor release of the ``community.mysql`` collection.
     This changelog contains all changes to the modules and plugins in this collection
     that have been made after the previous release.


10. If the content was recently moved from another collection, be sure you have all related changelog fragments in the ``changelogs/fragments`` directory. If not, copy them previously.

11. Run ``antsibull-changelog release --reload-plugins`` (should previously be installed with ``pip install antsibull-changelog``).

12. Verify that the ``CHANGELOG.rst`` looks as expected.

13. Commit and push changes to the ``CHANGELOG.rst`` and ``changelogs/changelog.yaml``, and potentially deleted/archived fragments to the ``origin`` repository's ``release_branch``.

.. code:: bash

   git commit -a -m "Release VERSION commit"
   git push origin release_branch

14. Create a pull request in the collection repository. If CI tests pass, merge it.

15. Checkout the default branch and pull the changes:

.. code:: bash

   git checkout main
   git pull --rebase upstream main

16. Add an annotated tag to the release commit with the collection version. Pushing this tag to the ``upstream`` repository will make Zuul publish the collection on `Ansible Galaxy <https://galaxy.ansible.com/>`_.

.. code:: bash

   git tag -n    # see current tags and their comments
   git tag -a NEW_VERSION -m "comment here"    # the comment can be, for example, "community.postgresql: 1.2.0"
   git push upstream NEW_VERSION

17. Wait until the new version is published on the collection's `Ansible Galaxy <https://galaxy.ansible.com/>`_ page (it will appear in a list of tarballs available to download).

18. Update the version in the ``galaxy.yml`` file to the next **expected** version. Add, commit, and push to the ``upstream``'s default branch.

19. Add a GitHub release for the new tag. Title should be the version and content ``See https://github.com/ansible-collections/community.xxx/blob/main/CHANGELOG.rst for all changes``.

20. Announce the release through the `Bullhorn Newsletter issue <https://github.com/ansible/community/wiki/News#the-bullhorn>`_.

21. Announce the release in the pinned release issue/community pinboard of the collection mentioned in step 3 and in the ``#ansible-community`` `Matrix/IRC channel <https://docs.ansible.com/ansible/devel/community/communication.html#real-time-chat>`_.
