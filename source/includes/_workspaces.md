# Workspaces

A Workspace is the highest entity in Upwave.
All data that is not directly tied to a users personal account is stored here.


## View a Workspace

`GET https://api.upwave.io/workspaces/1337/`

```shell
curl "https://api.upwave.io/workspaces/1337/"
  -H "Authorization: Token 9944b09199c62bcf9418ad846dd0e4bbdfc6ee4b"
```

> The above command returns JSON structured like this:

```json
{
    "id": 1,
    "title": "Acme Corporation",
    "logo": "https://path/to/image",
    "access":{
        "can_admin": true,
        "can_modify": true,
        "can_invite": true,
        "can_invite_existing": true
    },
    "logo": "https://path/to/image",
    "features": {
        ...
    }
}
```


## List Workspaces

`GET https://api.upwave.io/workspaces/`

```shell
curl "https://api.upwave.io/workspaces/"
  -H "Authorization: Token 9944b09199c62bcf9418ad846dd0e4bbdfc6ee4b"
```

> The above command returns JSON structured like this:

```json
{
    "count": 1,
    "next": None,
    "previous": None,
    "results": [
        {
            "id": 1337,
            "title": "Acme Corporation",
            "access":{
                "can_admin": true,
                "can_modify": true,
                "can_invite": true,
                "can_invite_existing": true
            },
            "logo": "https://path/to/image",
            "features": {
                ...
            }
        }
    ]
}
```
