.. _ee_overview:

***************************************
Ansible Execution Environments Overview
***************************************

.. contents::
   :local:

Terminology
===========

(TDB)

#Containerization-related applicable things (very briefly, minimum required)

#Ansible control node

#ansible-core

#ansible-collections

Rationale
=========

Software applications typically have dependencies.
It can be software libraries, configuration files or other services, to name a few, and Ansible,
generally being an exceptional automation tool, is not an exception in terms of the mentioned.

Traditionally, application dependencies are installed by administrator on top of
an operating system using packaging systems like RPM or Python-pip.

The major drawback of such approach is that an application might require versions
of dependencies different from those provided by default.

In case of Ansible, a typical installation consists of ansible-core and a set of Ansible collections.

At present, there are more than a hundred collections included in the Ansible package and
hundreds more are available on Ansible Galaxy and Automation Hub for manual installation.
Many of them have dependencies.

The Ansible collections can depend on the following pieces of software and their versions:

* ansible-core 
* Python
* Python packages
* system packages
* other Ansible collections

The dependencies have to be installed and sometimes can conflict with each other.

Moreover, typically an administrator doesn't really need the whole Ansible package
with those hundred collections.
In most cases, and it's considered a good practice, we need to install only ``ansible-core``
plus a set of collections for specific tasks if needed, no more.

For example, if you are a database administrator having only PostgreSQL RDBMS instances in your infrastructure,
you are probably interested in only ``ansible-core``, the ``community.postgresql`` Ansible collection
and a database driver (if you want to connect to servers from the control node) because
it's all what your actually need, nothing more.

Meanwhile, your colleagues responsible for other services and using the same Ansible control node or
tools like Ansible AWX/Controller can be interested in other collections
which can bring their own dependencies into play.
Moreover, if you want, say, to preserve, redeploy or share your Ansible controller runtime environment,
you might not be interested in having someone else's content there you don't need.

One way to **partly** resolve dependency and deploy issues is
to use Python virtual environments on Ansible controle node.
However, applied to Ansible, it has drawbacks and natural limitations.

That's why Ansible automation execution environments were introduced
to resolve all the mentioned issues and provide all benefits you can get from using containerization.

Section 2
=========

As described in the <SECTION ABOVE LINK HERE>, Python virtual environments have need replaced with Ansible execution environments.

Ansible, as a software application, can run in a container, thus, it can benefit from containerization the same as most other applications (see the <SECTION ABOVE LINK HERE> for Ansible-specific details).

The Ansible automation execution environment (hereinafter, execution environment or EE) is a container image serving as Ansible control node.

The EE image contains:

* ansible-core
* one of more Ansible collections
* Python
* set of dependencies required to run the collections

(To go on)


Section 2
=========

TBD

Section N
=========

TBD
