# Members
Workspace, Team and Board objects, the hierarchical access levels, can have members. A membership describes a users relation to an object using the *role* property.
The *role* property in turn, gives a set of permissions to a user on an object.

## List Members

`GET https://api.upwave.io/workspaces/1337/members/`


```shell
curl "https://api.upwave.io/workspaces/1337/members/"
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
            "id": 263345,
            "email": "coyote@example.com",
            "role": "admin",
            "is_disabled": false,
            "is_active": true,
            "lastname": "Coyote",
            "firstname": "Wile E.",
            "fullname": "Wile E. Coyote",
            "avatar": "https://path/to/image",
            "last_seen": "2019-05-21T11:37:41.870358Z",
            "created_dt": "2019-01-5T18:09:12.332Z"
        }
    ]
}
```

Listing members is always related to an object of type Workspace, Team or Board.


### Listing Team members

Listing members on team with id 482:

`GET https://api.upwave.io/workspaces/1337/teams/482/members/`


### Listing Board members

Listing members on board with id 65323:

`GET https://api.upwave.io/workspaces/1337/boards/65323/members/`


### Filters

Parameter | Format | Description
--------- | ------- | ---- | -----------
disabled | `boolean` | Include or exclude disabled members (only for Workspace members)
role | `string` | Show only members with this role
q | `string` | Search for member (email/name) matching string
page_size | `integer` | Size of result-set per page
