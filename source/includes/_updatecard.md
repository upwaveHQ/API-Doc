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
description | `string` | Plain-text or HTML allowed
due_dt | `YYYY-MM-DD` | Updates the cards due_dt. Pass *null* to remove due_dt
color | `color-id` | Updates the color for this Card. Pass *null* to remove color
archive | `boolean` | If true the Card will be moved to the archive
finished | `boolean` | Toggle the completed state of a Card
assigned | `id-list` | Will assign this Card to those user accounts
sort_before | `integer` | Sorts this Card before given Card id (0 will sort last)
watch | `boolean` | Watch/Unwatch youself for commment notifications on this Card

To update a Card you patch in a JSON object with the fields you'd like to update.
For date fields, use UTC.

<aside class="notice">The <strong>title</strong> field on a Card is automatically determined based on the first line of the description.</aside>


### Watching a Card

When watching a Card a User will be subscribed to notifications for that Card.
There are multiple ways to subscribe:

1. click the "Watch card" function in the UI
2. update the Card via API with *{"watch": true}*
1. create a Card and you are automatically subscribed
2. create a Comment and you are automatically subscribed
3. edit a Comment and you are automatically subscribed
4. mentioning someone in a Comment will subscribe them
5. assigning someone to a Card will subscribe them
6. assigning someone to a TaskListItem will subscribe them

The only way to unwatch a Card is to update the Card with *{"watch": false}* or use the UI function"Unwatch card".
