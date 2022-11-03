---

layout: doc
title: Modelling Worlds
lang: en
lang-ref: modelling-worlds
---

The first problem that I came across when approaching modelling a world in a decentralised adventure game is that different games have different needs. For example in my first experiments I had the idea of simply listing Settlements with a few buildings and without geolocation, but another game might have different needs (e.g. it may be unpopulated world in which co-ordinates are important and buildings are not, or it might be a world with 4 dimensional co-ordinates).

The main challenge in the decentralised web is to avoid making too many assumptions, and making your data models flexible.

# Regions

To meet this challenge in the context of world data, I propose to you a simple but extensible system of Regions and sub-Regions:

```turtle
mudworld:Region a mud:Locatable ;
    rdfs:subClassOf mud:Locatable ;
    rdfs:label "Region"@en ;
    rdfs:label "Région"@fr .

mudworld:subRegionOf a rdf:Property ;
    rdfs:label "subRegionOf"@en ;
    rdfs:comment "Indicates the region is nested within the target region"@en ;
    rdfs:comment "Indique que la région est imbriquée dans la région cible"@fr ;
    rdfs:domain mudworld:Region ;
    rdfs:range mudworld:Region .

# reverse relation to subRegionOf
mudworld:hasSubRegion a rdf:Property ;
    rdfs:label "hasSubRegion"@en ;
    rdfs:comment "Indicates the target region is nested within this region"@en ;
    rdfs:comment "Indique que la région cible est imbriquée dans cette région"@fr ;
    rdfs:domain mudworld:Region ;
    rdfs:range mudworld:Region .
```

Using this system we can nest areas of a world with a good level of flexibility:

<img src="{{ '/assets/img/graph/regionMudWorld.png' | absolute_url }}" class="blog-full-image-vertical" alt="A graph showing a top-level region called Galaxy, a child called Planet and indicating that there can be any number of sub-regions down to the base region" />

## Regions and the Open World Assumption

Note that RDF data is modelled with an "Open World Assumption". This essentially means that "just because this is all the data I have _here_, doesn't mean it's all the data that exists". Take for example that on another server, someone may define another Region which is a `subRegionOf` my Galaxy, but I have no idea.

Keeping worlds open is a good idea in scenarios where you want the world to be built on by other sources, e.g. if the region is the 'infinity' of the universe. When we want this, we can use the properties `subRegionOf` and `hasSubRegion` to connect any number of regions that we wish to the object. We can also use this properties, for example, to return to the user the graph of regions that they have discovered.

In other situations, we will want to indicate that the world is closed, e.g. when we want to say "these are all the neighbourhoods that exist in Big City". To achieve this in RDF, we can return the set of sub regions in a **Container**:

```turtle

```

Here is the same graph in JSON-LD:

```json

```
