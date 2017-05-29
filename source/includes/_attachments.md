# Attachments

Attachments may accompany a Comment and holds a resource link to either an uploaded file, a web resource or a Google Drive file.

## List Attachments

`GET https://<TEAM DOMAIN>.upwave.io/api/attachments/`

```shell
curl "https://<TEAM DOMAIN>.upwave.io/api/attachments/"
  -H "Authorization: <API TOKEN>"
```

> The above command returns JSON structured like this:

```json
  {
    "count": 3,
    "next": null,
    "previous": null,
    "results": [
      {
        "id": 1,
        "comment": 6,
        "card": 5,
        "name": "sketch.png",
        "source": "uploadedfile",
        "url": "some.image.url,
        "preview_url": "some.image.url",
        "cover_url": "some.image.url",
        "file_size": 5733,
      },
      {
        "id": 2,
        "comment": 6,
        "card": 5,
        "name": "Spreadsheet X",
        "source": "gdrive",
        "url": "https://drive.google.com/.............",
        "preview_url": null,
        "cover_url": null,
        "file_size": 0,
      },
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

Filtering options:

Parameter | Format | Description
--------- | ------- | ---- | -----------
comment | `integer` | Filter Attachments on their parent Comment
card | `integer` | Filter Attachment based on their parent Card
source | `string` | Filter Attachments on source (see below)

`"source" may be either of "uploadedfile", "link" or "gdrive"`

File sizes will only be listed for files that are either uploaded directly (source is "uploadedfile") or for Google Drive files that has a file size.

<aside class="warning">Attachments can only be created using the Comment api</aside>

## Deleting an Attachment
`DELETE https://<TEAM DOMAIN>.upwave.io/api/attachments/<ID>/`

```shell
# Deletes attachment with id 3
curl "https://<TEAM DOMAIN>.upwave.io/api/attachments/3/"
  -X DELETE
  -H "Authorization: <API TOKEN>"
```

Although you will have to create Attachments using the Comment API, deletion of attachments can be done using the Attachment API.
When deleting an Attachment, the comment will be set as edited by you.
