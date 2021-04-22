---

layout: doc
title: World Server
lang: en
lang-ref: world-server
---

{% include early-dev-disclaimer.md %}

A World Server is responsible for the shared data storage and is the source of Truth for a world on the MUD. It has the basic requirements of a datastore.

# Requirements

* Calling GET with no parameters on the configured `mud:worldEndpoint` SHOULD return the default graph of the world. Currently this means the entire physical world, but since we're only using small amounts of debug data at the moment, it's not a priority issue.

# Future Developments - Notes For Contributors

* Supporting an intelligent data store and CMS is effort we might not need to make. There is an [open issue](https://github.com/Multi-User-Domain/mud-jena/issues/32) about using Neo4J's graph storage via [neosemantics](https://neo4j.com/labs/neosemantics/), and about using AtomGraph's [LinkedDataHub](https://atomgraph.github.io/LinkedDataHub/), a triplestore using Tomcat and Jena (like MUD-Jena).