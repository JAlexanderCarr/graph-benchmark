================
Graph Benchmarks
================

Benchmarking Graph Databases
============================

In order to understand the benefits of implementing Bundled References in
a graph database, measuring performance will be required.  However, there
are many graph database benchmark options available, and they are not created equal.
Each benchmark tests different algorithms and is compatible with a 
specific set of graph databases.  To best evaluate the effect Bundled
References has on a graph database, graph benchmarks will need to be
analyzed as well.

Existing Graph Database Benchmarks
==================================

Graph databases are not new in Computer Science, and as such, there exist many
graph database benchmarks.  However, they each differ on the algorithms they implement
and the databases they are compatible with.  After discovering over 10 possible
graph database benchmarks, I narrowed it down to the two most comprehensive
options, the `Linked Data Benchmark Council (LDBC)`_ and `Graph Benchmark`_.

.. _Linked Data Benchmark Council (LDBC): https://ldbcouncil.org/
.. _Graph Benchmark: https://graphbenchmark.com/

Linked Data Benchmark Council
-----------------------------

LDBC is a group of individuals that have created a set of test suites
that can be used to evaluate the performance of various graph databases.
Although they have many different test suites with varying data sets, their
`Social Network Benchmark (SNB)`_ is the most relevant for testing a graph database
implemented with Bundled References.

The SNB is split into two main workloads, a business intelligence workload focused on
aggregation queries and a interactive workload focused on simpler queries with constant
inserts and updates.  Some of the supported queries include:

* Breadth First Search
* PageRank
* Single-source Shortest Path
* Local Clustering Coefficient

With extensive coverage of features, LDBC is a strong option for benchmarking an
adapted graph database with Bundled References.

.. _Social Network Benchmark (SNB): https://ldbcouncil.org/benchmarks/snb/

Graph Benchmark
---------------

Graph Benchmark was developed by Matteo Lissandrini, Martin Brugnara, and Yannis
Velegrakis.  This benchmark is highly customizable and provides functionality for
a wide range of queries and graph databases.  Just in the example test cases, over
70 different individual and bulk queries are highlighted.  In addition, these tests
also incorporate many different graph databases, including:

* Neo4j
* OrientDB
* Titan
* ArangoDB

Another major benefit of Graph Benchmark is the wide variety of data sets it supports
as well.  In fact, Graph Benchmark supports some data sets created by LDBC, like the
SNB data.  Therefore, due to Graph Benchmark's flexibility, it is the best choice to
benchmark a graph database implementation with Bundled References.

