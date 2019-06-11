# Members

A Workspace has Workspace-members, a Team has Team-members, a Board has Board-members.

A membership is inherited upwards in the hierarchy. A membership *role* is inherited downwards in the hierarchy.

Examples:

- Adding a membership on a Board (invite), will automatically add membership on the parent Team and Workspace.
- Updating a Workspace member from role "member" to role "admin" will give that user admin privileges on the Workspace and all Teams and Boards within the Workspace.
- Updating a Team member from role "member" to role "admin" will give that user admin privileges on the Team and all Boards within the Team.


## List Members

`GET https://api.upwave.io/workspaces/1337/members/`


```shell
curl "https://api.upwave.io/workspaces/1337/members/"
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
