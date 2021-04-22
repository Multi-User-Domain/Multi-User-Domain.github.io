---

layout: doc
title: Action Server
lang: en
lang-ref: action-server
---

{% include early-dev-disclaimer.md %}

An Action Server is a resource which exposes views to make actions on a World Server. The World Server may be on the same host or it may be distant. The World Server may expose other endpoints of its own to POST/PUT/PATCH data and generally speaking the Action Server is providing only specialised versions of these, for example for a game action which has side-effects.

# Discovery

TODO: currently in development. During Action Discovery, the client will discover the ways in which it can interact with a given graph via the providing Action Server. For example, I might give it a location, and it might return a Transit Activity endpoint for me to use.

# Acting

An Action Server MUST expose an endpoint "Act", which accepts `POST` or `GET` operations. 

The `POST` operation MUST accept the `taskUri` as a query parameter (pointing to the **type** of task being completed, e.g. `mudlogic:Transit`), and in the POST body a graph including the arguments needed to create the ask, i.e. a character model and a destination. Upon completion the Action Server MUST return HTTP response `201` with the URI of the created record in the `Location` header. It MAY also return the created action in the Response body.

The `GET` operation MUST accept the `taskUri` as a query parameter (this time pointing to the created task resource itself). The Client MAY NOT have sent a task which is stored on, or was created by the Action Server itself. During this operation the Action Server MAY complete any serverside checks on the action (e.g. if a Task been completed), but it MUST return `200` with the Requested Action resource, or an error. If the task is returned completed, then the Action Server SHOULD effect any changes to local datastores (if it is also a World Server, for example), and the Client SHOULD effect the changes to other data stores. The reasons for this [are outlined in this open issue about trust](https://github.com/Multi-User-Domain/Multi-User-Domain.github.io/issues/2).

The Action Server MUST advertise the endpoint through the [MUD Discovery]({{ 'docs/11-server-discovery' | relative_url }}) mechanism.

## Features

### Action Pre-requisites

An Action MAY have pre-conditions which must be true in order for the action to be carried out. This is the responsibility of the Action's endpoint to define and enforce. It MAY read the pre-condition from a data-entry on the Action, or it can be hardcoded in the endpoint's logic, depending on the developer's preference.

### Tasks

A Task is an Action of type `time:Interval`. It has a duration, a start-time, an end-time (which may be delayed if the task is paused), and `mudlogic:endState` consequences (which model the changes in state when the action is completed).