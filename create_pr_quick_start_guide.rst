*****************************
Quick-start development guide
*****************************

This guide describes all steps needed to create your first patch and submit a pull request.

We assume that you use Linux as a work environment (you can use a virtual machine as well) and have ``git`` installed.

1. If possible, make sure that you have installed and started ``docker``. While you can also run tests without docker, this makes it a lot easier since you do not have to install the precise requirements, and tests are running properly isolated and in the exact same environments as in CI. You often can also use ``podman`` with the ``docker`` executable shim, so if you have that you probably do not need to install ``docker``.

2. `Install <https://docs.ansible.com/ansible/devel/installation_guide/intro_installation.html>`_ Ansible or ansible-core.

3. Create the following directories in your home directory:

.. code:: bash

  mkdir -p ~/ansible_collections/NAMESPACE/COLLECTION_NAME

For example, if the collection is ``community.mysql``, it will be:

.. code:: bash

  mkdir -p ~/ansible_collections/community/mysql

If the collection is ``ansible.posix``, it will be:

.. code:: bash

  mkdir -p ~/ansible_collections/ansible/posix

4. Fork the collection repository through the GitHub web interface.

5. Clone the forked repository from your profile to the created path:

.. code:: bash

  git clone https://github.com/YOURACC/COLLECTION_REPO.git ~/ansible_collections/NAMESPACE/COLLECTION_NAME

If you prefer to use the SSH protocol:

.. code:: bash

  git clone git@github.com:YOURACC/COLLECTION_REPO.git ~/ansible_collections/NAMESPACE/COLLECTION_NAME

6. Go to your new cloned repository.

.. code:: bash

  cd ~/ansible_collections/NAMESPACE/COLLECTION_NAME

7. Be sure you are in the default branch (it is usually ``main``):

.. code:: bash

  git status

8. Show remotes. There should be the ``origin`` repository only:

.. code:: bash

  git remote -v

9. Add the ``upstream`` repository:

.. code:: bash

  git remote add upstream https://github.com/ansible-collections/COLLECTION_REPO.git

This is the repository where you forked from.

10. Update your local default branch. Assuming that it is ``main``:

.. code:: bash

  git fetch upstream
  git rebase upstream/main

11. Create a branch for your changes:

.. code:: bash

  git checkout -b name_of_my_branch

12. We recommend you start with writing integration tests if applicable.

Note: If there are any difficulties with writing / running the tests or you are not sure if the case can be covered, feel free to skip this step.
If needed, other contributors can help you with it later.

Note: Some collections do not have integration tests.

All integration tests are stored in ``tests/integration/targets`` subdirectories.
Go to the subdirectory containing the name of the module you are going to change.
For example, if you are fixing the ``mysql_user`` module in the ``community.mysql`` collection,
its tests are in ``tests/integration/targets/test_mysql_user/tasks``.

The ``main.yml`` file holds test tasks and includes other test files.
Look for a suitable test file to integrate your tests or create and include a dedicated test file.
You can use one of the existing test files as a draft.

When fixing a bug, write a task which reproduces the bug from the issue.

Put the reported case in the tests, then run integration tests with the following command:

.. code:: bash

  ansible-test integration name_of_test_subdirectory --docker -v

For example, if the tests files you changed are stored in ``tests/integration/targets/test_mysql_user/``, the command will be:

.. code:: bash

  ansible-test integration test_mysql_user --docker -v

You can use the ``-vv`` or ``-vvv`` argument, if you need more detailed output.

In the examples above, the default test image will be automatically downloaded and used to create and run a test container.
Use the default test image for platform independent integration tests such as those for cloud modules.

If you need to run the tests against a specific distribution, see the `list of supported container images <https://docs.ansible.com/ansible/latest/dev_guide/testing_integration.html#container-images>`_. In this case, the command can look like:

.. code:: bash

  ansible-test integration name_of_test_subdirectory --docker centos8 -v

Note: If you are not sure whether you should use the default image for testing or a specific one, skip the entire step - the community will help you later.
You can also try to use the collection repository's CI to figure out which containers are used.

If the tests ran successfully, there are usually two possible outcomes:
a) If the bug has not appeared and the tests have passed successfully, ask the reporter to provide more details. The bug can be not a bug actually or can relate to a particular software version used or specifics of local environment configuration.

b) The bug has appeared and the tests has failed as expected showing the reported symptoms.

13. Fix the bug.

14. Run ``flake8`` against a changed file:

.. code:: bash

  flake8 path/to/changed_file.py

It is worth installing (``pip install flake8``, or install the corresponding package on your operating system) and running ``flake8`` against the changed file(s) first.
It shows unused imports, which is not shown by sanity tests (see the next step), as well as other common issues.
Optionally, you can use the ``--max-line-length=160`` command-line argument.

15. Run sanity tests:

.. code:: bash

  ansible-test sanity path/to/changed_file.py --docker -v

If they failed, look at the output carefully - it is usually very informative and helps to identify a problem line quickly.
Sanity failings usually relate to wrong code and documentation formatting.

16. Run integration tests:

.. code:: bash

  ansible-test integration name_of_test_subdirectory --docker -v

For example, if the tests files you changed are stored in ``tests/integration/targets/test_mysql_user/``, the command will be:

.. code:: bash

  ansible-test integration test_mysql_user --docker -v

You can use the ``-vv`` or ``-vvv`` argument, if you need more detailed output.

If you need to run the tests against a specific distribution, see step 12.

There are two possible outcomes:
a) They have failed. Look at the output of the command.
Fix the problem place in the code and run again.
Repeat the cycle until the tests pass.

b) They have passed. Remember they failed originally? Our congratulations! You have fixed the bug.

17. Commit your changes with an informative but short commit message:

.. code:: bash

  git add /path/to/changed/file
  git commit -m "module_name_you_fixed: fix crash when ..."

18. Push the branch to the ``origin`` (your fork):

.. code:: bash

  git push origin name_of_my_branch

19. Go to the ``upstream`` (http://github.com/ansible-collections/COLLECTION_REPO).

20. Go to ``Pull requests`` tab and create a pull request.

GitHub is tracking your fork, so it should see the new branch in it and automatically offer
to create a pull request. Sometimes GitHub does not do it and you should click the ``New pull request`` button yourself.
Then choose ``compare across forks`` under the ``Compare changes`` title.
Choose your repository and the new branch you pushed in the right drop-down list. Confirm.

Fill out the pull request template with all information you want to mention.

Put ``Fixes + link to the issue`` in the pull request's description.

Put ``[WIP] + short description`` in the pull request's title. It's often a good idea to mention the name of the module/plugin you are modifying at the beginning of the description.

Click ``Create pull request``.

21. Add a `changelog fragment <https://docs.ansible.com/ansible/devel/community/development_process.html#changelogs>`_ to the ``changelog/fragments`` directory. It will be published in release notes, so users will know about the fix.

Commit and push it:

.. code:: bash

  git add changelog/fragments/myfragment.yml
  git commit -m "Add changelog fragment"
  git push origin name_of_my_branch

22. The CI tests will run automatically on Red Hat infrastructure after every commit.

You will see the CI status in the bottom of your pull request.
If they are green and you think that you do not want to add more commits before someone should take a closer look at it, remove ``[WIP]`` from the title. Mention the issue reporter in a comment and let contributors know that the pull request is "Ready for review".

23. Wait for reviews. You can also ask for review on IRC in the ``#ansible-community`` channel.

24. If the pull request looks good to the community, committers will merge it.

For details, refer to the `Ansible developer guide <https://docs.ansible.com/ansible/latest/dev_guide/index.html>`_.
