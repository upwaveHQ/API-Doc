## Updating a Card

`PATCH https://api.upwave.io/workspaces/1337/cards/611785/`

```shell
# Updates Card 611785
curl https://api.upwave.io/workspaces/1337/cards/611785/
  -H 'Authorization: Token 9944b09199c62bcf9418ad846dd0e4bbdfc6ee4b'
  -H "Content-Type: application/json"
  -X PATCH
  -d '{"finished": null}'
```

> The above command will uncomplete card 611785

Field | Format | Description
-------- | ----------- | --------------
description | `string` | plain-text or HTML allowed
due_dt | `YYYY-MM-DD` | updates the cards due-dt. Pass *null* to remove due-dt
color | `color-id` | updates the color for this Card. Pass *null* to remove color
archive | `boolean` | if true the Card will be moved to the archive
finished | `boolean` | toggle the completed state of a Card
assigned | `id-list` | will assign this Card to those user accounts
sort_before | `integer` | sorts this Card before given Card id (0 will sort last)
watch | `boolean` | Watch/Unwatch youself for commment notifications on this Card

To update a Card you patch in a JSON object with the fields you'd like to update.
For date fields, use UTC.

<aside class="notice">The <strong>title</strong> field on a Card is automatically determined based on the first line of the description.</aside>


### Watching a Card

A User, when on a watch list to a Card, will be notified on important changes on that Card.
A User will automatically be added to the watch list when..

1. the user is assigned a Card,
2. the user is mentioned in a Comment on a Card
3. the user choose to watch the Card

The only way to unwatch a Card is to update the Card with *{"watch": false}*
This is also the mechanism for how to manually add oneselves to the watch list.
