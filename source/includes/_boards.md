# Boards

A Board is a container for Cards and will hold some type of structure where the Cards can be positioned.
The structure-types includes; columns, rows, colors and boxes


## View a Board

`GET https://api.upwave.io/workspaces/1337/boards/65323/`

```shell
curl "https://api.upwave.io/workspaces/1337/boards/65323/"
  -H "Authorization: Token 9944b09199c62bcf9418ad846dd0e4bbdfc6ee4b"
```

> The above command returns JSON structured like this:

```json
{
    "id": 65323,
    "title": "Rocket driven hoverboard",
    "purpose": "Development of the new rocket driven hoverboard",
    "background_image_url": "https://path/to/image",
    "background_image_thumb_url": "https://path/to/image",
    "created_dt": "2019-04-13T10:33:20.581Z",
    "rows_enabled": false,
    "plugin_type": "classic",
    "team": {
        "id": 482,
        "title": "R & D",
        "hex_color": "#00796b",
        "hex_text_color": "#ffffff"
    },
    "created_by_user": {
        "id": 263345,
        "email": "coyote@example.com",
        "fullname": "Wile E.",
        "firstname": "Coyote",
        "avatar": "https://path/to/image",
    },
    "columns": [
        {
            "id": 52431,
            "name": "Todo",
            "state": 1
        },
        {
            "id": 52432,
            "name": "In progress",
            "state": 2
        },
        {
            "id": 52433,
            "name": "Completed",
            "state": 3
        },
    ],
    "rows": [
        {
            "id": 23534,
            "name": "Row-1"
        }
    ],
    "colors": [
        {
            "id": 34511,
            "name": "High risk"
        },
        {
            "id": 34512,
            "name": "Low risk"
        }
    ]
}
```


## List Boards

`GET https://api.upwave.io/workspaces/1337/boards/`

```shell
curl "https://api.upwave.io/workspaces/1337/boards/"
  -H "Authorization: Token 9944b09199c62bcf9418ad846dd0e4bbdfc6ee4b"
```

> The above command returns JSON structured like this:

```json
{
    "count": 1,
    "next": null,
    "previous": null,
    "results": [
        {
            "id": 65323,
            "title": "Rocket driven hoverboard",
            "purpose": "Development of the new rocket driven rollerblades",
            "background_image_url": "https://path/to/image",
            "background_image_thumb_url": "https://path/to/image",
            "created_dt": "2019-04-13T10:33:20.581Z",
            "rows_enabled": false,
            "plugin_type": "classic",
            "team": {
                "id": 482,
                "title": "Development",
                "hex_color": "#00796b",
                "hex_text_color": "#ffffff"
            },
            "created_by_user": {
                "id": 263345,
                "email": "coyote@example.com",
                "fullname": "Wile E.",
                "firstname": "Coyote",
                "avatar": "https://path/to/image",
            }
        }
    ]
}
```

This endpoint retrieves all the Boards you can access in a paginated fashion.
They are ordered by creation date (created_dt) with the newest Board listed first.


### Filters

Parameter | Format | Description
--------- | ------- | ---- | -----------
q | `string` | Search for Board title matching string
ordering | `field` | Order result-set by field (default "title")
page_size | `integer` | Size of result-set per page
