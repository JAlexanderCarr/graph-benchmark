======
Papers
======

Bundling Linked Data Structures for Linearizable Range Queries
==============================================================

The Bundled References implementation described in this paper
serve as the inspiration for applying Bundled References to a
graph database.  The goal of my project is to take this
implementation of Bundled References and add additional update
functionality.  Then, using an augmented Bundled References
data structure, adapt a graph database that uses linked data
structures to use Bundled References instead.  The goal is for
this adaptation to increase the performance of range queries
on graph database nodes.  `Bundling Linked Data Structures for
Linearizable Range Queries`_ was authored by Jacob Nelson-Slivon,
Ahmed Hassan, and Roberto Palmieri.

.. _Bundling Linked Data Structures for Linearizable Range Queries: https://arxiv.org/abs/2201.00874

Abstract
--------

We present bundled references, a new building block to provide
linearizable range query operations for highly concurrent
lock-based linked data structures. Bundled references
allow range queries to traverse a path through the data
structure that is consistent with the target atomic snapshot. We
demonstrate our technique with three data structures: a
linked list, skip list, and a binary search tree. Our evaluation
reveals that in mixed workloads, our design can improve
upon the state-of-the-art techniques by 1.2x-1.8x for a skip
list and 1.3x-3.7x for a binary search tree. We also integrate
our bundled data structure into the DBx1000 in-memory
database, yielding up to 40% gain over the same competitors.

Black-box Concurrent Data Structures for NUMA Architectures
===========================================================

Besides applying Bundled References to graph databases, there
are other ways of achieving higher performance.  One of those ways is
through taking advantage of NUMA architectures.  The reason for
reviewing this paper was to create a better understanding
of how data structures could be adapted to take full
advantage of NUMA machines.  `Black-box Concurrent
Data Structures for NUMA Architectures`_ was authored by Irina Calciu,
Siddhartha Sen, Mahesh Balakrishnan, and Marcos K. Aguilera.

.. _Black-box Concurrent Data Structures for NUMA Architectures: https://dl.acm.org/doi/pdf/10.1145/3093336.3037721

Abstract
--------

High-performance servers are Non-Uniform Memory Access (NUMA) machines.
To fully leverage these machines, programmers need efficient concurrent
data structures that are aware of the NUMA performance artifacts. We
propose Node Replication (NR), a black-box approach to obtaining such
data structures. NR takes an arbitrary sequential data structure and
automatically transforms it into a NUMA-aware concurrent data structure
satisfying linearizability. Using NR requires no expertise in concurrent
data structure design, and the result is free of concurrency bugs. NR
draws ideas from two disciplines: shared-memory algorithms and distributed
systems. Briefly, NR implements a NUMA-aware shared log, and then uses the
log to replicate data structures consistently across NUMA nodes. NR is best
suited for contended data structures, where it can outperform lock-free
algorithms by 3.1x, and lock-based solutions by 30x. To show the benefits
of NR to a real application, we apply NR to the data structures of Redis,
an in-memory storage system. The result outperforms other methods by up to
14x. The cost of NR is additional memory for its log and replicas.

NUMASK: High Performance Scalable Skip List for NUMA
====================================================

To dive a bit deeper on NUMA performance improvements, I reviewed a paper
that used NUMA to speed up implementation of a skip list, which is a linked
data structure that could also be adapted for Bundled References.  Therefore,
my goal was to consider the benefits of using Bundled References and NUMA aware
linked data structures in graph databases.  `NUMASK: High Performance Scalable
Skip List for NUMA <https://drops.dagstuhl.de/opus/volltexte/2018/9807/pdf/LIPIcs-DISC-2018-18.pdf>`_
was authored by Henry Daly, Ahmed Hassan, Michael F. Spear, and Roberto Palmieri.

Abstract
--------

This paper presents NUMASK, a skip list data structure specifically designed to exploit the
characteristics of Non-Uniform Memory Access (NUMA) architectures to improve performance.
NUMASK deploys an architecture around a concurrent skip list so that all metadata accesses
(e.g., traversals of the skip list index levels) read and write memory blocks allocated in the NUMA
zone where the thread is executing. To the best of our knowledge, NUMASK is the first NUMA-
aware skip list design that goes beyond merely limiting the performance penalties introduced by
NUMA, and leverages the NUMA architecture to outperform state-of-the-art concurrent high-
performance implementations. We tested NUMASK on a four-socket server. Its performance
scales for both read-intensive and write-intensive workloads (tested up to 160 threads). In write-
intensive workload, NUMASK shows speedups over competitors in the range of 2x to 16x.

Harnessing Epoch-based Reclamation for Efficient Range Queries
==============================================================

Bundled References uses an epoch based global timestamp to order
references, which greatly speeds up range queries.  A competing
linked data structure described in this paper also utilizes an
epoch based global timestamp to speed up range queries as well.
I reviewed this paper in order to get a better understanding of
how this implementation differs from Bundled References, and
consider if there are any graph database applications for this
linked data structure.  `Harnessing Epoch-based Reclamation for
Efficient Range Queries`_ was authored by Maya Arbel-Raviv and
Trevor Brown.

.. _Harnessing Epoch-based Reclamation for Efficient Range Queries: https://dl.acm.org/doi/pdf/10.1145/3200691.3178489

Abstract
--------

Concurrent sets with range query operations are highly desirable
in applications such as in-memory databases. However, few set
implementations offer range queries. Known techniques for augmenting
data structures with range queries (or operations that can be used
to build range queries) have numerous problems that limit their
usefulness. For example, they impose high overhead or rely heavily
on garbage collection. In this work, we show how to augment data
structures with highly efficient range queries, without relying
on garbage collection. We identify a property of epoch-based memory
reclamation algorithms that makes them ideal for implementing range
queries, and produce three algorithms, which use locks, transactional
memory and lock-free techniques, respectively. Our algorithms are
applicable to more data structures than previous work, and are
shown to be highly efficient on a large scale Intel system.

Constant-Time Snapshots with Applications to Concurrent Data Structures
=======================================================================

Another competing linked data structure optimized for range queries is
versioned CAS (vCAS), which is described in this paper.  This implements
a unique way of subsituting new verions of linked nodes during a compare
and swap operation.  I reviewed this paper to analyze the performance of
vCAS in relation to Bundled References.  `Constant-Time Snapshots with
Applications to Concurrent Data Structures`_ was authored by Yuanhao Wei,
Naama Ben-David, Guy E. Blelloch, Panagiota Fatourou, Eric Ruppert, and
Yihan Sun.

.. _Constant-Time Snapshots with Applications to Concurrent Data Structures: https://dl.acm.org/doi/pdf/10.1145/3437801.3441602

Abstract
--------

Given a concurrent data structure, we present an approach
for efficiently taking snapshots of its constituent CAS objects.
More specifically, we support a constant-time operation that
returns a snapshot handle. This snapshot handle can later be
used to read the value of any base object at the time the snap-
shot was taken. Reading an earlier version of a base object
is wait-free and takes time proportional to the number of
successful writes to the object since the snapshot was taken.
Importantly, our approach preserves all the time bounds and
parallelism of the original data structure.

Our fast, flexible snapshots yield simple, efficient imple-
mentations of atomic multi-point queries on a large class
of concurrent data structures. For example, in a search tree
where child pointers are updated using CAS, once a snapshot
is taken, one can atomically search for ranges of keys, find
the first key that matches some criteria, or check if a collec-
tion of keys are all present, simply by running a standard
sequential algorithm on a snapshot of the tree.

To evaluate the performance of our approach, we apply it
to three search trees, one balanced and two not. Experiments
show that the overhead of supporting snapshots is low across
a variety of workloads. Moreover, in almost all cases, range
queries on the trees built from our snapshots perform as well
as or better than state-of-the-art concurrent data structures
that support atomic range queries.

G-Tran: A High Performance Distributed Graph Database with a Decentralized Architecture
=======================================================================================

G-Tran is a graph database implementation that uses a Multi-Version Optimistic
Concurrency Control (MV-OCC) mechanism to address large read or write sets, very similar
to a range query.  This MV-OCC system acts very similarly to Bundled References,
just implemented in a different way.  Reviewing this paper provided a deep dive into
a graph database that is adapted for increased performance on range queries, which
is the goal of using Bundled References in a graph database implementation.  `G-Tran:
A High Performance Distributed Graph Database with a Decentralized Architecture
<https://www.vldb.org/pvldb/vol15/p2545-chen.pdf>`_ was authored by Hongzhi Chen,
Changji Li, Chenguang Zheng, Chenghuan Huang, Juncheng Fang, James Cheng, and Jian
Zhang.

Abstract
--------

Graph transaction processing poses unique challenges such as ran-
dom data access due to the irregularity of graph structures, low
throughput and high abort rate due to the relatively large read/write
sets in graph transactions. To address these challenges, we present
G-Tran, a remote direct memory access (RDMA)-enabled distributed
in-memory graph database with serializable and snapshot isolation
support. First, we propose a graph-native data store to achieve
good data locality and fast data access for transactional updates
and queries. Second, G-Tran adopts a fully decentralized architec-
ture that leverages RDMA to process distributed transactions with
the massively parallel processing (MPP) model, which can achieve
high performance by utilizing all computing resources. In addition,
we propose a new multi-version optimistic concurrency control
(MV-OCC) protocol with two optimizations to address the issue of
large read/write sets in graph transactions. Extensive experiments
show that G-Tran achieves competitive performance compared
with other popular graph databases on benchmark workloads.

