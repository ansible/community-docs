*****************************
Quick-start development guide
*****************************

This guide describes all steps needed to test another author's pull request (hereinafter ``PR``).

.. contents:: Topics

Prepare your environment
========================

We assume that you use Linux as a work environment (you can use a virtual machine as well) and have ``git`` installed.

1. If possible, make sure that you have installed and started ``docker``. While you can also run tests without docker, this makes it a lot easier since you do not have to install the precise requirements, and tests are running properly isolated and in the exact same environments as in CI. You often can also use ``podman`` with the ``docker`` executable shim, so if you have that you probably do not need to install ``docker``.

2. `Install <https://docs.ansible.com/ansible/devel/installation_guide/intro_installation.html>`_ Ansible or ansible-core.

3. Create the following directories in your home directory:

.. code:: bash

  mkdir -p ~/ansible_collections/NAMESPACE/COLLECTION_NAME

For example, if the collection is ``community.general``, it will be:

.. code:: bash

  mkdir -p ~/ansible_collections/community/general

If the collection is ``ansible.posix``, it will be:

.. code:: bash

  mkdir -p ~/ansible_collections/ansible/posix

4. Fork the collection repository through the GitHub web interface.

5. Clone the forked repository from the author profile to the created path:

.. code:: bash

  git clone https://github.com/AUTHOR_ACC/COLLECTION_REPO.git ~/ansible_collections/NAMESPACE/COLLECTION_NAME

6. Go to the cloned repository.

.. code:: bash

  cd ~/ansible_collections/NAMESPACE/COLLECTION_NAME

7. Checkout to the PR branch (it can be retrieved from the PR's page):

.. code:: bash

  git checkout pr_branch

Test the Pull Request
=====================

8. Include `~/ansible-collections` in COLLECTIONS_PATHS.

Refer to the `Ansible documentation <https://docs.ansible.com/ansible/devel/reference_appendices/config.html#collections-paths>`_ for details.

9. Run your playbook again this time using the changed PR.

10. Run sanity tests:

.. code:: bash

  ansible-test sanity path/to/changed_file.py --docker -v

If they failed, look at the output carefully - it is usually very informative and helps to identify a problem line quickly.
Sanity failings usually relate to wrong code and documentation formatting.

11. Run integration tests:

.. code:: bash

  ansible-test integration name_of_test_subdirectory --docker -v

For example, if the tests files you changed are stored in ``tests/integration/targets/test_mysql_user/``, the command will be:

.. code:: bash

  ansible-test integration test_mysql_user --docker -v

You can use the ``-vv`` or ``-vvv`` argument, if you need more detailed output.

Give Feedback
=============

12. You can now give feedback on Pull Request or the linked issue(s).
