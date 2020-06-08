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
  - name: Kevin Huck
    orcid: 0000-0001-7064-8417
    affiliation: "8"
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
 - name: Oregon Advanced Computing Institute for Science and Society (OACISS), University of Oregon
   index: 8
date: 28.05.2020
bibliography: paper.bib
---

# Summary

The new challenges presented by Exascale system architectures have resulted in
difficulty achieving a desired scalability using traditional distributed-memory
runtimes. Asynchronous many-task systems (AMT) are based on a new paradigm
showing promises in addressing these challenges, providing application
developers with a productive and performant approach to programming on next
generation systems. HPX is a C++ Library for Concurrency and Parallelism that is
developed by The STE||AR Group, an international group of collaborators working
in the field of distributed and parallel programming
[@heller2017hpx;@hpx_github; @tabbal2011preliminary]. HPX's main goal is to
improve efficiency and scalability of parallel applications by increasing
resource utilization and reducing synchronization through providing an
asynchronous API and employing adaptive scheduling. The consequent use of
futures intrinsically enables overlap of computation and communication and
constraint-based synchronization. HPX is able to maintain load balance among all
the available resources resulting in significantly reducing processor
starvation and effective latencies while controlling overheads. HPX is fully
conforming to the C++ ISO Standards and implements the standardized concurrency
mechanisms and parallelism facilities. Further, HPX extends those facilities to
distributed use cases, thus enabling syntactic and semantic equivalence of local
and remote operation on the API level. HPX uses the C++ future to transform
sequential tasks into wait-free asynchronous executions. Futurization results in
data flow execution trees of potentially millions of lightweight HPX tasks
executed in the
proper order. HPX also provides a work-stealing task scheduler that takes care
of fine-grained parallelizations. Furthermore, HPX implements functionalities
proposed as part of the ongoing C++ standardization process.

![Sketch of HPX's architecture with all the components and their interactions.\label{fig:architecture}](hpx_architecture.pdf)


\autoref{fig:architecture} sketches HPX's architectures. The components of HPX
and their references are listed below:

- **Threading Subsystem** [@kaiser2009parallex] The thread manager manages the
    light-weight user level threads created by HPX. These light-weight threads
    have extremely short context switching times resulting in the reduced latencies
    even for very short operations. HPX provides following pre-defined scheduling
    policies: static, thread local, and hierarchical.
- **Active Global Address Space (AGAS)** [@kaiser2014hpx;@amini2019agas]
    To support distributed objects, HPX supports a global address
    resolution component that is extending the PGAS model to enable runtime based
    resource allocation and data placement.
    This layer enables HPX to expose a uniform API for local and remote
    execution. Unlike PGAS, AGAS provides the user with the ability to
    transparently move global objects in a distributed system. This enables AGAS
    to support load balancing via object migration.
- **Parcel Transport Layer** [@kaiser2009parallex; @biddiscombe2017zero]
    This component is an active-message networking layer.
    The parcelport is able to leverage AGAS in order to
    launch functions on global objects regardless of their current placement
    in a distributed system.
    Additionally its asynchronous protocol enables the
    parcelport to implicitly overlap communication and computation.
    The parcelport is modular to support multiple communication library
    backends. By default HPX supports TCP/IP, Message passing Interface (MPI),
    and libfabric [@daiss2019piz].
- **Performance counters** [@grubel2016dynamic]
    HPX provides its users with a uniform suite of performance counters
    to monitor system metrics that are accessible globally. These counters have
    their names registered with AGAS, which enables the users to
    easily query for different metrics at runtime.
    Additionally, HPX provides an API for users to create their
    own counters to gather information customized to their own application.
    By default HPX provides performance counters for its components, such as
    networking, AGAS operations, thread scheduling, and various statistics.
- **Policy Engine/Policies** [@huck2015autonomic]
    Often, modern applications must adapt to runtime environments
    to ensure acceptable performance. Autonomic Performance Environment for
    Exascale (APEX) enables this flexibility by measuring HPX tasks, monitoring
    system utilization, and accepting user provided policies
    that are triggered by defined events.
    In this way, features such as parcel coalescing [@wagle2018methodology] can
    adapt to the current phase of an application or even state of a system.
- **Accelerator Support**
    HPX has suport for two methods of integration with GPUs:
    HPXCL [@diehl2018integration; @martin_stumpf_2018_1409043] and HPX.Compute
    [@copik2017using]
    HPXCL provides users the ability to manage GPU kernels through a
    global object. This enables HPX to coordinate the launching and
    synchronization of CPU and GPU code.
    HPX.Compute [@copik2017using] aims to provide a single source
    solution to heterogeneity by automatically generating GPU kernels
    from C++ code. This enables HPX to launch both CPU and GPU kernels
    as dictated by the current state of the system.
- **Local Control Objects**
    HPX has support for many of the C++20 primitives, such as `hpx::latch`,
    `hpx::barrier`, and `hpx::counting_semaphore` to synchronize the code or
    overlap computation and communication. These functions are standard conform
    according to the C++20 [@standard2017programming]. For asyncronous computing
    HPX provides `hpx::async` and `hpx::future`, see the second exmaple in the
    next section.
- **Software Resilience**
    HPX supports software level resilience [@gupta2020implementing] through its
    resiliency API, such as `hpx::async_replay` and `hpx::async_replicate` and
    its dataflow counterparts `hpx::dataflow_replay` and
    `hpx::dataflow_replicate`. These APIs are resilient against memory bit
    flips and processor inacurracies.
    HPX provides an easy method to port to resilient API by replacing
    `hpx::async` or `hpx::dataflow` with its resilient API counterpart everywhere
    in the code without making any other changes.
- **C++ Standards conforming API**
    HPX implements all of the C++17 parallel algorithms [@standard2017programming]
    and extends those with asynchronous versions. Here, HPX provides the
    `hpx::execution::seq`, `hpx::execution::par` execution policies, and (as an
    extension) their asynchronous equivalents
    `hpx::execution::seq(hpx::execution::task)` and
    `hpx::execution::par(hpx::execution::task)` (see the first code example
    in the next section).

HPX is utilzed in a diverse set of applications: Octo-Tiger [@daiss2019piz;
@heller2019harnessing; @pfander2018accelerating], an astrophysics code for
stellar mergers; libGeoDecomp [@Schafer:2008:LGL:1431669.1431721], an
auto-parallelizing library to speed up stencil code based computer simulations;
and NLMech [@diehl2018implementation], a simulation tool for non-local models,
e.g. Peridynamics.


# Example code

The following is an example of HPX's parallel algorithms API using execution
policies as defined in
the C++17 Standard [@standard2017programming]. HPX implements all of the
parallel algorithms defined therein. The parallel algorithms extend the classic
STL algorithms by adding an additional first argument (called execution policy).
The `hpx::execution::seq` implies sequential execution while `hpx::execution::par`
will execute the algorithm in parallel.
HPX's parallel algorithm library API is completely standards conforming.

```cpp
#include <hpx/include/parallel_reduce.hpp>
#include <iostream>
#include <vector>

int main()
{
    std::vector<int> values = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};

    // Compute the sum in a sequential fashion
    int sum1 = hpx::reduce(hpx::execution::seq, values.begin(), values.end(), 0);
    std::cout << sum1 << '\n';      // will print 55

    // Compute the sum in a parallel fashion based on a range of values
    int sum2 = hpx::reduce(hpx::execution::par, values, 0);
    std::cout << sum2 << '\n';      // will print 55 as well

    return 0;
}
```

Example for the HPX's concurrency API where the Taylor series for the $\sin(x)$
function is computed. The Taylor series is given by

$$ \sin(x) \approx = \sum\limits_{n=0}^N (-1)^{n-1} \frac{x^{2n}}{(2n)!}.$$

For the concurrent computation, the interval $[0, N]$ is split in two
partitions from $[0, N/2]$ and $[(N/2)+1, N]$ and these are computed
asynchronously using `hpx::async`. Note that each asynchronous function call
returns an `hpx::future` which is needed to synchronize the collection
of the partial results. The future has a `get()` method that returns the result
once the computation of the Taylor function finished. If the result is not ready
yet, the current thread is suspended until the result is ready. Only if
`f1` and `f2` are ready, the overall result will be printed to the standard
output stream.

```cpp
#include <hpx/include/future.hpp>
#include <cstddef>
#include <cmath>
#include <iostream>

// Define the partial taylor function
double taylor(std::size_t begin, std::size_t end, std::size_t n, double x)
{
    double res = 0;
    for (std::size_t i = begin; i != end; ++i)
    {
        res += std::pow(-1, i - 1) * std::pow(x, 2 * n) / factorial(2 * n);
    }
    return res;
}

int main()
{
    // Compute the Talor series sin(2.0) for 100 iterations
    std::size_t n = 100;

    // Launch two concurrent computations of each partial result
    hpx::future<double> f1 = std::async(taylor, 0, n / 2, n, 2.);
    hpx::future<double> f2 = std::async(taylor, (n / 2) + 1, n, n, 2.);

    // Introduce a barrier to gather the results
    double res = f1.get() + f2.get();

    // Print the result
    std::cout << "Sin(2.) = " << res << std::endl;
}
```

Please report any bugs or feature requests on the HPX's
[GitHub](https://github.com/STEllAR-GROUP/hpx) page.

# Acknowledgments

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
