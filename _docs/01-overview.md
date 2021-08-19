---

layout: doc
title: High Level View
lang: en
lang-ref: overview
---

# What is the MUD?

At its' core, the MUD is a set of specifications pertaining to a particular way to build a decentralised game.

## What is a decentralised game?

Traditionally, an online game involves one client and one server. The player requests their actions with the client, e.g. by pressing the keys for move forward and move backward. The server chooses how to respond, and replies to the client telling the player what has happened. The game is therefore _centralised_ by the server which controls all.

In a decentralised game therefore, the game is controlled by many parties working in tandem. This opens new possibilities in building a game which is built collaboratively by a community.

## Worlds (Game Data)

The user's store their personal data. Imagine this as a spaceship (actually a [Solid Pod](https://solidproject.org)), containing all of the data which a user can take with them between different worlds.

A **World** is the part of the specification responsible for _storing_ shared data, e.g. the towns and villages of a virtual world. The responsibility of the world is to manage access to this data and control who can change what.

Note that the world server does not necessarily know all of the ways in which the world data can be changed (e.g. the construction of a building) - this is the point. It's simply a way in which a space can be shared in common between players.

## Interaction (Game State Changes)

The **Interaction** part of the specifications refers to the standards and endpoints used to _act_ in a virtual world, for example to order a drink in a bar or to build a house. The actions themselves are self-describing, meaning that a client follows the protocol in order to discover them, the client doesn't need to be written and tailored in advance for each specific action, nor does the world server. This is one of the key strengths which makes writing a decentralised game worth it.

One thing to note is that the client which is carrying out a given action is not necessarily a human player. Endpoints can be made available to robots, for example to carry out population growth simulation on a world server.

## Content (Player Experience)

Other than interacting with the world, the player needs to experience it through their senses. The client application is probably running on the web browser and implenting the client specification, and it is responsible for building an interface which the player can use to explore and interact with the world. This refers to the interface for user input but also for deciding how to render the data to the user, for example in a text-based format or as a comic book.

The client will work closely with the **Content** specification, which describes the process a server follows to assist the client in describing the data to the user. For example, there are models defined to describe character perspective, including verbs such as "sees" and "hears".

## Game Progression

The MUD is a sandbox in the sense that it's not designed with a centralised narrative in mind - the joy is intended in exploring and shaping the worlds around you, and interacting with other players. In this sense the narrative is built by the player - like a role-playing game.

Building centralised narratives over this layer of freedom is an interesting question!
