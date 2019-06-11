# Attachments

Attachments may accompany a Comment. An attachment can be either an uploaded file, a web page resource or a cloud hosted file.

Source | Description
--------- | ------- | ---- | -----------
uploadedfile | Indicates that the file was uploaded
link | Indicates that the attachment is a web page or web resource
gdrive | Indicates that the file is a Google Drive file
dropbox | Indicates that the file is a Dropbox file
onedrive | Indicates that the file is a Microsoft OneDrive file


## List Attachments

`GET https://api.upwave.io/workspaces/1337/attachments/?card=611785`

```shell
curl "https://api.upwave.io/workspaces/1337/attachments/?card=611785"
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
        "id": 265422,
        "comment": 446119,
        "card": 611785,
        "name": "Example",
        "source": "link",
        "url": "https://example.com",
        "preview_url": null,
        "cover_url": null,
        "file_size": 0,
      },
    ]
  }
```

Filtering options:

Parameter | Format | Description
--------- | ------- | ---- | -----------
source | `string` | Filter Attachments on source (see table above)
*comment | `integer` | Filter Attachments on their parent Comment
*card | `integer` | Filter Attachment based on their parent Card
*board | `integer` | Filter Attachment based on their parent Board

`* You must provide either a comment, card or board to filter on`

File sizes will only be listed for files that are either uploaded directly (source is "uploadedfile") or for Google Drive files that has a file size.

<aside class="warning">Attachments can only be created using the Comment api</aside>

## Deleting an Attachment
`DELETE https://api.upwave.io/workspaces/1337/attachments/265422/`

```shell
# Deletes attachment with id 265422
curl "https://api.upwave.io/workspaces/1337/attachments/3/"
  -X DELETE
  -H "Authorization: Token 9944b09199c62bcf9418ad846dd0e4bbdfc6ee4b"
```

Although you will have to create Attachments using the Comment API, deletion of attachments is done using the Attachment API.
When deleting an Attachment, the comment will be set as edited by you.
