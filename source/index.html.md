---
title: MIU Contracts API

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - python


toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true

code_clipboard: true

meta:
  - name: description
    content: Documentation for the Kittn API
---

# Introduction

Welcome. This guide is a general overview of the Miu micro-services and APIs.

The Miu APIs are REST APIs and use JSON format requests and responses.

In general, all programming languages that can access RESful services can be used to access Miu APIs. We recommend the following languages:

- Python

- Java

- C#

- JavaScrip

- Visual Basic

- R
# Miu client-api library install:

> To install Miu API Python library, you will need to use the following 


```python
from commons.utils.clients import *
from apiclient.exposurelibrary.elt_client import *

Credentials = Clients.from_credentials(user_name=UserInfo.user_name, password=UserInfo.password, env=Environment.PROD)
```

```shell
# With shell, you can just pass the correct header with each request
curl -X 'POST' \
  'https://cms.miuinsights.com/v2/oauth2/token' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/x-www-form-urlencoded' \
  -d 'username=USERNAMME%40CLIENT.com&password=PASSWORD!&grant_type=password'
```


> Make sure to replace `meowmeowmeow` with your API key.

Miu Contracts generates an access token when provided with Miu insight’s user_name and password. If you need to reset your password, please access the following link: [MIU Insight](https://www.miuinsights.com/login?returnUrl=contracts).

MIU Contracts expects for the API token to be included in all API requests to the server in a header that looks like the following:

`Authorization:WiHwMQeD580lL0bjTmr76maLe2EDJxDtaIn4TQgp `

<aside class="notice">
It is important to keep your password secure! Please place your password in a seperate file which you can reference; Do not expose your password in every script
</aside>

# Authentication

> To authorize, use this code:



```python
from commons.utils.clients import *
from apiclient.exposurelibrary.elt_client import *

Credentials = Clients.from_credentials(user_name=UserInfo.user_name, password=UserInfo.password, env=Environment.PROD)
```

```shell
# With shell, you can just pass the correct header with each request
curl -X 'POST' \
  'https://cms.miuinsights.com/v2/oauth2/token' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/x-www-form-urlencoded' \
  -d 'username=USERNAMME%40CLIENT.com&password=PASSWORD!&grant_type=password'
```


> Make sure to replace `meowmeowmeow` with your API key.

Miu Contracts generates an access token when provided with Miu insight’s user_name and password. If you need to reset your password, please access the following link: [MIU Insight](https://www.miuinsights.com/login?returnUrl=contracts).

MIU Contracts expects for the API token to be included in all API requests to the server in a header that looks like the following:

`Authorization:WiHwMQeD580lL0bjTmr76maLe2EDJxDtaIn4TQgp `

<aside class="notice">
It is important to keep your password secure! Please place your password in a seperate file which you can reference; Do not expose your password in every script
</aside>

# Exposure Library

Exposure in Contracts is sepearted into 3 types:

- ELT Event Loss Tables
- PLT Period Loss Tables
- SF-ELT Share Factor Event Loss Tables

The exposure piece below allows you to run general querries that returns availbale exposures by data version, Peril, Region and/or  ...

## Exposure

### Find Exposures



```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```shell
curl "http://example.com/api/kittens" \
  -H "Authorization: meowmeowmeow"
```


> The above command returns JSON structured like this:

```json
[
  {
    "exposureUuid": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "companyUuid": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "isPublic": true,
    "createdBy": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "createdAt": "2022-04-18T06:24:44.216Z",
    "exposureType": {},
    "description": "string",
    "dataVersionUuids": [
      "3fa85f64-5717-4562-b3fc-2c963f66afa6"
    ],
    "unitCode": "string",
    "modelUuid": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "perilUuid": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "regionUuid": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "subRegionResolutionUuid": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
    "subPerilUuids": [
      "3fa85f64-5717-4562-b3fc-2c963f66afa6"
    ],
    "subRegionUuids": [
      "3fa85f64-5717-4562-b3fc-2c963f66afa6"
    ],
    "lobUuids": [
      "3fa85f64-5717-4562-b3fc-2c963f66afa6"
    ],
    "isIlc": true,
    "totalExposure": 0,
    "isShareFactor": true,
    "startDate": "2022-04-18T06:24:44.216Z",
    "endDate": "2022-04-18T06:24:44.216Z",
    "periodMin": {},
    "periodMax": {}
  }
]
```

This Call retrieves all Exposures available in the data library; Event loss tables, Period Loss Tables and Share factors. 

##### HTTP Request

`GET http://example.com/api/kittens`

##### Query Parameters
Executing a call without providing any parameters returns a list of all the available exposure in the risk library.

Parameter | Default | Description
--------- | ------- | -----------
uuid      | -       | If Exposure Uuid is provided, the call returns information on that Uuid
dataVersionUuid | -    | If not provided the function will return exposure data for all data versions.
perilUuid | -    | Peril Uuid 
regionUuid | -    | If not provided the function will return exposure data for all data versions.
subRegionResolutionUuid | -    | If not provided the function will return exposure data for all data versions.
subPerilUuid | -    | If not provided the function will return exposure data for all data versions.
subRegionUuid | -    | If not provided the function will return exposure data for all data versions.
lobUuid | -    | If not provided the function will return exposure data for all data versions.
isUnderlyingIlc | -    | If not provided the function will return exposure data for all data versions.
isShareFactor | -    | If not provided the function will return exposure data for all data versions.
emptySubPerils | -    | If not provided the function will return exposure data for all data versions.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

## Get a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/2" \
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.get(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve

## Delete a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.delete(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.delete(2)
```

```shell
curl "http://example.com/api/kittens/2" \
  -X DELETE \
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.delete(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint deletes a specific kitten.

### HTTP Request

`DELETE http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to delete

