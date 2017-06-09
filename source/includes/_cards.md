# Cards

UpWave Cards is an information carrier that holds task-description, comments, files etc.

### Subscription

A User, when subscribed to a card, will be notified on important changes on that Card.
A Subscription will start when
a) a user is assigned a Card,
b) a user is mentioned in a Comment on a Card
c) a user choose to Subscribe to a Card

The only way to terminate a subscription is to update the card with *{"subscribe": false}*
This is also the mechanism for how to manually subscribe to a Card.

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
They are ordered by creation date (created_dt) with the newest Card listed first.

### Filters

Parameter | Format | Description
--------- | ------- | ---- | -----------
created_by_user | `integer` | Filter Cards on what user created them
start_dt | `YYYY-MM-DD` | Filter Cards that has due_dt on or after this date
end_dt | `YYYY-MM-DD` | Filter Cards that has due_dt on or before this date
finished | `true/false` | Filter Cards on whether they are completed or not
state | `integer` | Filter Cards based on their column state
board | `integer` | Filter Cards based on their parent Board
assigned | `1,2,3` | Filter Cards based on who are assigned
q | `querystring` | Search for querystring in Card title and description

The `assigned` parameter supports comma separated list which will be OR'ed.
For example, to filter Cards that are assigned to either of user-account 1 or 2 you can pass in:
`?assigned=1,2`

Date arguments `start_dt` and `end_dt` are given on the format `YYYY-MM-DD`.

When filters are combined they will be AND'ed together. For example to list all Cards that are finished **and** which contains the word "Oslo",
simply combine the filters like so: `?finished=true&q=Oslo`

## Get a Specific Card

`GET https://<TEAM DOMAIN>.upwave.io/api/cards/<ID>/`

This endpoint retrieves a specific Card.

```shell
curl "https://<TEAM DOMAIN>.upwave.io/api/cards/4723/"
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
    "subscribed": true
  }
```

In order to fetch additional data belonging to a Card, such as Comments, Attachments, TaskListItems,
use the appropriate API with a card-filter. Example: *api/comments/?card=\<CARD ID\>*
