# Micropump

**Disclaimer:** Just kidding about 'micropump', not really trying for a frankenspec with with a new name. This is a strawman skeleton document for what the Social (and Federation) API could look like, taking bits from [ActivityPump](http://w3c-social.github.io/activitypump/) and the Indieweb ecosystem (including [Micropub](http://indiewebcamp.com/Micropub) and [SoLiD](http://linkeddata.github.io/SoLiD/) *as they currently stand*; all are subject to ongoing development. [PRs and issues ~~welcome~~ ~~encouraged~~ necessary](http://www.ludumdare.com/compo/wp-content/uploads/2013/04/i-have-no-idea-what-im-doing-dog.jpg).

## Overview

People and the content they create are the core componants of the social web; they make up the social graph. This document describes (eventually) a standard way in which people can:

* create, update and delete social content;
* connect with other people and subscribe to their content;
* interact with other people's content;
* be notified when other people interact with their content;

regardless of what that content is or where it is stored.

This should provide the building blocks for new, interoperable social systems that allow people to express themselves, ideas to be shared, organisations to collaborate, and.. all manner of other exciting things.

## Vocabulary

| ActivityPump | Micropub | SoLiD |
| ------------ | -------- | ----- |
| ActivityStreams 2.0 | Microformats2 | Any suitable RDF ontology (eg. FOAF, SIOC) |

## Syntax

| ActivityPump | Micropub | SoLiD |
| ------------ | -------- | ----- |
| JSON-LD | form-encoded or JSON | RDF (Turtle or JSON-LD) |


## Authorization

* Bearer tokens for authentication
* Leave obtaining the bearer token out of the spec, since there are already several RFCs for ways to obtain bearer tokens.
* ...access control...

### Identity

Not to be over-thought. Terminology:

| ActivityPump | Micropub | SoLiD |
| ------------ | -------- | ----- |
| `Actor` from ActivityStreams2.0 | `author` from microformats2 | `foaf:Agent` maybe? |

Engage debate: relationship between people (personas, no IRL requirement; or orgs or groups or whatever), profiles (documents about people) and accounts.

We are *not* trying to re-standardize identity on the web, but we need to be clear about our core assumptions.

## Publishing

### Exposing content

Publish a feed/stream that others can read (subject to permissions).

| ActivityPump | Indieweb |
| ------------ | -------- |
| JSON at discoverable `outbox` | HTML page marked up with microformats2 (ie. `h-entry`s inside a `h-feed`) |

### Creating content

`POST` to an endpoint that can suitable handle the data.

|              | ActivityPump | Micropub |
| ------------ | --------------------------------------------- | -------- |
| **Endpoint** | discoverable outbox                           | `rel="micropub"` |
| **Data**     | `{`                                           | Form-encoding: |
|              | ` "@type": "Create",`                         | `h=entry&` |
|              | ` "published": "2015-05-15T13:06:00+02:00",`  | `content=hello+moon&` |
|              | ` "actor": "http://rhiaro.co.uk/about#me",`   | `category[]=indieweb&` |
|              | ` "object": {`                                | `category[]=micropub&` |
|              | `    "content": "hello world",`               | `author=http://rhiaro.co.uk/about#me&` |
|              | `    "category": ["indieweb","micropub"]`     | `published=2015-05-15T13:06:00+02:00` |
|              | `  }`                                         | JSON: |
|              | `}`                                           | `{` |
|              |                                               | `  "type": [h-entry],` |
|              |                                               | `  "properties": {` |
|              |                                               | `    "content": ["hello world"],` |
|              |                                               | `    "category": ["indieweb","micropub"]` |
|              |                                               | `  }` |
|              |                                               | `}` |

test trying to figure out codeblocks in table

|   |                |   |   |   |
|---|----------------|---|---|---|
|   | ``` asdf } ``` |   |   |   |
|   |                |   |   |   |
|   |                |   |   |   |


## Subscribing

## Propagating

### Propagating content

### Updating the social graph
