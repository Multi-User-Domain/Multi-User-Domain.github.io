---

layout: doc
title: Scene and Perspective
lang: en
lang-ref: scene
---

{% include early-dev-disclaimer.md %}

A Scene refers to a graph containing models pertaining to resources within a user's perspective, for example the characters, buildings and context of the café in which a player happens to be sat.

Both Action and Content server provide features using scenes - the Content Server might describe it and the Action Server might analyse it to find available actions.

# Implementation

## Scene Generation

A simple client can POST a scene description by dumping the characters and objects which it knows to be present - and this is valid - but the client MAY also seek to "develop" the scene beforehand, for example by making a call to a Scene Generation endpoint which integrates.

At the time that the client passes a scene to the scene description utility, it SHOULD be considered final and the Content Server SHOULD NOT generate any new objects into the scene, which for example frees the client to asynchronously call many Content Servers with the finished scene.

If the server supports scene generation, then it SHOULD return a `mud:sceneGenerationEndpoint` property in its [MUD Configuration]({{ 'docs/02-server-discovery' | relative_url }}), with a URL value where the endpoint can be found. The endpoint, if supported, MUST receive a POST request, with the data containing an RDF graph of resources to be included in the scene. The endpoint should inspect this graph, insert any generated content and return the completed graph with a status code `200`.

## Scene Contents

The contents of the Scene SHOULD include the objects which were passed by the client in the request, and any physical world objects which have been injected, for example a generated character whom the player could talk to.

TODO: The Scene MAY also include contextual, non-physical objects including social context and abstract information.

# Notes

The server MAY incur side-effects to World state during the scene generation if it chooses - for example triggering an event.

A client MAY or MAY NOT confirm the perspective and show it to the player. The act of calling the Scene generation endpoint SHOULD NOT be considered in the server to meaning that the player is committed to the scene. 
