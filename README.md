Cassandra in Docker
===

This repository provides everything you need to run Cassandra in Docker, and is tuned for fast
container startup.

Why?
---
While naive Cassandra images take around 30 seconds to start, our containers take only a few seconds.
Optimizations include:

* Disabling vnodes. We don't use them at Spotify, and Cassandra starts much faster without them
  (~10 sec).
* Disabling something called "waiting for gossip to settle down" because there is no gossip in a
  one-node cluster (another ~10 sec).

In the box
---
* **connectedhomes/cassandra21**

  This is probably the image you want, it runs a one-node Cassandra cluster.
  Built from the `cassandra` directory.

* **connectedhomes/cassandra21:cluster**

  Runs a Cassandra cluster. Expects `CASSANDRA_SEEDS` and `CASSANDRA_TOKEN` env variables to be set.
  If `CASSANDRA_SEEDS` is not set, node acts as its own seed. If `CASSANDRA_TOKEN` is not set, the
  container will not run. Built from the `cassandra-cluster` directory.

* **connectedhomes/cassandra21:base**

  The base image with an unconfigured Cassandra installation. You probably don't want to use this
  directly. Built from the `cassandra-base` directory.
