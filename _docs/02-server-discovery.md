---

layout: doc
title: Saying Hello. Server Discovery
lang: en
lang-ref: server-discovery
---

{% include early-dev-disclaimer.md %}

With the knowledge that we're building a platform in which the client is "server-agnostic" and the server is "client-agnostic", meaning that a client will connect its users to more than one MUD-providing servers and that neither the server nor the client can know at developer-time which client or server it will be pairing with (it's up to the user).

Evidently the first problem that the two will face, then, will be saying hello.

More specifically, we need the server to explain to the client what features it supports and where it can find the endpoints for these features. This isn't a new problem, and actually in another domain it's already been solved by the [Open ID Connect Discovery specification](https://openid.net/specs/openid-connect-discovery-1_0.html).

Very roughly, there is one standard endpoint (`/.well-known/openid-configuration/`), at which the server (the identity provider) returns a JSON document describing the features it supports and where to find them.

# Definition of terms

* A **MUD Provider** is a server compatible with our standards and protocols, but that doesn't mean it provides everything, it may provide a subset or a superset of the features outlined in the documentations.

# MUD Configuration endpoint

The MUD is in very early development and we're designing it as we need it. Imaginatively, we're going to use `/.well-known/mud-configuration/` as our standard endpoint for a MUD Provider.

A MUD Provider which provides this endpoint MUST return a graph of `rdf:type` `mud:Configuration`, with at minimum the keys defined in the sections below. The format of this document should be in RDF depending on the request of the client and the support of the server. As a minimum, MUD Providers MUST support Turtle serialization of this document.

## Required Keys

### World Server (Optional)

A MUD Provider which supports a datastore for World Data MUST return a triple for the property `mud:worldEndpoint`. The object of this triple MUST be the location of the [world data endpoint]({{ 'docs/03-world-server' | relative_url }}), E.g. `http://example.org/mud/world/`.

Supporting a World Server is not required and if absent, the Client SHOULD assume that the MUD Provider does not support any World storage functionality.

### Content Server (Optional)

Supporting Content Server functionality is not required.

A MUD Provider which supports [Content Server]({{ 'docs/04-content-server' | relative_url }}) functionality MUST provide one or more of the following endpoint properties for the Content Server:
* `mudcontent:sceneDescriptionEndpoint`
* `mudcontent:simpleObjectDescriptionEndpoint`

The value of these properties MUST be a URL pointing to the location of the respective endpoints, which MUST behave as stated in the relevant parts of the Content Server specification.

### Action Server (Optional)

Supporting Action Server functionality is not required.

A MUD Provider which supports [Action Server]({{ 'docs/05-action-server' | relative_url }}) functionality MUST provide an `mudlogic:actionDiscoveryEndpoint` property. The value of this property MUST be a URL pointing to the location of the endpoint, and it MUST behave as stated in the relevant parts of the Action Server specification.

### Example Configuration

A MUD server configuration with all of the keys expressed in this document, optional or required:

```turtle
@prefix mud: <https://raw.githubusercontent.com/Multi-User-Domain/vocab/main/mud.ttl#>.
@prefix mudcontent: <https://raw.githubusercontent.com/Multi-User-Domain/vocab/main/mudcontent.ttl#>.
@prefix mudlogic: <https://raw.githubusercontent.com/Multi-User-Domain/vocab/main/mudlogic.ttl#>.

:configuration a mud:Configuration ;
    mud:worldEndpoint <http://localhost:8080/mud/world/> ;
    mudcontent:sceneDescriptionEndpoint <http://localhost:8080/mud/content/> ;
    mudcontent:simpleObjectDescriptionEndpoint <http://localhost:8080/mud/content/> ;
    mudlogic:actionDiscoveryEndpoint <http://localhost:8000/mud/act/discover/> .
```

### Notes for Contibutors

Notice that by passing the endpoints in a configuration as above, the client no longer has an implicit relationship with the server's API on where to access an endpoint. Notice also that it _does_ still have an implicit relationship regarding _how_ to access that endpoint - the shape of the data it should pass and the shape of the data it should expect back. There are proposals on how to make this part explicit and interoperable too. For more information see the [Git issue](https://github.com/Multi-User-Domain/mud-jena/issues/16).
