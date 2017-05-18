---
title: UpWave API Reference

language_tabs:
  - shell: cURL

toc_footers:
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - boards
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

Welcome to the UpWave API!

This API is in it's early infant stages but will indeed help you out if you are looking for ways to list 
cards and boards. It also have some means of updating your data.

As this API is considered extremely early beta, some sections may be tagged with TODO.

If you have any problems or requests please file an issue in our [UpWave API GitHub repo](https://github.com/upwaveHQ/api).


### API Endpoint

Since UpWave confines each team with its own unique subdomain (e.g. mycompany.upwave.io),
the API endpoint will reflect this by being directly below your team location.
For example if your team domain is *myteam* the endpoint will be:

`API endpoint example: https://myteam.upwave.io/api/`

<aside class="notice">Remember that your API endpoint rests below <strong>your</strong> team domain - referred to as &lt;TEAM DOMAIN&gt; throughout this document.</aside>





# Authentication

```shell
# Authenticate to any API ENDPOINT by adding the Authorization header
curl "<API ENDPOINT>"
  -H 'Authorization: Token <API TOKEN>'
  ```
> Make sure to replace `<API TOKEN>` with your own.

For clients to authenticate, the token key should be included in the Authorization HTTP header. The key should be prefixed by the string literal "Token", with whitespace separating the two strings. For example:

`Authorization: Token 9944b09199c62bcf9418ad846dd0e4bbdfc6ee4b`

The token can be obtained by visiting your account settings. Click your profile image, select "Settings" and find your API-Key in the "Account" tab.





# Pagination

Requests that return multiple items always comes paginated. The pagination size is set to 100.
Follow the "next" and "previous" urls to turn the pages. The actual list of items are kept within the **results** block.

<aside class="notice">In paginated responses the list of items are held within the <strong>results</strong> block.</aside>



