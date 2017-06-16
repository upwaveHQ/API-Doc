# Comments

Comments are posted onto Cards by users.
A Comment holds a text message and optionally a list of [Attachments](#attachments).

### Mentioning

The content of a Comment may include mentions. If a user is mentioned in a Comment,
that user will receive a notification and will also be added to a [watch list](#cards) for the Card.

Mention type | Format | Description
--------- | ------- | ---- | -----------
User | @{\<USER ID\>} | Mentions the user with id \<USER ID\>
Group | @{board} | Will notify all members on the parent Board

<aside class="notice">To mention a user, enclose the user's ID in curly brackets with a @ in front - like this: "Hi @{657233}, do you need any help on this Task?"</aside>

## List Comments
`GET https://<TEAM DOMAIN>.upwave.io/api/comments/`

```shell
curl "https://<TEAM DOMAIN>.upwave.io/api/comments/"
  -H "Authorization: <API TOKEN>"
```

> The above command returns JSON structured like this:

```json
  {
    "count": 1,
    "next": null,
    "previous": null,
    "results": [
      {
        "id": 10,
        "card": 6,
        "created_dt": "2017-05-18T11:37:55.938664Z",
        "created_by_user": {
          "id": 1,
          "email": "person@example.com",
          "fullname": "John Doe",
          "firstname": "John",
          "avatar": "https://my.profile.image"
        },
        "last_edited_dt": null,
        "last_edited_by_user": null,
        "text": "Hi @{2}, did you see my previous comment?",
        "attachments": [
          {
            "id": 3,
            "comment": 7,
            "card": 6,
            "name": "My site",
            "source": "link",
            "url": "https://example.com",
            "preview_url": null,
            "cover_url": null,
            "file_size": 0,
          }
        ],
        "mentions": [
          {
          "id": 2,
          "email": "person2@example.com",
          "fullname": "Lisa Doe",
          "firstname": "Lisa",
          "avatar": "https://my.profile.image"
        }
        ]
      }
    ]...
}
```

Lists Comments you can access in a paginated fashion.
They are ordered by creation date (created_dt) with the newest Comment listed first.

### Filters

Parameter | Format | Description
--------- | ------- | ---- | -----------
created_by_user | `integer` | Filter Comments on what user created them
card | `integer` | Filter Comments based on their parent Card
q | `querystring` | Search for querystring in Comment text

When filters are combined they will be AND'ed together. For example to list all Comments created by user 74 **and** which contains the word "Thanks",
simply combine the filters like so: `?created_by_user=74&q=Thanks`

## Get a specific Comment
`GET https://<TEAM DOMAIN>.upwave.io/api/comments/<ID>/`

Identical to a Comment in the list-format above.

```shell
curl "https://<TEAM DOMAIN>.upwave.io/api/comments/1/"
  -H "Authorization: <API TOKEN>"
```

> The above command returns JSON structured like this:

```json
  {
    "id": 10,
    "card": 6,
    "created_dt": "2017-05-18T11:37:55.938664Z",
    "created_by_user": {
      "id": 1,
      "email": "person@example.com",
      "fullname": "John Doe",
      "firstname": "John",
      "avatar": "https://my.profile.image",
    },
    "last_edited_dt": null,
    "last_edited_by_user": null,
    "text": "The number is 42!",
    "attachments": [
      {
        "id": 3,
        "comment": 7,
        "card": 6,
        "name": "mysite",
        "source": "link",
        "url": "https://mysite.com",
        "preview_url": null,
        "cover_url": null,
        "file_size": 0,
      }
    ]
  }
```

## Updating a Comment
`POST https://<TEAM DOMAIN>.upwave.io/api/comments/<ID>/`

```shell
curl "https://<TEAM DOMAIN>.upwave.io/api/comments/10/"
  -H "Authorization: <API TOKEN>"
  -X POST
  -d '{
        "text": "43!, my mistake"
      }
```

You are allowed to edit the text in a Comment. Doing so will also update the "last_edited_dt" and "last_edited_by_user".

Argument | Description
-------- | -----------
text | The content of the Comment in plain text format

<aside class="notice">Deleting an attachment in a comment can only be done through the Attachment API</aside>


## Creating a new Comment
`POST https://<TEAM DOMAIN>.upwave.io/api/comments/`

Create new Comments by passing in a text and which Card it should be posted to.
A Comment may also carry Attachments.

```shell
# Creates a new Comment on Card 2
curl "https://<TEAM DOMAIN>.upwave.io/api/comments/"
  -H "Authorization: <API TOKEN>"
  -H "Content-Type: application/json"
  -X POST
  -d '{
        "text": "Well done!",
        "card": 2
      }'

# Creates a new Comment with both text and Attachment on Card 2
curl "https://<TEAM DOMAIN>.upwave.io/api/comments/"
  -H "Authorization: <API TOKEN>"
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
        "card": 2
      }'
```

Currently the public API only support adding URL-Attachments to a Comment.

Argument | Description
-------- | -----------
card* | The parent Card
text | The content of the Comment in plain text format
attachments | A list of Attachments

`* required field`

## Deleting a Comment
`DELETE https://<TEAM DOMAIN>.upwave.io/api/comments/<ID>/`

```shell
# Deletes Comment with id 10
curl "https://<TEAM DOMAIN>.upwave.io/api/comments/10/"
  -X DELETE
  -H "Authorization: <API TOKEN>"
```
If you just direct your eyes slightly to the right, you will see how to delete a Comment
