# Comments

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
        "card": 7,
        "created_dt": "2017-05-18T11:37:55.938664Z",
        "created_by_user": {
          "id": 1,
          "email": "person@example.com",
          "fullname": "John Doe",
          "firstname": "John",
          "avatar": "https://my.profile.image",
          "timezone": "UTC",
          "language_code": "en",
          "first_day": 1
        },
        "last_edited_dt": null,
        "last_edited_by_user": null,
        "text": "The number is 42!",
        "attachments": []
      }
    ]...
}
```

This endpoint retrieves all the Comments you can access in a paginated fashion.
They are ordered by creation date (created_dt) with the newest Comment listed first.

A Comment is a text message attached to a Card. 
The Comment may also carry attachments such as uploaded files or references to web resources [(see Attachments)](#attachments)

Parameter | Format | Description
--------- | ------- | ---- | -----------
created_by_user | `integer` | Filter Comments on what user created them
card | `integer` | Filter Comments based on their parent Card
