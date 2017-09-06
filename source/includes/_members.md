# Members

A Team has Team Members, a Board has Board Members. A Member is a user account tied to an entity such as Team or Board.

## List Team Members
`GET https://<TEAM DOMAIN>.upwave.io/api/members/`

```shell
curl "https://<TEAM DOMAIN>.upwave.io/api/members/"
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
        "id": 1,
        "email": "person@example.com",
        "fullname": "John Doe",
        "firstname": "John",
        "avatar": "https://my.profile.image"
      }
    ]
  }
```

### Arguments

Parameter | Format | Description
--------- | ------- | -----------
board | `integer` | Lists only members that have direct access to the given Board
ordering | "created"/"seen" | Order result list
page_size | `integer` | Size of result-set per page
