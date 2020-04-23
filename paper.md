---
title: 'HPX - The C++ Standard Library for Parallelism and Concurrency'
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
    affiliation: "5"
  - name: Agustín Berge
    affiliation: "6"
  - name: John Biddiscombe
    orcid: 0000-0002-6552-2833
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
  - name: Zahra Khatami
    orcid: 0000-0001-6654-6856
    affiliation: "7"
  - name: Auriane Reverdell
    orcid: 0000-0002-5531-0458
    affiliation: "4"
  - name: Mikael Simberg
    orcid: 0000-0002-7238-8935
    affiliation: "4"
  - name: Bibek Wagle
    orcid: 0000-0001-6619-7115
    affiliation: "1"
  - name: Weile Wei
    orcid: 0000-0002-3065-4959
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
 - name: Swiss National Supercomputing Centre
   index: 4
 - name: NVIDIA
   index: 5
 - name: STE$||$AR Group
   index: 6
 - name: Oracle
   index: 7
date: \today
bibliography: paper.bib

---

# Summary

HPX is a C++ Standard Library for Concurrency and Parallelism [@heller2017hpx; @hpx_github; @tabbal2011preliminary] for distributed and parallel prgramming based on an Asynchronous Many Task (AMT) runtime system. It implements all of the corresponding facilities as defined by the ISO C++ Standard. Additionally, in HPX we implement functionalities proposed as part of the ongoing C++ standardization process. 

In the following, the compoments of HPX and their references are listed:

- Thread Manager [@kaiser2009parallex] handles the light-weighted user level threads. HPX provides follwing pre-defined scheduling olicues: static, thread local, and hierarchical.
- Performance counters [@grubel2016dynamic]
- Parcelport [@kaiser2009parallex; @biddiscombe2017zero] as an active-message networking layer that enables running functions close to the objects they operate on. This also
implicitly overlaps computation and communication. For the communication between nodes the tcp protocol, the Message passing Interface (MPI), or libfabric [@daiss2019piz] is supported.
- Active Global Address Space (AGAS) [@kaiser2014hpx] that supports load balancing via object migration and enables exposing a uniform API for local and remote execution.
- Autonomic Performance Environment for Exascale (APEX) [@huck2015autonomic], an in-situ profiling and adaptive tuning framework.
- Integration of GPUs with HPX.Compute [@copik2017using] and HPXCL [@diehl2018integration; @martin_stumpf_2018_1409043] for providing a single source solution to heterogeneity.

HPX is utilzed in a diverse set of applications: Octo-Tiger [@@daiss2019piz; @heller2019harnessing; @pfander2018accelerating], a astrophysic code for stellar mergers, libGeoDecomp [@Schafer:2008:LGL:1431669.1431721], a library for stencil code based computer simulations, and NLMech [@diehl2018implementation], a simulation tool for non-local models, e.g. Peridyanmics.

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
