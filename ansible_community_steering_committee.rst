************************************
Ansible Community Steering Committee
************************************

Mission
=======

The Steering Committee’s mission (hereinafter the Committee) is to provide continuity, guidance, and
suggestions to the Ansible community, to ensure delivery and high quality of the Ansible package.

The Committee helps decide the technical direction of the Ansible project and is responsible for approval of new
proposals and policies in the community, package, and community collections world, new community collection-inclusion requests,
and other technical aspects regarding inclusion and packaging.

The Committee should reflect the scope and breadth of the Ansible Community.

The Committee Responsibilities
==============================

The committee

* Designs policies and procedures for the community collections world; vote on approval changes to established policies and procedures.
* Reviews community collections for compliance with the policies. 
* Helps create and define roadmaps for our deliverables such as the ``ansible`` package, major community collections, and documentation.
* Reviews community collections submitted for inclusion in the Ansible package and decides whether to include them or not.
* Review other proposals of importance that need the Committee's attention and provide feedback.

Members
=======

+------------------+---------------+-------------+
| Name             | GitHub        | Start year  |
+==================+===============+=============+
| Alicia Cozine    | acozine       | 2021        |
+------------------+---------------+-------------+
| Andrew Klychkov  | Andersson007  | 2021        |
+------------------+---------------+-------------+
| Brad Thornton    | cidrblock     | 2021        |
+------------------+---------------+-------------+
| Brian Scholer    | briantist     | 2022        |
+------------------+---------------+-------------+
| Dylan Silva      | thaumos       | 2021        |
+------------------+---------------+-------------+
| Felix Fontein    | felixfontein  | 2021        |
+------------------+---------------+-------------+
| James Cassell    | jamescassell  | 2021        |
+------------------+---------------+-------------+
| Jill Rouleau     | jillr         | 2021        |
+------------------+---------------+-------------+
| John Barker      | gundalow      | 2021        |
+------------------+---------------+-------------+
| Markus Bergholz  | markuman      | 2022        |
+------------------+---------------+-------------+
| Sorin Sbarnea    | ssbarnea      | 2021        |
+------------------+---------------+-------------+

See also the `list of past Committee members and chairpersons <https://github.com/ansible/community-docs/blob/main/steering_committee_past_members.rst>`_.

Committee members are selected based on their active contribution to the Ansible Project and its Community.

See the `Steering Committee Membership Guidelines <https://github.com/ansible/community-docs/blob/main/steering_committee_membership_guidelines.rst>`_ to learn details.

New Policy/Proposals & Inclusion Requests
=========================================

* The Committee uses the `community-topics repository <https://github.com/ansible-community/community-topics/issues>`_ to asynchronously discuss with the Community and vote on Community topics in corresponding issues.

* Create a new issue in the `community-topics repository <https://github.com/ansible-community/community-topics/issues>`_ as a discussion topic if you want to discuss an idea that impacts any of the following:

  * Ansible Community
  * Community collection best practices and requirements
  * Community collection inclusion policy
  * The Community governance
  * Other proposals of importance that need the Committee's or overall Ansible community attention

* Changes to the inclusion policy and collection requirements are submitted through a new pull request to the `ansible-collections/overview <https://github.com/ansible-collections/overview>`_ repository and a corresponding issue containing their rationale is created in the `community-topics repository <https://github.com/ansible-community/community-topics/issues>`_ repository.

* New collection inclusion requests are submitted through a new discussion in the `ansible-inclusion <https://github.com/ansible-collections/ansible-inclusion/discussions/new>`_ repository.

Depending on a topic you want to discuss with the Community and the Committee, as you prepare your proposal, please consider the requirements established by:

* `Ansible Community Code of Conduct <https://docs.ansible.com/ansible/latest/community/code_of_conduct.html#code-of-conduct>`_.
* `Ansible Collection Requirements <https://github.com/ansible-collections/overview/blob/main/collection_requirements.rst>`_.
* `Ansible Collection Inclusion Checklist <https://github.com/ansible-collections/overview/blob/main/collection_checklist.md>`_.

Community Topics Workflow
-------------------------

The Committee uses the `Community-topics workflow <https://github.com/ansible-community/community-topics/blob/main/community_topics_workflow.md>`_ to asynchronously discuss and vote on the `community-topics <https://github.com/ansible-community/community-topics/issues>`_.

The quorum, the minimum number of Committee members who must vote on a topic in order for a decision to be officially made, is half of the whole number of the Committee members. If the quorum number contains a fractional part, it is rounded up to the next whole number. For example, if there are thirteen members currently in the committee, the quorum will be seven.

Votes must always have "no change" as an option.

In case of equal numbers of votes for and against a topic, the chairperson's vote will break the tie. For example, if there are six votes for and six votes against a topic, and the chairperson's vote is among those six which are for the topic, the final decision will be positive. If the chairperson has not voted yet, other members ask them to vote.

For votes with more than two options, one choice must have at least half of the votes. If two choices happen to both have half of the votes, the chairperson's vote will break the tie. If no choice has at least half of the votes, the vote choices have to be adjusted so that a majority can be found for a choice in a new vote.

Collection Inclusion Requests Workflow
--------------------------------------

When reviewing community collection `inclusion requests <https://github.com/ansible-collections/ansible-inclusion/discussions>`_, the Committee members check if a collection adheres to the `Community collection requirements <https://github.com/ansible-collections/overview/blob/main/collection_requirements.rst>`_.

#. A Committee member who conducts the inclusion review copies the `Ansible community collection checklist <https://github.com/ansible-collections/overview/blob/main/collection_checklist.md>`_ into a corresponding `discussion <https://github.com/ansible-collections/ansible-inclusion/discussions>`_.

#. In the course of the review, the Committee member marks items as completed or leaves a comment saying whether the reviewer expects an issue to be addressed or whether it is optional (for example, it could be **MUST FIX:** <what> or **SHOULD FIX:** <what> under an item).

#. For a collection to be included in the Ansible community package, the collection must be reviewed and approved by, at least, two Committee members.

#. After the collection gets two or more Committee member approvals, a Committee member creates a `community topic <https://github.com/ansible-community/community-topics/issues>`_ linked to the corresponding inclusion request. The issue's description says that the collection has been approved by two or more Committee members and establishes a date (a week by default) when the inclusion decision will be considered made. This time period can be used to raise concerns.

#. If no objections are raised up to the established date, the inclusion request is considered successfully resolved. In this case, a Committee member:

  #. Declares the decision in the topic and in the inclusion request.
  #. Moves the request to the ``Resolved reviews`` category.
  #. Adds the collection to the ``ansible.in`` file in a corresponding directory of the `ansible-build-data repository <https://github.com/ansible-community/ansible-build-data>`_.
  #. Announces the inclusion through the `Bullhorn newsletter <https://github.com/ansible/community/wiki/News#the-bullhorn>`_.
  #. Closes the topic.

Meetings
========

See the Community Working Group meeting `schedule <https://github.com/ansible/community/blob/main/meetings/README.md#wednesdays>`_.

Meeting summaries are posted in the `Community Working Group Meeting Agenda <https://github.com/ansible/community/issues?q=is%3Aopen+label%3Ameeting_agenda+label%3Acommunity+>`_ issue.

.. note::

  Participation in the Community Working Group meetings is optional for Committee members. Decisions on community topics are made asynchronously in the `community-topics <https://github.com/ansible-community/community-topics/issues>`_ repository.

The meeting minutes can be found at the `fedora meetbot site <https://meetbot.fedoraproject.org/sresults/?group_id=ansible-community&type=channel>`_ and the same is posted to `Ansible Devel Mailing List <https://groups.google.com/g/ansible-devel>`_ after every meeting.
