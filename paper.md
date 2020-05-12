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
  - name: Steven R. Brandt
    orcid: 0000-0002-7979-2906
    affiliation: "1"
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
  - name: Alireza Kheirkhahan
    orcid: 0000-0002-4624-4647
    affiliation: "1"
  - name: Adrian S. Lemoine
    affiliation: "6"
  - name: Auriane Reverdell
    orcid: 0000-0002-5531-0458
    affiliation: "4"
  - name: Shahrzad Shirzad
    orcid: 0000-0001-9496-8044
    affiliation: "1"
  - name: Mikael Simberg
    orcid: 0000-0002-7238-8935
    affiliation: "4"
  - name: Bibek Wagle
    orcid: 0000-0001-6619-7115
    affiliation: "1"
  - name: Weile Wei
    orcid: 0000-0002-3065-4959
    affiliation: "1"
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
date: 28.05.2020
bibliography: paper.bib
---

# Summary

HPX is a C++ Library for Concurrency and Parallelism [@heller2017hpx; @hpx_github; @tabbal2011preliminary]
for distributed and parallel programming based on an Asynchronous Many Task (AMT) runtime system.
Its main goal is to improve efficiency and scalability by increasing resource utilization and reducing synchronization through providing asynchronization and employing adaptive scheduling. HPX is able to significantly reduce the processor starvation and effective latencies while controlling overheads.
In addition to providing the scalable parallelisms, HPX implements the concurrency mechanisms and parallelism facilities as defined by the ISO C++ Standard yet extends them to run in a distributed context. Furthermore, HPX implements functionalities proposed as part of the ongoing C++ standardization process. [TODO: Maybe adding advantages of having hpx in c++ standardization compared to the other methods that are not?]

[TODO: Maybe talking about HPX future and dataflow and execution policies after going into HPX components!?]

The compoments of HPX and their references are listed below:

- **Thread Manager** [@kaiser2009parallex] The thread manager manages
    the light-weighted user level threads created by HPX. These light-weight threads have extremely short context switching times resulting in the reduced latencies even for very short operations. HPX provides
    follwing pre-defined scheduling olicues **(?)**: static, thread
    local, and hierarchical.
- **Active Global Address Space (AGAS)** [@kaiser2014hpx]
    To support distributed objects, HPX has implemented an address
    resolution component similar to the PGAS model. **Citation**
    This layer enables HPX to exposing a uniform API for local and
    remote execution. Unlike PGAS, however, AGAS provides the user
    with the ability to move global objects in a distributed system
    without needing to create a new Global Identifier (GID)
    This enables AGAS to support load balancing via object migration.
    **More?**
- **Parcelport** [@kaiser2009parallex; @biddiscombe2017zero]
    This component is an active-message networking layer.
    The parcelport is able to leverage AGAS in order to
    launch functions on global objects regardless of where
    they are in a distributed system.
    Additionally its asynchronus protocol enables the
    parcelport to implicitly overlap communication and computation.
    The parcelport is modular to suport multiple communication libary
    backends. By default HPX supports tcp, Message passing Interface (MPI),
    and libfabric [@daiss2019piz].
- **Performance counters** [@grubel2016dynamic]
    HPX provides its users with a uniform suite of global counters
    to monitor system metrics. These counters have
    names registered with AGAS which enables the users to
    easily query for different metrics at runtime. **(Check me)**
    Additionally, HPX provides an API for users to create their
    own counters to gather infromation customize to thier own applicaiton.
    By default HPX provides performance counters for networking,
    AGAS performance, and thread scheduling.
- **Autonomic Performance Environment for Exascale (APEX)** [@huck2015autonomic]
    Often, modern applications must adapt to runtime environments
    to ensure acceptable performance. APEX enables this flexibility
    by accepting user provided policies that are triggered by defined events.
    In this way, features such as parcel coalescing **Cite** can adapt
    to the current phase of an application or eve state of a system.
- **Accelerator Support**
    HPX has suport for two methods of integration with GPUs:
    HPXCL [@diehl2018integration; @martin_stumpf_2018_1409043] and HPX.Compute [@copik2017using]
    HPXCL provides users the ability to manage GPU kernels through a
    global object. This enables HPX to coordinate the launcing and
    synchonization of CPU and GPU code.
    HPX.Compute [@copik2017using] aims to provide a single source
    solution to heterogeneity by automatically generating GPU kernels
    from C++ code. This enables HPX to launch both CPU and GPU kernels
    as dictated by the current state of the system.

HPX is utilzed in a diverse set of applications:
Octo-Tiger [@@daiss2019piz; @heller2019harnessing; @pfander2018accelerating],
a astrophysic code for stellar mergers,
libGeoDecomp [@Schafer:2008:LGL:1431669.1431721],
a library for stencil code based computer simulations,
and NLMech [@diehl2018implementation], a simulation tool
for non-local models, e.g. Peridyanmics.

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
