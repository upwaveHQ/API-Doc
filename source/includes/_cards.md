# Cards

Upwave Cards are information carriers that can hold a description, comments, files and more.


## View a Card

`GET https://api.upwave.io/workspaces/1337/cards/611785/`

This endpoint retrieves a specific Card.

```shell
# View card with id 611785
curl "https://api.upwave.io/workspaces/1337/cards/611785/"
  -H "Authorization: Token 9944b09199c62bcf9418ad846dd0e4bbdfc6ee4b"
```

The `cardlocation` block will differ depending on what kind of Board we are dealing with (plugin_type `classic` vs. plugin_type `canvas`).
For "classic" boards, the cardlocation will hold column/row information. For "canvas" boards, the cardlocation will hold container information and offset values.

> The above command returns JSON structured like this:

```json
{
    "id": 611785,
    "title": "Designing the engine",
    "description": "<h1>Designing the engine</h1><p>Since the engine will run on Thorium, we need to ...</p>",
    "cover_image_url": "https://path/to/image",
    "state": 1,
    "created_by_user": 263345,
    "created_dt": "2019-03-18T14:13:44.921Z",
    "finished_by_user": 263345,
    "finished_dt": "2019-05-04T08:53:24.921Z",
    "due_dt": "2019-05-05T12:00:00.921Z",
    "archived_dt": null,
    "watched": true,
    "num_comments": 2,
    "num_attachments": 1,
    "board": {
        "id": 65323,
        "title": "Rocket driven hoverboard"
    }
    "progress": {
        "completed": 0,
        "total": 0
    },
    "color": {
        "id": 52778,
        "name": "High risk",
        "hex_color": "#f080a2"
    },
    "assigned": [
        {
            "id": 263345,
            "email": "coyote@example.com",
            "fullname": "Wile E.",
            "firstname": "Coyote",
            "avatar": "https://path/to/image",
        }
    ],
    "cardlocation": {
        "column": {
            "id": 52433,
            "name": "Completed"
        },
        "row": {
            "id": 23534,
            "name": "Row-1"
        }
    }
}
```


## List Cards

`GET https://api.upwave.io/workspaces/1337/cards/`

```shell
curl "https://api.upwave.io/workspaces/1337/cards/"
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
            "id": 611785,
            "title": "Designing the engine",
            "description": "<h1>Designing the engine</h1><p>Since the engine will run on Thorium, we need to ...</p>",
            "cover_image_url": "https://path/to/image",
            "state": 3,
            "created_by_user": 263345,
            "created_dt": "2019-03-18T14:13:44.921Z",
            "finished_by_user": 263345,
            "finished_dt": "2019-05-04T08:53:24.921Z",
            "due_dt": "2019-05-05T12:00:00.921Z",
            "archived_dt": null,
            "watched": true,
            "num_comments": 2,
            "num_attachments": 1,
            "board": {
                "id": 65323,
                "title": "Rocket driven hoverboard"
            }
            "progress": {
                "completed": 0,
                "total": 0
            },
            "color": {
                "id": 52778,
                "name": "High risk",
                "hex_color": "#f080a2"
            },
            "access":{
                "can_admin": true,
                "can_modify": true,
                "can_invite": true,
                "can_invite_existing": true
            }
            "assigned": [
                {
                    "id": 263345,
                    "email": "coyote@example.com",
                    "fullname": "Wile E.",
                    "firstname": "Coyote",
                    "avatar": "https://path/to/image",
                }
            ]
        }
    ]
}
```

This endpoint retrieves all the Cards you can access in a paginated fashion.
They are ordered by creation date (created_dt) with the newest Card listed first.

### Filters

Parameter | Format | Description
--------- | ------- | ---- | -----------
created_by_user | `integer` | Filter Cards on what user created them
created_start | `YYYY-MM-DD` | Filter Cards that were created on or after this date
created_end | `YYYY-MM-DD` | Filter Cards that were created on or before this date
due_start | `YYYY-MM-DD` | Filter Cards that have due_dt on or after this date
due_end | `YYYY-MM-DD` | Filter Cards that have due_dt on or before this date
finished_start | `YYYY-MM-DD` | Filter Cards that were completed on or after this date
finished_end | `YYYY-MM-DD` | Filter Cards that were completed on or before this date
finished | `boolean` | Filter Cards on whether they are completed or not
state | `integer` | Filter Cards based on their column state
board | `integer` | Filter Cards based on their parent Board
assigned | `1,2,3` | Filter Cards based on who are assigned
q | `string` | Search for string in Card title and description
ordering | `field` | Order result-set by field (default "-created")
page_size | `integer` | Size of result-set per page

The `assigned` parameter supports comma separated list which will be OR'ed.
For example, to filter Cards that are assigned to either of user-account 1 or 2 you can pass in:
`?assigned=1,2`

The ordering parameter will order the result-set on the field given. Acceptable fields are:
"created", "finished", "due". To specify a descending ordering direction set a minus in front e.g. `?ordering=-created`

When filters are combined they will be AND'ed together. For example to list all Cards that were
completed in month May 2019, combine filters like so: `?finished_start=2019-05-1&finished_end=2019-05-31`
