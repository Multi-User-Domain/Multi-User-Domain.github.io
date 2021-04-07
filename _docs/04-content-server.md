---

layout: doc
title: Content Server
lang: en
lang-ref: content-server
---

{% include early-dev-disclaimer.md %}

A Content Server is responsible for accepting data input, describing a **scene**, annotating it with content (text, audio, ..?) and returning this data in the response. It MAY also be involved in the building of the scene.

# Requirements

## Description Format

A Content Server MUST return any found content using the format outlined in the [MUDContent Vocabulary](https://github.com/Multi-User-Domain/vocab/blob/main/mudcontent.ttl).

<img src="https://user-images.githubusercontent.com/10801930/112872247-0cea5c80-90b8-11eb-8a7a-c4e7ff56c208.png" class="blog-full-image" alt="A directed RDF graph showing how a MUDContent object is structured. A foaf:Agent has a property 'sees' directed to a mudcontent:Content resources, which in turn has properties 'hasText' and 'hasImage', alongside a key property 'describes' which points to the resource the Content is describing" />

At some point the Content Server configuration might return `mudcontent:serverSupportsContentFormat` triples, but at the moment it's implicit that only this format can be suppoorted. If you have your own ideas then please go implement and let us know we need to update the documentation :-)

# Features

## Scene Description

A Content Server MAY support the description of a scene, advertising the endpoint during the Content Server Discovery.

If a Content Server advertises support for `mud:SceneDescription`, then it MUST accept a `POST` request on the advertised endpint. The Client requesting the scene description MUST submit in the `POST` body the uris of all objects in the scene which the server should describe. The Content Server SHOULD look at each and search for a description on that resource.

The Content Server MAY implement the "Content Describer" pattern used in the Apache Jena Action Server code. TODO: write-up a description of this pattern and link to it.

## Simple Object Description

A Content Server MAY support the simple description of an object.

If a Content Server advertises support for `mud:SimpleObjectDescription`, then it MUST accept a `GET` request on the advertised endpoint, accepting the object uri on the `uri` query parameter.