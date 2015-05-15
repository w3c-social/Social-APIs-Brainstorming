# Social APIs Brainstorming

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

- Ability to get source of post (e.g. original markdown posted in)
- Uploading multiple files
- Split up specification into more manageable chunks and not be one huge daunting spec

### Minimum viable create request

The minimum allowed in the spec is:
```json
{
    "@Type": "Post",
    "object": {
        "content": "Hello world!",
        "@Type": "Note"
    }
}
```

If we had it so that an activity could be created as a side effect:
```json
{
    "content": "Hello world!",
    "@Type": "Note"
}
```
This as a side-effect would not only create the note but also create an
activity.

## Notes
* In ActivityPump, following someone results in seeing everything they post directed to their followers
* "quiet posting" in AP doesn't exist, e.g. you can't make something public and *not* have it pushed to everyone- 

