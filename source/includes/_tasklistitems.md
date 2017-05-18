# TaskListItems

## List TaskListItems

`GET https://<TEAM DOMAIN>.upwave.io/api/tasklistitems/`

```shell
curl "https://<TEAM DOMAIN>.upwave.io/api/tasklistitems/"
  -H "Authorization: <API TOKEN>"
```

> The above command returns JSON structured like this:

```json
  {
    "count": 2,
    "next": null,
    "previous": null,
    "results": [
      {
        "id": 11,
        "description": "Write API documentation for TaskListItem",
        "finished_dt": null,
        "sort_index": 0,
        "card": 1
      },
      {
        "id": 12,
        "description": "Write tests for TaskListItem API",
        "finished_dt": "2017-05-18T11:53:41.402858Z",
        "sort_index": 1,
        "card": 2
      }
    ]
  }
```

This endpoint retrieves all the TaskListItems you can access in a paginated fashion.

A TaskListItem is essentially a subtask and consist of a description, a field determining if its finished or not, and a sort index.

### Query Parameters

Parameter | Format | Description
--------- | ------- | ---- | -----------
finished | `true/false` | Filter TaskListItems on whether they are completed or not
card | `integer` | Filter TaskListItems based on their parent Card

## Creating a new TaskListItem

`POST https://<TEAM DOMAIN>.upwave.io/api/tasklistitems/`

```shell
# Creates a new TaskListItem on Card 2
curl https://<TEAM DOMAIN>.upwave.io/api/tasklistitems/
  -H 'Authorization: Token <API_TOKEN>'
  -H "Content-Type: application/json"
  -X POST
  -d '{"description": "Write tests for Cmment API", "card": 2}'
```

The new TaskListItem will be sorted last automatically (use update to change it).

Argument | Description
-------- | -----------
description* | The description of the TaskListItem
card* | The parent Card

`* required field`

## Updating a TaskListItem

`PATCH https://<TEAM DOMAIN>.upwave.io/api/tasklistitems/<ID>/`

```shell
# Updates TaskListItem 13
curl https://<TEAM DOMAIN>.upwave.io/api/tasklistitems/13/
  -H 'Authorization: Token <API_TOKEN>'
  -H "Content-Type: application/json"
  -X POST
  -d '{"description": "Write tests for Comment API", "finished_dt": "2017-05-10T09:38:06.459119", "sort_before": "12"}'
```

Allowed field | Type | Description
-------- | ----------- | --------------
description | `string` | plain-text
finished | `boolean` | toggle the completed state of a TaskListItem
sort_before | `integer` | sorts this TaskListItem before given TaskListItem id. (0 will sort last)
