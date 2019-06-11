# Comments

Comments are posted onto Cards by users.
A Comment holds a text message and optionally a list of [Attachments](#attachments).


### Mentioning

The content of a Comment may include mentions. If a user is mentioned in a Comment,
that user will receive a notification and will also be added to the [watch list](#cards) for the Card.

Mention type | Format | Description
--------- | ------- | ---- | -----------
User | @{263346} | Mentions the user with id 263346
Group | @{board} | Will notify all members on the parent Board

<aside class="notice">Example comment text: "Hi @{263346}, do you need any help on this task?"</aside>


## View a Comment

`GET https://api.upwave.io/workspaces/1337/comments/687137/`

```shell
# View comment with id 687137
curl "https://api.upwave.io/workspaces/1337/comments/687137/"
  -H "Authorization: 9944b09199c62bcf9418ad846dd0e4bbdfc6ee4b"
```

> The above command returns JSON structured like this:

```json
{
    "id": 687137,
    "card": 611785,
    "text": "Hi @{263346}, do you need any help on this task?",
    "last_edited_dt": null,
    "last_edited_by_user": null,
    "created_dt": "2019-05-18T11:37:55.938664Z",
    "created_by_user": {
        "id": 263345,
        "email": "coyote@example.com",
        "fullname": "Wile E.",
        "firstname": "Coyote",
        "avatar": "https://path/to/image",
    },
    "attachments": [
        {
            "id": 2529,
            "comment": 687137,
            "card": 611785,
            "name": "Thorim Engine Specs",
            "source": "link",
            "url": "https://path/to/resource",
            "preview_url": null,
            "cover_url": null,
            "file_size": 0,
        }
    ],
    "mentions": [
        {
            "id": 263346,
            "email": "rascal@example.com",
            "fullname": "Rascal",
            "firstname": "Coyote",
            "avatar": "https://path/to/image"
        }
    ]
}
```


## List Comments

`GET https://api.upwave.io/workspaces/1337/comments/?card=611785`

```shell
# List Comments on card with id 611785
curl "https://api.upwave.io/workspaces/1337/comments/?card=611785"
  -H "Authorization: 9944b09199c62bcf9418ad846dd0e4bbdfc6ee4b"
```

> The above command returns JSON structured like this:

```json
  {
    "count": 1,
    "next": null,
    "previous": null,
    "results": [
        {
            "id": 687137,
            "card": 611785,
            "text": "Hi @{263346}, do you need any help on this task?",
            "last_edited_dt": null,
            "last_edited_by_user": null,
            "created_dt": "2019-05-18T11:37:55.938664Z",
            "created_by_user": {
                "id": 263345,
                "email": "coyote@example.com",
                "fullname": "Wile E.",
                "firstname": "Coyote",
                "avatar": "https://path/to/image",
            },
            "attachments": [
                {
                    "id": 2529,
                    "comment": 687137,
                    "card": 611785,
                    "name": "Thorim Engine Specs",
                    "source": "link",
                    "url": "https://path/to/resource",
                    "preview_url": null,
                    "cover_url": null,
                    "file_size": 0,
                }
            ],
            "mentions": [
                {
                    "id": 263346,
                    "email": "rascal@example.com",
                    "fullname": "Rascal",
                    "firstname": "Coyote",
                    "avatar": "https://path/to/image"
                }
            ]
        }
    ]
}
```

Lists Comments you can access in a paginated fashion.
They are ordered by creation date (created_dt) with the newest Comment listed first.


### Filters

Parameter | Format | Description
--------- | ------- | ---- | -----------
created_by_user | `integer` | Filter Comments on what user created them
card | `integer` | Filter Comments based on their parent Card
q | `string` | Search for string in Comment text

When filters are combined they will be AND'ed together.
For example to list all Comments created by user 263345 **and** which contains the word "specs",
simply combine the filters like so: `?created_by_user=263345&q=specs`


## Updating a Comment

`PATCH https://api.upwave.io/workspaces/1337/comments/687137/`

```shell
# Update Comment with id 687137
curl "https://api.upwave.io/workspaces/1337/comments/687137/"
  -H "Authorization: Token 9944b09199c62bcf9418ad846dd0e4bbdfc6ee4b"
  -X PATCH
  -d '{"text": "..."}'
```

You are allowed to edit the text in a Comment. Doing so will also update the "last_edited_dt" and "last_edited_by_user".

Field | format | Description
--------- | ------- | ---- | -----------
text | `string` | The content of the Comment in plain text format

<aside class="notice">Deleting an attachment in a comment can only be done through the Attachment API</aside>


## Creating a new Comment

`POST https://api.upwave.io/workspaces/1337/comments/`

Create new Comments by passing in a text and which Card it should be attached to.
A Comment may also carry Attachments.

```shell
# Creates a new Comment on Card with id 611785
curl "https://api.upwave.io/workspaces/1337/comments/"
  -H "Authorization: Token 9944b09199c62bcf9418ad846dd0e4bbdfc6ee4b"
  -H "Content-Type: application/json"
  -X POST
  -d '{
        "text": "Well done!",
        "card": 611785
      }'

# Creates a new Comment with both text and Attachment on Card with id 611785
curl "https://api.upwave.io/workspaces/1337/comments/"
  -H "Authorization: Token 9944b09199c62bcf9418ad846dd0e4bbdfc6ee4b"
  -H "Content-Type: application/json"
  -X POST
  -d '{
        "text": "See attached url",
        "attachments": [
          {
            "url": "https://example.com",
            "name": "Example"
          }
        ]
        "card": 611785
      }'
```

Currently the public API only support adding URL-Attachments to a Comment.
To make the URL appear as a clickable image, you may set the "preview_url" attribute pointing to an image of your choice.
The image URL needs to be behind HTTPS protocol and the image should be 200x200 pixels in size.

Argument | Description
-------- | -----------
card* | The parent Card
text | The content of the Comment in plain text format
attachments | A list of Attachments

`* required field`

## Deleting a Comment
`DELETE https://api.upwave.io/workspaces/1337/comments/446119/`

```shell
# Deletes Comment with id 10
curl "https://api.upwave.io/workspaces/1337/comments/446119/"
  -X DELETE
  -H "Authorization: Authorization: Token 9944b09199c62bcf9418ad846dd0e4bbdfc6ee4b"
```
