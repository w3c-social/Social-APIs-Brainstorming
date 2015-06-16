# Social APIs Brainstorming

## Common Ground

### Bearer tokens
* Bearer tokens for authentication
* Leave obtaining the bearer token out of the spec, since there are already several RFCs for ways to obtain bearer tokens

### Endpoints

Similar but different:

|              | Publish content | Receive content/notifications |
| ------------ | ------- | ------- |
| ActivityPump | post to /outbox | get from /inbox |
| Micropub     | discover micropub endpoint (rel="micropub") and post to it | receive webmention at discoverable rel="webmention" endpoint; how to handle not spec'd |

## Issues

* Vocabulary - `h-entry` and `h-card` vs ActivityStreams 2.0 content types
* `author` in microformats vs `actor` and `attributedTo` in AS
* `url` and `uid` in microformats vs `url`, `@id` and `href` in AS

## Micropub

### Things ActivityPump does that Micropub wants
* Audience targeting for private content ("to")
* Propagating state changes (e.g. an "update" of an object needs to propagate to consumers)
* Collections - managing the "following" collection vs the "posts" collection

### Ideas
* Generating "activity" posts after manipulating content posts
* Or attaching all metadata to the 'object' and sending pure objects (that [still look like activities](http://rhiaro.co.uk/2015/05/micropubbing-with)) for publishing and distribution as JSON.

### Example of Micropub requests posted as JSON

** Expansion upon these at [http://rhiaro.co.uk/2015/05/micropubbing-with](http://rhiaro.co.uk/2015/05/micropubbing-with) **

#### Creating a Post

Creating a post, specifying properties from the microformats2 vocab. The type and properties map to the output of the [Microformats 2 parsed result](http://microformats.org/wiki/microformats2-parsing).

Form-encoded requests have a property `h=*` which specifies the type of object being created. All other properties are considered properties of the object being created.

```
h=entry&
content=hello+moon&
category[]=indieweb&
category[]=micropub
```

When submitting a request in JSON format, simply send the JSON-encoded representation of the Microformats2 object you are creating. Properties such as author and publish date are set by the Micropub endpoint if not specified in the request.

```json
{
  "type": ["h-entry"],
  "properties": {
    "content": ["hello moon"],
    "category": ["indieweb","micropub"]
  }
}
```

#### Editing a post

Because of the nuances of modifying specific values in properties, these requests do not have a "simple" form-encoded representation, and must use nested properties with array notation. These form-encoded requests are the same structure as the JSON version, but serialized as form-encoded instead.

##### Replacing all values of a property

Updating a specific property of a post, replacing all values of the property. If the property does not exist already, it is created.

```
edit-of=http://example.com/post/1
&update[properties][content]=hello+moon
```

```json
{
  "edit-of": "http://example.com/post/1",
  "update": {
    "properties": {
      "content": ["hello moon"]
    }
  }
}
```

##### Adding a value to a property

Adding a value. If there are any existing values for this property, they are not changed, the new values are added. If the property does not exist already, it is created.

```
edit-of=http://example.com/post/1
&add[properties][category][]=indieweb
&add[properties][category][]=foo
```

```json
{
  "edit-of": "http://example.com/post/1",
  "add": {
    "properties": {
      "category": ["indieweb","foo"]
    }
  }
}
```

##### Removing a value from a property

Removing a value. This removes just the "indieweb" value from the "category" property, leaving all other values. If no values remain, the property is removed.

```
edit-of=http://example.com/post/1
&remove[properties][category]=indieweb
```

```json
{
  "edit-of": "http://example.com/post/1",
  "delete": {
    "properties": {
      "category": ["indieweb"]
    }
  }
}
```

##### Removing a property

```
edit-of=http://example.com/post/1
&remove[properties]=indieweb
```

```json
{
  "edit-of": "http://example.com/post/1",
  "delete": {
    "properties": ["category"]
  }
}
```

#### Deleting a post

```
delete-of=http://example.com/post/1
```

```json
{
  "delete-of": "http://example.com/post/1"
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
    "@context": "http://www.w3.org/ns/activitystreams",
    "@type": "Post",
    "object": {
        "@type": "Note",
        "content": "Hello world!"
    }
}
```

If we had it so that an activity could be created as a side effect:
```json
{
    "@context": "http://www.w3.org/ns/activitystreams",
    "@type": "Note",
    "content": "Hello world!"
}
```
This as a side-effect would not only create the note but also create an
activity.

## Notes
* In ActivityPump, following someone results in seeing everything they post directed to their followers
* "quiet posting" in AP doesn't exist, e.g. you can't make something public and *not* have it pushed to everyone- 

