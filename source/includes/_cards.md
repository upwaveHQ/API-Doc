# Cards

## List Cards

`GET https://<TEAM DOMAIN>.upwave.io/api/cards/`

```shell
curl "https://<TEAM DOMAIN>.upwave.io/api/cards/"
  -H "Authorization: <API TOKEN>"
```

> The above command returns JSON structured like this:

```json
  {
    "count": 7, 
    "next": "https://<TEAM DOMAIN>.upwave.io/api/cards/?page=2",
    "previous": None, 
    "results": [
      {
        "id": 4723,
        "title": "A Card",
        "description": "<h1>A Card</h1><p>More text in a paragraph.</p>",
        "color": null,
        "created_dt": "2016-07-13T10:33:26.645Z",
        "created_by_user": {
          "id": 2,
          "email": "person2@example.com",
          "fullname": "Lisa Doe",
          "firstname": "Lisa",
          "avatar": "https://my.profile.image"
        },
        "finished_dt": "2016-08-04T08:53:24.921Z",
        "due_dt": null,
        "assigned": [
          {
            "id": 1,
            "email": "person1@example.com",
            "fullname": "John Doe",
            "firstname": "John",
            "avatar": "https://my.profile.image"
          },
          {
            "id": 2,
            "email": "person2@example.com",
            "fullname": "Lisa Doe",
            "firstname": "Lisa",
            "avatar": "https://my.profile.image"
          },
        ]
      },
      ..
    ]
  }
```

This endpoint retrieves all the Cards you can access in a paginated fashion.

### Query Parameters

Parameter | Format | Description
--------- | ------- | ---- | -----------
start_dt | `YYYY-MM-DD` | Filter Cards that has due_dt on or after this date
end_dt | `YYYY-MM-DD` | Filter Cards that has due_dt on or before this date
finished | `true/false` | Filter Cards on whether they are completed or not
state | `integer` | Filter Cards based on their column state
board | `integer` | Filter Cards based on their parent Board
assigned | `1,2,3` | Filter Cards based on who are assigned

The `assigned` parameter supports comma separated list which will be OR'ed.
For example, to filter Cards that are assigned to either of user-account 1 or 2 you can pass in:
`?assigned=1,2`

Date arguments `start_dt` and `end_dt` are given on the format `YYYY-MM-DD`.

## Get a Specific Card
`GET https://<TEAM DOMAIN>.upwave.io/api/cards/<ID>`

```shell
curl "https://<TEAM DOMAIN>.upwave.io/api/cards/4723"
  -H "Authorization: <API TOKEN>"
```

> The above command returns JSON structured like this:

```json
  {
    "id": 4723,
    "title": "A Card",
    "description": "<h1>A Card</h1><p>More text in a paragraph.</p>",
    "color": null,
    "created_dt": "2016-07-13T10:33:26.645Z",
    "created_by_user": {
      "id": 2,
      "email": "person2@example.com",
      "fullname": "Lisa Doe",
      "firstname": "Lisa",
      "avatar": "https://my.profile.image"
    },
    "finished_dt": "2016-08-04T08:53:24.921Z",
    "due_dt": null,
    "assigned": [
      {
        "id": 1,
        "email": "person1@example.com",
        "fullname": "John Doe",
        "firstname": "John",
        "avatar": "https://my.profile.image"
      },
      {
        "id": 2,
        "email": "person2@example.com",
        "fullname": "Lisa Doe",
        "firstname": "Lisa",
        "avatar": "https://my.profile.image"
      },
    ],
    "tasklist": [
      {
        "id": 1,
        "text": "Subtask 1",
        "finished_dt": null
      },
      {
        "id": 2,
        "text": "Subtask 2",
        "finished_dt": null
      }
    ],
    "comments": [
      {
        "id": 1,
        "created_dt": "2016-07-13T11:14:28.581Z",
        "text": "This is a comment on the card and it has some attachments too",
        "attachments": [
          {
            "id": 1,
            "name": "Beautiful image",
            "url": "www.some.url/image.png",
            "preview_url": "www.some.url/preview_image.png",
            "mime_type": "image/png",
            "file_size": 0
          }
        ]
      }
    ]
  }
```
