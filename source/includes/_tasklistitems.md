# TaskListItems

TaskListItems is Upwaves way of handling sub-tasks.

## List TaskListItems

`GET https://api.upwave.io/workspaces/1337/tasklistitems/`

```shell
# List TaskListItems on card 417445
curl "https://api.upwave.io/workspaces/1337/tasklistitems/?card=417445"
  -H "Authorization: Token 9944b09199c62bcf9418ad846dd0e4bbdfc6ee4b"
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
            "due_dt": null,
            "sort_index": 0,
            "card": {
              "id": 611785,
              "title": "Designing the engine"
            },
            "assigned": {
              "id": 263345,
              "email": "coyote@example.com",
              "fullname": "Wile E.",
              "firstname": "Coyote",
              "avatar": "https://path/to/image",
            }
        },
        {
            "id": 3654332,
            "description": "Make purchasing order",
            "finished_dt": "2019-05-18T11:53:41.402858Z",
            "due_dt": "2020-09-17T06:41:57Z",
            "sort_index": 1,
            "card": {
              "id": 611785,
              "title": "Designing the engine"
            },
            "assigned": null
        }
    ]
}
```

This endpoint lists the TaskListItems belonging to the Workspace 1337.

### Filters

Parameter | Format | Description
--------- | ------- | ---- | -----------
finished | `boolean` | Filter TaskListItems on whether they are completed or not
card | `integer` | Filter TaskListItems based on their parent Card
board | `integer` | Filter TaskListItems based on their parent Board
assigned | `integer` | Filter TaskListItems on assigned user being yourself
due_start | `YYYY-MM-DD` | Filter TaskListItems that have due_dt on or after this date
due_end | `YYYY-MM-DD` | Filter TaskListItems that have due_dt on or before this date


## Creating a new TaskListItem

`POST https://api.upwave.io/workspaces/1337/tasklistitems/`

```shell
# Creates a new TaskListItem on Card 417445
curl https://api.upwave.io/workspaces/1337/tasklistitems/
  -H 'Authorization: Token 9944b09199c62bcf9418ad846dd0e4bbdfc6ee4b'
  -H "Content-Type: application/json"
  -X POST
  -d '{"description": "Send item to assembler", "card": 417445}'
```

The new TaskListItem will be sorted last automatically (use update to change it).

Field | Format | Description
--------- | ------- | ---- | -----------
description* | `string` | The description
card* | `integer` | Id of the parent Card
assigned | `integer` | Id of User to assign this TaskListItem
finished | `boolean` | Toggle the completed state
due_dt | `YYYY-MM-DD` | Sets the due_dt
`* required field`


## Updating a TaskListItem

`PATCH https://api.upwave.io/workspaces/1337/tasklistitems/553113/`

```shell
# Updates TaskListItem 553113
curl https://api.upwave.io/workspaces/1337/tasklistitems/553113/
  -H 'Authorization: Token 9944b09199c62bcf9418ad846dd0e4bbdfc6ee4b'
  -H "Content-Type: application/json"
  -X PATCH
  -d '{"finished": true}'
```

> The above command will update the TaskListItem 553113, marking it as completed

Field | Type | Description
-------- | ----------- | --------------
description | `string` | Plain-text description
assigned | `integer` | Id of User to assign this TaskListItem. Pass *null* to remove
finished | `boolean` | Toggle the completed state of a TaskListItem
due_dt | `YYYY-MM-DD` | Updates the due_dt. Pass *null* to remove
sort_before | `integer` | Sorts this TaskListItem before given TaskListItem id. (0 will sort last)


## Deleting a TaskListItem
`DELETE https://api.upwave.io/workspaces/1337/tasklistitems/553113/`

```shell
# Deletes TaskListItem with id 553113
curl "https://api.upwave.io/workspaces/1337/tasklistitems/553113/"
  -X DELETE
  -H "Authorization: Token 9944b09199c62bcf9418ad846dd0e4bbdfc6ee4b"
```
