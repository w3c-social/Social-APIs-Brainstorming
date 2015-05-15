# Social APIs Brainstorming

## Common Ground

### Bearer tokens
* Bearer tokens for authentication
* Leave obtaining the bearer token out of the spec, since there are already several RFCs for ways to obtain bearer tokens

## Things ActivityPump does that Micropub wants
* Audience targeting for private content ("to")
* Propagating state changes (e.g. an "update" of an object needs to propagate to consumers)
* Collections - managing the "following" collection vs the "posts" collection

### Example of a Micropub request posted as JSON

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


## Things that Micropub does that ActivityPump wants


## Notes
* In ActivityPump, following someone results in seeing everything they post directed to their followers
* "quiet posting" in AP doesn't exist, e.g. you can't make something public and *not* have it pushed to everyone

