---
title: Upwave API Reference

language_tabs:
  - shell: cURL

toc_footers:
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - workspaces
  - teams
  - boards
  - members
  - cards
  - updatecard
  - createcard
  - tasklistitems
  - comments
  - attachments
  - errors


search: true
---


# Introduction

**Welcome to the Upwave API!**

This API will give you the means to integrate Upwave into your projects.
Typical use cases would be to list/find resources or create Cards/Comments in Upwave programatically.

If you have any problems or requests please file an issue in the [Upwave API GitHub repo](https://github.com/upwaveHQ/api).


# API Endpoints


## Workspaces

`https://api.upwave.io/workspaces/`

This is the most likely the endpoint you are looking for. It will list all the Workspaces you have access to.
Digging deeper into its structure, it will allow listing, modifying and creating entities such as Cards.


## Notifications

`https://api.upwave.io/notifications/`

Personal notifications are listed by this endpoint. It only supports the GET method.


## Auth

`https://api.upwave.io/auth/`

The auth endpoint can be used to check your authentication. It only support the GET method, and will return your account data.


# Authentication

```shell
# Authenticate to any API ENDPOINT by adding the Authorization header
curl "https://api.upwave.io/auth/"
  -H 'Authorization: Token 9944b09199c62bcf9418ad846dd0e4bbdfc6ee4b'
  ```
> Make sure to replace the API Token with your own.

For clients to authenticate, the token key should be included in the Authorization HTTP header. The key should be prefixed by the string literal "Token", with whitespace separating the two strings. For example:

`Authorization: Token 9944b09199c62bcf9418ad846dd0e4bbdfc6ee4b`

The token can be obtained by visiting your account settings. Click your profile image, select "Settings" and find your API-Key in the "Account" tab.

<aside class="notice">The token is personal - Do not share it with others</aside>

## Restrictions

If a Workspace is linked to a social account (e.g. Google Workspace, Microsoft 365), your API requests may be rejected if you have not proven that you have successfully authenticated using that social provider.


# Pagination

GET requests that return multiple items always comes paginated. The max pagination size is 100.
Follow the "next" and "previous" URLs to turn the pages. The actual list of items are kept within the **results** block.

For most of the requests, a `page_size` parameter can be issued to control the size.

<aside class="notice">In paginated responses the list of items are held within the <strong>results</strong> block.</aside>


# Throttling

All API requests are throttled. This means you will receive a status code of 429 "Too Many Requests" if you exceed our limits.
We have two quotas to control this; one per hour (for bursts) and one per day.


# Access and permissions
Most entities in this API comes with an *access* property that describes the permissions you have on the specific object.
The permissions are determined by what *role* you have in your membership.

The *access* property can have up to 5 permissions:

- can_admin
- can_modify
- can_comment
- can_invite
- can_invite_existing

<aside class="notice">There is no need for a <i>can_view</i>-access. All data returned is always personalized.</aside>


## Permission can_admin

The *can_admin* permission determines if you have the privileges of editing/administrating the object.


## Permission can_modify

The *can_modify* permission tells if you have the privileges to create sub objects on the object.
For example if the object is a Board entity you will be able to create Cards or change the Board structure objects like Colors, Columns or Rows.


## Permission can_comment

The *can_comment* permission is only present at certain objects where commenting is available and tells whether or not the user is allowed to create comments.


## Permission can_invite

The *can_invite* permission decides if the user is allowed to invite new users to the object. New users will become member of the object and any parent object.


## Permission can_invite_existing

The *can_invite_existing* permission tells if the user is allowed to invite existing Workspace members to the object.