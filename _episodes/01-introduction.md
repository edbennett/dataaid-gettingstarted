---
title: "Introduction"
teaching: 5
exercises: 0
questions:
- "What does the infrastructure we'll be using look like?"
objectives:
- "Understand the setup of the machine we'll be using."
keypoints:
- "Sunbird is a supercomputer, which has login nodes, compute nodes, and storage."
- "The joint DI-AIMLAC CDT has some dedicated compute nodes and storage"
- "The dedicated storage is not accessible from the rest of the compute nodes for security"
---

For the DataAid challenge, we will be making use of the Sunbird supercomputer at Swansea University. This is part of the Supercomputing Wales infrastructure. A complete introduction to High-Performance Computing is beyond the scope of this lesson; the interested learner can visit [the Introduction to High Performance Computing with Supercomputing Wales](https://supercomputingwales.github.io/SCW-tutorial).

To cut a long story short, modern supercomputers (or _clusters_), including Sunbird, comprise a large number of relatively but not incredibly powerful servers, or _nodes_, linked together by a high-speed network. Most of these nodes are used for performing computations (compute nodes), a few are used for storage (which is made available over the network to the other nodes), and a handful are used interactively to manage the tasks running on the cluster (login nodes). The last of these is where you as a user will usually log in, to leave the compute nodes free to run the computationally-intensive tasks that the cluster is used for.

The joint DI-AIMLAC CDT has procured some additional nodes that are attached to Sunbird, specifically, two compute nodes and a storage node. Currently, to ensure that the charity data are kept secure and confidential, the CDT storage is connected only to the CDT compute nodes and an extra gateway node, and cannot be accessed from the main Sunbird login or compute nodes.

Note that Supercomputing Wales receives funding from the European Union via the Welsh Government to facilitate its activities. As such, we have to impose certain requirements. Specifically:

* When you publish work that has made use of the Supercomputing Wales facilities in its production, you must include the following text in the Acknowledgements section of the publication: "We acknowledge the support of the Supercomputing Wales project, which is part-funded by the European Regional Development Fund (ERDF) via Welsh Government.".
* If you apply for funding that is enabled by the use of the Supercomputing Wales facilities (either in the preparation of the application, or in carrying out the work of the grant), then please explicitly mention Supercomputing Wales in the proposal. If it is awarded, then we would appreciate a statement attributing the grant to Supercomputing Wales, so that we can report back to Welsh Government that the funding was enabled by Supercomputing Wales.

The Supercomputing Wales project `scw1738` has been set up to give access to the facilities for the DataAid challenge. If you want to keep using Supercomputing Wales facilities for your own research after the event, you will need to join or create a new project. Please talk to your local Supercomputing Wales RSEs if you need help with this (if you're at Bristol, talk to the Swansea team in the first instance).

{% include links.md %}

