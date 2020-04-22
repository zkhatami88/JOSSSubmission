---
title: 'The C++ Standard Library for Parallelism and Concurrency'
tags:
  - concurrency
  - task-based run time system
  - parallelsim
  - distributed  
authors:
  - name: Parsa Amini
    orcid: 0000-0002-6439-8404
    affiliation: "1"
  - name: Bryce Adelstein Lelbach
    orcid: 0000-0002-7995-5226
    affiliation: "4"
  - name: Patrick Diehl
    orcid: 0000-0003-3922-8419
    affiliation: "1"
  - name: Nikunj Gupta
    orcid: 0000-0003-0525-3667
    affiliation: "3"
  - name: Thomas Heller
    orcid: 0000-0003-2620-9438
    affiliation: "2"
  - name: Hartmut Kaiser
    orcid: 0000-0002-8712-2806
    affiliation: "1"
  - name: Weile Wei
    orcid: 0000-0002-3065-4959
    affiliation: "1"
  - name: Bibek Wagle
    orcid: 0000-0001-6619-7115
    affiliation: "1"
  - name: Author will be ordered alphabetical 
    affiliation: "2" # (Multiple affiliations must be quoted)
affiliations:
 - name: Center of Computation \& Technology, Louisiana State University 
   index: 1
 - name: Exasol
   index: 2
 - name: Indian Institute of Technology, Roorkee, India
   index: 3
 - name: NVIDIA
   index: 4
 - name: Institution
   index: 5
date: 13 April 2020
bibliography: paper.bib

---

# Summary

HPX is a C++ Standard Library for Concurrency and Parallelism `[@heller2017hpx]`. It implements all of the corresponding facilities as defined by the C++ Standard. Additionally, in HPX we implement functionalities proposed as part of the ongoing C++ standardization process. We also extend the C++ Standard APIs to the distributed case.

The goal of HPX is to create a high quality, freely available, open source implementation of a new programming model for conventional systems, such as classic Linux based Beowulf clusters or multi-socket highly parallel SMP nodes. At the same time, we want to have a very modular and well designed runtime system architecture which would allow us to port our implementation onto new computer system architectures. We want to use real-world applications to drive the development of the runtime system, coining out required functionalities and converging onto a stable API which will provide a smooth migration path for developers.

The API exposed by HPX is not only modeled after the interfaces defined by the C++11/14/17/20 ISO standard, it also adheres to the programming guidelines used by the Boost collection of C++ libraries. We aim to improve the scalability of today's applications and to expose new levels of parallelism which are necessary to take advantage of the exascale systems of the future.


# Acknowledgements

We would like to acknowledge the NSF, DoE, DTIC, DARPA, the Center for
Computation and Technology (CCT) at Louisiana State University, The Swiss 
National Supercomputing Centre (CSCS), and the Department of Computer Science 3 
- Computer Architecture at the University of Erlangen Nuremberg who fund and 
support our work.

We would also like to thank the following organizations for granting us
allocations of their compute resources: LSU HPC, LONI, XSEDE, NERSC, CSCS/ETHZ,
and the Gauss Center for Supercomputing.

HPX has been funded by:

- The National Science Foundation through awards 1240655 (STAR), 1339782
  (STORM), and 1737785 (Phylanx).

  Any opinions, findings, and conclusions or recommendations expressed in this
  material are those of the author(s) and do not necessarily reflect the views
  of the National Science Foundation.

- The Department of Energy (DoE) through the awards DE-AC52-06NA25396 (FLeCSI)
  and DE-NA0003525 (Resilience).

  Neither the United States Government nor any agency thereof, nor any of their
  employees makes any warranty, express or implied, or assumes any legal
  liability or responsibility for the accuracy, completeness, or usefulness of
  any information, apparatus, product, or process disclosed, or represents that
  its use would not infringe privately owned rights. Reference herein to any
  specific commercial product, process, or service by trade name, trademark,
  manufacturer, or otherwise does not necessarily constitute or imply its
  endorsement, recommendation, or favoring by the United States Government or
  any agency thereof. The views and opinions of authors expressed herein do not
  necessarily state or reflect those of the United States Government or any
  agency thereof.

- The Defense Technical Information Center (DTIC) under contract
  FA8075-14-D-0002/0007

  Neither the United States Government nor any agency thereof, nor any of their
  employees makes any warranty, express or implied, or assumes any legal
  liability or responsibility for the accuracy, completeness, or usefulness of
  any information, apparatus, product, or process disclosed, or represents that
  its use would not infringe privately owned rights.

- The Bavarian Research Foundation (Bayerische Forschungsstiftung) through the
  grant AZ-987-11.

- The European Commission's Horizon 2020 programme through the grant
  H2020-EU.1.2.2. 671603 (AllScale).

# References
