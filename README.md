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


## Things that Micropub does that ActivityPump wants


## Notes
* In ActivityPump, following someone results in seeing everything they post directed to their followers
* "quiet posting" in AP doesn't exist, e.g. you can't make something public and *not* have it pushed to everyone

