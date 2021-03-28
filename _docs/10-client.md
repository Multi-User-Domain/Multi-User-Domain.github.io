---

layout: doc
title: Game Client
lang: en
lang-ref: game-client
---

{% include early-dev-disclaimer.md %}

A MUD Game Client (from hereon referred to as the "Client") is a type of client-side application which is written to interface with the MUD Servers in order to provide the user with a playable game.

# Requirements

## User and "POD" Management

The user connects to a client application of their choice via their [Solid POD](https://solidproject.org), essentially this is a datastore controlled by the user, and a semantic extension of OIDC which allows them to authenticate it with any number of applications.

The Client MAY provide registration functionality for a user, in which case when carrying this out it SHOULD store on the user's profile a [mud:Account](https://github.com/Multi-User-Domain/vocab/blob/main/mud.ttl#L78) entry. At the time of writing it will also need to initialise an empty [mud:CharacterList](https://github.com/Multi-User-Domain/vocab/blob/main/mud.ttl#L82) due to serverside limitations.

MUD Servers of any kind are written with the assumption that they do not have permission to access the client's data-store and should not seek it. This means that any client which interfaces with an Action Server MUST effect any changes returned from the Action Server which operate on data from the user's POD. The Client SHOULD ask the user to confirm before making the POD-side changes.

# Responsibilities

## Quality Control

The Client is responsible for managing the user's experience, and so cannot expect that the Content Servers and Action Servers it interacts with will all produce high-quality content. The Client SHOULD filter the content the player interacts with and prioritise on quality, and it SHOULD allow the user to set policy in this regard, for example blocking poor quality servers.

The Client is responsible for defining its own metrics on what "good quality" means (TODO: make some suggestions).