# Boards

An UpWave Board is a surface where Cards live. The Board consist of columns, rows and colors which together forms the structure of the Board.

## List Boards
`GET https://<TEAM DOMAIN>.upwave.io/api/boards/`

```shell
curl "https://<TEAM DOMAIN>.upwave.io/api/boards/"
  -H "Authorization: <API TOKEN>"
```

> The above command returns JSON structured like this:

```json
  {
    "count": 1, 
    "next": None,
    "previous": None, 
    "results": [
      {
        "id": 1,
        "title": "My Awesome UpWave Board",
        "purpose": "This Board just has explanatory purpose",
        "created_dt": "2016-07-13T10:33:20.581Z",
        "created_by_user": {
          "id": 1,
          "email": "person@example.com",
          "fullname": "John Doe",
          "firstname": "John",
          "avatar": "https://my.profile.image",
        },
      {
        "id": 2,
        ..
      },
    ]
  }
```

This endpoint retrieves all the Boards you can access in a paginated fashion.
They are ordered by creation date (created_dt) with the newest Board listed first.

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_columns | `false` | If set to `true`, the result will also include columns for each board.


## Get a Specific Board
`GET https://<TEAM DOMAIN>.upwave.io/api/boards/<ID>/`

```shell
curl "https://<TEAM DOMAIN>.upwave.io/api/boards/1/"
  -H "Authorization: <API TOKEN>"
```

> The above command returns JSON structured like this:

```json
  {
    "id": 1,
    "title": "My Awesome UpWave Board",
    "purpose": "This Board just has explanatory purpose",
    "created_dt": "2016-07-13T10:33:20.581Z",
    "created_by_user": {
      "id": 1,
      "email": "person@example.com",
      "fullname": "John Doe",
      "firstname": "John",
      "avatar": "https://my.profile.image"
    },
    "columns": [
      {
        "state": 1,
        "id": 1,
        "name": "To do"
      },
      {
        "state": 2,
        "id": 2,
        "name": "In progress"
      },
      {
        "state": 3,
        "id": 3,
        "name": "Completed"
      }
    ],
    "rows": [
      {
        "id": 1,
        "name": "Row-1"
      }
    ],
    "colors": [
      {
        "name": "Red",
        "id": 1,
        "hex_color": "#f37477"
      },
      {
        "name": "Yellow",
        "id": 2,
        "hex_color": "#fed562"
      },
      {
        "name": "Green",
        "id": 3,
        "hex_color": "#aed581"
      }
    ]
  }
```

This endpoint retrieves a specific Board.

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_members | `false` | If set to `true`, the result will also include members on the board.

## Note on Board structure

The Board has some characteristics worth pointing out.
The Board structure consists of Colors, Columns and Rows. These 3 dimensions have very different behaviours.

- A Board will always have at least one Column and one Row.
- Whereas a Row has no intrinsic purpose other than for the visual aspect, a Column does.

**Columns** are used for keeping track of Card statuses. The property **state** on a Column is used as a *universal status indicator*.
When a Card is moved to a Column, the card will inherit the status of that Column.

A Column always has one of these states:

Column state | Description
--------- | -----------
0 | Not specified
1 | Not started
2 | In progress
3 | Completed

As a result UpWave can aggregate Card statuses across Boards (more on that in the Cards section.
Also, we have built a triggering system on top of this that you may notice.

Currently there are two triggers in effect on all Boards.

- When a card is ticked off as completed, it will automatically be moved to the left-most Column with state 3 (if found).
- When a card is dragged to a Column with state 3, the card will automatically be ticked off as completed.

<aside class="notice">User actions may on rare occasions trigger update events.</aside>

## Updating a Board
`POST https://<TEAM DOMAIN>.upwave.io/api/boards/<ID>/`

TODO

## Creating a new Board
`POST https://<TEAM DOMAIN>.upwave.io/api/boards/`

TODO

## Deleting a Board
`DELETE https://<TEAM DOMAIN>.upwave.io/api/boards/<ID>/`

```shell
# Deletes Board with id 1
curl "https://<TEAM DOMAIN>.upwave.io/api/boards/1/"
  -X DELETE
  -H "Authorization: <API TOKEN>"
```

Right? Yes, look right to see how to delete a Board.
