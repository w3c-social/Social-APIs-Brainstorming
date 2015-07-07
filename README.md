# W3C Social Web WG Brainstorming

This repo is a collection of resources related to ongoing development of Social and Federation API specificaitons, according to the [SocialWG charter](http://www.w3.org/2013/socialweb/social-wg-charter).

## Table of contents

* [Brainstorming: comparison of Micropub, ActivityPump and SoLiD](#brainstorming) (this document).
* [Social API draft](https://github.com/rhiaro/Social-APIs-Brainstorming/blob/master/socialapi.md)

# Brainstorming

## Common Ground

### Bearer tokens
* Bearer tokens for authentication
* Leave obtaining the bearer token out of the spec, since there are already several RFCs for ways to obtain bearer tokens

## Issues

* Vocabulary - `h-entry` and `h-card` vs ActivityStreams 2.0 vocab


## Micropub

### Things ActivityPump does that Micropub wants
* Audience targeting for private content ("to")
* Propagating state changes (e.g. an "update" of an object needs to propagate to consumers)
* Collections - managing the "following" collection vs the "posts" collection

### Ideas
* Generating "activity" posts after manipulating content posts


### Example of a Micropub request posted as JSON

Creating a post (implied action:create because no URL is given)
```json
{
  "object": {
    "content": "hello moon",
    "category": ["indieweb"]
  }
}
```

Updating a post (implied action:update)

```json
{
  "url": "http://example.com/post/1",
  "object": {
    "content": "hello moon"
  }
}
```

Adding a value to an array (implied action:update)

```json
{
  "url": "http://example.com/post/1",
  "add": {
    "category": ["indieweb"]
  }
}
```

Removing a value from an array (implied action:update)

```json
{
  "url": "http://example.com/post/1",
  "remove": {
    "category": ["indieweb"]
  }
}
```

Removing a value (or an array) (implied action:update)

```json
{
  "url": "http://example.com/post/1",
  "remove": ["category"]
}
```

Deleting a post:

```json
{
  "url": "http://example.com/post/1",
  "action": "delete"
}
```

## ActivityPump

### Things that Micropub does that ActivityPump wants


### Minimum viable create request
What does a minimum create post look like, with as many values implied as possible.


## Notes
* In ActivityPump, following someone results in seeing everything they post directed to their followers
* "quiet posting" in AP doesn't exist, e.g. you can't make something public and *not* have it pushed to everyone

