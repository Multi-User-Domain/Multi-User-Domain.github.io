---

layout: doc
title: High Level View
lang: en
lang-ref: overview
---

In essence the MUD is a platform for building shared virtual worlds and exposing them to agents, be they web crawlers designed to simulate changes in bird migrations or front-end applications designed to provide eyes and ears to a human player.

Through this we provide a separation of concerns:
* The **World Server** stores the shared data, e.g. the towns and villages of a virtual world, and manages the access to it.
* The User's [POD](https://solidproject.org): provides identity to the user, and a means for the user's to store their own data, portable between different worlds (e.g. characters and possessions).
* The **Content Server** refers to the standards and endpoints used to _describe_ the data in a virtual world, when it's needed for a human player. This is the component which, given an agent and an object, tells you what they see, and maybe how they feel about it. It might infer that there's a game on at the stadium, so it's noisy, and it might be one in a chain of content servers used by the client to build a game.
* The **Action Server** refers to the standards and endpoints used to _act_ in a virtual world, for example to order a drink in a bar or to build a house. It may be exposed to any actor, human or otherwise, to effect changes on the virtual world.

It's worth stating explicitly that MUD is a **decentralised** platform intended to be highly extensible, which means that the worlds and clients need to agree on a protocol to communicate through and tolerate differences. The client in particular should be as **backend-agnostic** as possible and should avoid containing world logic within it. It means that the client needs to be directed by the server, and that the server needs to talk with the client about what it can support, how it wants to go about this etc.

RDF data on the semantic web is open by design, making it highly extensible. There is a lot of fun to be had in the building of a world, even without any "text-based adventure", simply by creating a village, coming back in 6 months to find that your village is now a city, or that the bartender at the saloon you visited last week is complaining about another player who came in and challenged them to a duel.

Your world server doesn't have to define what a duel is, what a saloon is or what a memory is, it just needs to allow players and machines to write to it in RDF.

It doesn't have to redefine how to describe what's happening because this concern has been separated to the content server providers.