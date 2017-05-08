## Creating a new Card

`POST https://<TEAM DOMAIN>.upwave.io/api/cards/`

```shell
# Creates a new Card on Board 311
curl https://<TEAM DOMAIN>.upwave.io/api/cards/
  -H 'Authorization: Token <API_TOKEN>'
  -H "Content-Type: application/json"
  -X POST
  -d '{"description": "A new card", "board": 311}'
```

Argument | Description
-------- | -----------
description* | The content of the Card. May be HTML formatted
board* | The parent Board
color | Will set the Color of this card
due_dt | Will set the due_dt of this card
column | Will position the card in this Column (defaults to left-most Column with state 1 if exists else left-most Column)
row | Will position the card in this Row (defaults to first Row)


`* required field`

<aside class="notice">The <strong>title</strong> attribute of a Card cannot be set as it is automatically based on the description fields first line.</aside>
