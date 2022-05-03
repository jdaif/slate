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


> Make sure to replace `UserInfo` with your credentials.

Here is a detailed description of how to build a virtual environment in pycharm that is fully compatible with our API library and how to install the Miu Python API client: 
 
1.	You can create a Miu Contracts  in pycharm.
 
2.	You can set up a virtual environment to install the dependencies for the Miu-API python without it being affected by general Python updates in your main Python enviroment. You can set up your virtual environment with your current Python version.
4.	Copy the requirements file to the script folder under the location directory of your virtual environment. C:\Users\[user]\PycharmProjects\Python2\venv\Scripts
 
5.	Open the Command Prompt in Windows and redirect to the above directory using the following script: Cd C:\Users\[user]\PycharmProjects\Python2\venv\Scripts
 
6.	Run this script to install requirements to the new virtual environment : pip install -r requirements.txt
7.	Run this script to install miu-api client : pip install miu-api-client --extra-index-url=https://pypi.miuinsights.com/srwz2bogyPJO7NRcOA8cPO1Q0HXpnYyGfU55TibhVKV 
 

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


> Make sure to replace `UserInfo` with your credentials.

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
## Event Info


### Get Event data,  by specifying Peril, Region, Data version and if requred a limit and an offset to the number of eventd to be imported.
```python
from commons.utils.clients import *
from apiclient.exposurelibrary.elt_client import *

Credentials = Clients.from_credentials(user_name=UserInfo.user_name, password=UserInfo.password, env=Environment.PROD)

Credentials.event_info.get('WS','US','4b292524-d70c-4edb-9137-e9bc4bb41016')
```

```shell
curl -X 'GET' \
  'https://exposurelibrary.miuinsights.com/v1/events?perilCode=WS&regionCode=US&dataVersionUuid=4b292524-d70c-4edb-9137-e9bc4bb41016&limit=100' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer trihPlWCssXdQvMn73vPJ46YN8ROVpt8w7mBPJ3G'
```
> The above command returns this JSON with a description of every EventId 

```json
[
  {
    "eventId": 2847001,
    "perilUuid": "e1978b0b-8cde-4ada-8943-c82fae79a569",
    "perilCode": "WS",
    "primaryRegionUuid": "cb19d52b-a19c-4e56-970f-568f7881be56",
    "primaryRegionCode": "NA",
    "dataVersionUuid": "4b292524-d70c-4edb-9137-e9bc4bb41016",
    "rate": 1e-10,
    "alternativeRate": 1e-10
  },
  {
    "eventId": 2847002,
    "perilUuid": "e1978b0b-8cde-4ada-8943-c82fae79a569",
    "perilCode": "WS",
    "primaryRegionUuid": "cb19d52b-a19c-4e56-970f-568f7881be56",
    "primaryRegionCode": "NA",
    "dataVersionUuid": "4b292524-d70c-4edb-9137-e9bc4bb41016",
    "rate": 1e-10,
    "alternativeRate": 1e-10
  }, 
  .....
  
```
### Get Event data by providing EventId:
```python
from commons.utils.clients import *
from apiclient.exposurelibrary.elt_client import *

Credentials = Clients.from_credentials(user_name=UserInfo.user_name, password=UserInfo.password, env=Environment.PROD)

Credentials.event_info.get_by_event_id("2847001")
```

```shell
curl -X 'GET' \
  'https://exposurelibrary.miuinsights.com/v1/events/2847001' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer trihPlWCssXdQvMn73vPJ46YN8ROVpt8w7mBPJ3G'
```
> The above command returns this JSON with a description of the specified EventId and it's rate per dataversion

```json
[
 {
    "eventId": 2847001,
    "perilUuid": "e1978b0b-8cde-4ada-8943-c82fae79a569",
    "perilCode": "WS",
    "primaryRegionUuid": "cb19d52b-a19c-4e56-970f-568f7881be56",
    "primaryRegionCode": "NA",
    "dataVersionUuid": "ca9d8219-776e-4024-b6be-1247f4e28150",
    "typeCode": "STOC",
    "name": "NOTNAMED, 06/25/1851",
    "description": "NOTNAMED, 06/25/1851: TX-C1 GM1",
    "rate": 1e-10,
    "alternativeRate": 1e-10,
    "landFallInfo": {
      "first": {
        "category": "1",
        "gateRegionCode": "Texas",
        "state": "TX",
        "latitude": "28.13",
        "longitude": "-96.67",
        "oneMinuteWindSpeed": "92",
        "byPassing": "L",
        "direction": "282",
        "forwardVelocity": "6",
        "rMaxRight": "-96.67"
      }
    },
    "magnitude": "0",
    "segment": "1"
  },
  
```

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

