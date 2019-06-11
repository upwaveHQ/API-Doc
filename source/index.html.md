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

If a Workspace is linked to a social account (e.g. Google G Suite, Microsoft 365), your API requests may be rejected if you have not proven that you have successfully authenticated using that social provider.


# Pagination

GET requests that return multiple items always comes paginated. The default pagination size is set to 50 whereas the max pagination size is 100.
Follow the "next" and "previous" URLs to turn the pages. The actual list of items are kept within the **results** block.

For most of the requests, a `page_size` parameter can be issued to control the size.

<aside class="notice">In paginated responses the list of items are held within the <strong>results</strong> block.</aside>


# Throttling

All API requests are throttled. This means you will receive a status code of 429 "Too Many Requests" if you exceed our limits.
We have two quotas to control this; one per hour (for bursts) and one per day.


# Access levels

In the examples throughout this docs, you will notice the **access** block.
This block shows what access you have on the object in question.

It consist of 3 parts:

- can_edit
- can_create
- can_delete

<aside class="notice">There is no need for a <i>can_view</i>-access. All data returned is always personalized.</aside>


## Access can_edit

The *can_edit* attribute determines if you have the privileges of editing the object.
For example if the object is a Board entity, you will be able to edit its title and settings.


## Access can_create

The *can_create* attribute determines if you have the privileges to create sub objects on the object.
For example if the object is a Board entity you will be able to create Cards or Board structure objects like Colors, Columns or Rows.


## Access can_delete

The *can_delete* attribute determines if you have the privileges to delete the object.
