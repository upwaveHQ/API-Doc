## Updating a Card

`PATCH https://<TEAM DOMAIN>.upwave.io/api/cards/<ID>/`

```shell
# Updates Card 4723
curl https://<TEAM DOMAIN>.upwave.io/api/cards/4723/
  -H 'Authorization: Token <API_TOKEN>'
  -H "Content-Type: application/json"
  -X POST
  -d '{"description": "My new description", "due_dt": "2017-05-10T09:38:06.459119"}'
```

Allowed field | Type | Description
-------- | ----------- | --------------
description | `string` | plain-text or HTML allowed
due_dt | `datetime-iso` | updates the cards due-dt. Pass *null* to remove due-dt
color | `color-id` | updates the color for this card. Pass *null* to remove color
archive | `boolean` | if true the card will be moved to the archive
finished | `boolean` | toggle the completed state of a card
assigned | `id-list` | will assign this card to those user accounts
sort_before | `mixed` | sorts this card before given card id. (0 will sort last)

To update a card you patch in a JSON object with the fields you'd like to update.
For date fields, use UTC.

<aside class="notice">The <strong>title</strong> attribute of a Card cannot be set as it is automatically based on the description fields first line.</aside>
