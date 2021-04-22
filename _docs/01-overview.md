---

layout: doc
title: High Level View
lang: en
lang-ref: overview
---

Whilst the codebases are useful, the MUD project is at its core a set of specifications for building and interfacing open virutal worlds.

**"Open"**: in order to be open a MUD server MUST supply [Linked Data](https://www.w3.org/TR/ldp/) content to the front-end, at minimum in Turtle format.

In the specifications, and in the codebases, we provide a separation of concerns:
* The **World Server** stores the shared data, e.g. the towns and villages of a virtual world, and manages the access to it.
* The User's [POD](https://solidproject.org): provides identity to the user, and a means for the user's to store their own data, portable between different worlds (e.g. characters and possessions).
* The **Client Application** refers to a front-end client which accesses a single MUD server or a federation of servers in order to provide its user with perspective, and/or the ability to _act_ in that world.
* The **Content Server** refers to the standards and endpoints used to _describe_ the data in a virtual world, when it's needed for a human player. This is the component which, given an agent and an object, tells you what they see, and maybe how they feel about it. It might infer that there's a game on at the stadium, so it's noisy, and it might be one in a chain of content servers used by the client to build a game.
* The **Action Server** refers to the standards and endpoints used to _act_ in a virtual world, for example to order a drink in a bar or to build a house. It may be exposed to any actor, human or otherwise, to effect changes on the virtual world.
