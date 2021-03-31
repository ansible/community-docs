
.. _releasing_collections:

*********************
Releasing collections
*********************

The collections under the `ansible-collections organization <https://github.com/ansible-collections>`_ follow the `semantic versioning <https://semver.org/>`_ when releasing.

The collections have:
- publicly available policy of releasing, versioning and deprecation (for example, written in its README or in a dedicated pinned issue)
- a pinned issue when its release managers inform the community about planned / completed releases (can be combined with the release policy issue mentioned above)
- changelog, preferably with ``changelogs/changelog.yaml``
- releases of the collection tagged in the collection's repository
- CI pipelines up and running (can be implemented by using GitHub Actions, Azure Pipelines, ZUUL)
- all CI tests running against a commit that releases the collection; if they do not pass, the collection will NOT be released


# Put things that are common for all the collections here (small and big, with stable branches and w/o, etc.)


# References to (when the docs are added):

# 1. releasing without branches

# 2. releasing with stable branches

# 3. ...
