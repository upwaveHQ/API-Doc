# TaskListItems

TaskListItems is Upwaves way of handling sub-tasks.

## List TaskListItems

`GET https://api.upwave.io/workspaces/1337/tasklistitems/?card=417445`

```shell
# List TaskListItems on card 417445
curl "https://api.upwave.io/workspaces/1337/tasklistitems/?card=417445"
  -H "Authorization: 9944b09199c62bcf9418ad846dd0e4bbdfc6ee4b"
```

> The above command returns JSON structured like this:

```json
{
    "count": 2,
    "next": null,
    "previous": null,
    "results": [
        {
            "id": 3654331,
            "description": "Book demo meeting",
            "finished_dt": null,
            "sort_index": 0,
            "card": 417445
        },
        {
            "id": 3654332,
            "description": "Make purchasing order",
            "finished_dt": "2019-05-18T11:53:41.402858Z",
            "sort_index": 1,
            "card": 417445
        }
    ]
}
```

This endpoint retrieves all the TaskListItems belonging to the selected card or board object.

A TaskListItem is essentially a subtask and consist of a description, a field determining if its finished or not, and a sort index.

### Filters

Parameter | Format | Description
--------- | ------- | ---- | -----------
finished | `boolean` | Filter TaskListItems on whether they are completed or not
*card | `integer` | Filter TaskListItems based on their parent Card
*board | `integer` | Filter TaskListItems based on their parent Board

`* You must provide either a card or board to filter on`


## Creating a new TaskListItem

`POST https://api.upwave.io/workspaces/1337/tasklistitems/`

```shell
# Creates a new TaskListItem on Card 417445
curl https://api.upwave.io/workspaces/1337/tasklistitems/
  -H 'Authorization: 9944b09199c62bcf9418ad846dd0e4bbdfc6ee4b'
  -H "Content-Type: application/json"
  -X POST
  -d '{"description": "Send item to assembler", "card": 417445}'
```

The new TaskListItem will be sorted last automatically (use update to change it).

Field | Format | Description
--------- | ------- | ---- | -----------
description* | `string` | The description of the TaskListItem
card* | `integer` | Id of the parent Card

`* required field`


## Updating a TaskListItem

`PATCH https://api.upwave.io/workspaces/1337/tasklistitems/553113/`

```shell
# Updates TaskListItem 553113
curl https://api.upwave.io/workspaces/1337/tasklistitems/553113/
  -H 'Authorization: Token 9944b09199c62bcf9418ad846dd0e4bbdfc6ee4b'
  -H "Content-Type: application/json"
  -X PATCH
  -d '{"description": "finished": true}'
```

> The above command will update the TaskListItem 553113, marking it as completed

Field | Type | Description
-------- | ----------- | --------------
description | `string` | Plain-text description
finished | `boolean` | toggle the completed state of a TaskListItem
sort_before | `integer` | sorts this TaskListItem before given TaskListItem id. (0 will sort last)


## Deleting a TaskListItem
`DELETE https://api.upwave.io/workspaces/1337/tasklistitems/553113/`

```shell
# Deletes TaskListItem with id 553113
curl "https://api.upwave.io/workspaces/1337/tasklistitems/553113/"
  -X DELETE
  -H "Authorization: 9944b09199c62bcf9418ad846dd0e4bbdfc6ee4b"
```
