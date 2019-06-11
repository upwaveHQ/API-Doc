## Creating a new Card

`POST https://api.upwave.io/workspace/1337/cards/`

```shell
# Creates a new Card on Board 65323
curl https://api.upwave.io/workspace/1337/cards/
  -H 'Authorization: Token 9944b09199c62bcf9418ad846dd0e4bbdfc6ee4b'
  -H "Content-Type: application/json"
  -X POST
  -d '{"description": "<h1>Order titanium rims</h1>", "board": 65323}'
```

The new Card will be inserted last in the first column with state 1 (use update to change it).
If no column with state 1 is found, it will be inserted in the first column.

Field | Format | Description
--------- | ------- | ---- | -----------
description* | `string` | The content of the Card. May be HTML formatted
board* | `integer` | The id of the parent Board
color | `integer` | The id of the Color
due_dt | `YYYY-MM-DD` | Will set the due_dt of this card
column | `integer` | Will position the card in this Column (defaults to left-most Column with state 1 if exists else left-most Column)
row | `integer` | Will position the card in this Row (defaults to first Row)


`* required field`


## Deleting a Card
`DELETE https://api.upwave.io/workspace/1337/cards/611798/`

```shell
# Deletes Card with id 611798
curl "https://api.upwave.io/workspace/1337/cards/611798/"
  -X DELETE
  -H "Authorization: 9944b09199c62bcf9418ad846dd0e4bbdfc6ee4b"
```
