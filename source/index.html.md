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

The exposure piece below allows you to run general queries that return available exposures by data version, Peril, Region, and...
## Event Info
This section contains calls that help retrieve Events information; the calls below are :

1. Get event data by This call allows you to get event data by Peril, Region, data version.
2. Get event data by EventId: This call allows you to get event data by providing the EventId

Both calls return either one object or a series of objects that describe the Event and its metadata.


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

### Find Exposures by providing characteristics	 
#### : Peril Uuid, Region Uuid, subRegionResolutionUuid,subRegionUuid,lobUuid



```python
from commons.utils.clients import *
from apiclient.exposurelibrary.elt_client import *

Credentials = Clients.from_credentials(user_name=UserInfo.user_name, password=UserInfo.password, env=Environment.PROD)
Credentials.exposure.all(uuids=None,data_version_uuid='4b292524-d70c-4edb-9137-e9bc4bb41016',peril_uuid='4e2c16bc-1cf4-45e2-b7e5-86591b9802a2',
                         region_uuid='5b07643e-2bd8-4014-a837-569ab1ba1404',sub_region_resolution_uuid='7581d3ae-600b-44b4-85d9-27e821867792',
                        sub_peril_uuids=None,sub_region_uuids=None,lob_uuids=None,is_underlying_ilc=False,is_share_factor=False)
```

```shell
curl -X 'GET' \
  'https://exposurelibrary.miuinsights.com/v1/exposures?dataVersionUuid=4b292524-d70c-4edb-9137-e9bc4bb41016&perilUuid=4e2c16bc-1cf4-45e2-b7e5-86591b9802a2&regionUuid=5b07643e-2bd8-4014-a837-569ab1ba1404&subRegionResolutionUuid=7581d3ae-600b-44b4-85d9-27e821867792&isUnderlyingIlc=false&isShareFactor=false&emptySubPerils=true' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer 8YvIkh61xaRL2T3oAtAShzqMeHfSPVkSAKiPHGog'
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
Remember 
</aside>

### Add data versions to exposures:
```python
from commons.utils.clients import *
from apiclient.exposurelibrary.elt_client import *

Credentials = Clients.from_credentials(user_name=UserInfo.user_name, password=UserInfo.password, env=Environment.PROD)

AddExposureDataVersionJson = {
    "exposureUuids": [
        "0802a08f-d521-42ec-95d0-684a65f89479"
    ],
    "dataVersionUuid": "ca9d8219-776e-4024-b6be-1247f4e28150"
}
Credentials.exposure.add_data_version(AddExposureDataVersionJson)
```

```shell
curl -X 'POST' \
  'https://exposurelibrary.miuinsights.com/v1/exposures/addDataVersion' \
  -H 'accept: */*' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer sPfhI60JZCgeMMvSwYAqf2WQEa5nMHN90zFmiUrk' \
  -d '{
    "exposureUuids": [
        "0802a08f-d521-42ec-95d0-684a65f89479"
    ],
    "dataVersionUuid": "ca9d8219-776e-4024-b6be-1247f4e28150"
}'
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

Executing this call assigns a new data version to the exposures mentioend in the list.
### Find exposure's Peril & Region
```python
from commons.utils.clients import *
from apiclient.exposurelibrary.elt_client import *

Credentials = Clients.from_credentials(user_name=UserInfo.user_name, password=UserInfo.password, env=Environment.PROD)

AddExposureDataVersionJson = {
    "exposureUuids": [
        "0802a08f-d521-42ec-95d0-684a65f89479"
    ],
    "dataVersionUuid": "ca9d8219-776e-4024-b6be-1247f4e28150"
}
Credentials.exposure.add_data_version(AddExposureDataVersionJson)
```

```shell
curl -X 'POST' \
  'https://exposurelibrary.miuinsights.com/v1/exposures/addDataVersion' \
  -H 'accept: */*' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer sPfhI60JZCgeMMvSwYAqf2WQEa5nMHN90zFmiUrk' \
  -d '{
    "exposureUuids": [
        "0802a08f-d521-42ec-95d0-684a65f89479"
    ],
    "dataVersionUuid": "ca9d8219-776e-4024-b6be-1247f4e28150"
}'
```
> The above command returns this JSON with a description of the specified EventId and it's rate per dataversion

```json
{
  "perils": [
    {
      "perilUuid": "4e2c16bc-1cf4-45e2-b7e5-86591b9802a2",
      "regionUuids": [
        "5b07643e-2bd8-4014-a837-569ab1ba1404"
      ]
    }
  ]
}
  
```
## ELT event Loss tables

The series of calls below are specific to Event loss tables or ELTs. 

1. Find ELTs: This call retrieves information about all available ELTs
2. Delete ELT UUID: This call deletes an existing ELT using its UUID
3. Find ELT by UUID: This call retrieves information about a specific ELT using the UUID
4. Find ELT data: This call returns the Event loss table(Data)for a ceratin Uuid UUID
### Find ELTs

You can provide the data version, ELT uuids- one or more and specify whether the ELT is public or an ILC. The last piece is helpful if you want to retrieve ILC data.
```python
from commons.utils.clients import *
from apiclient.exposurelibrary.elt_client import *

Credentials = Clients.from_credentials(user_name=UserInfo.user_name, password=UserInfo.password, env=Environment.PROD)

Credentials.elt.all(data_version_uuid='4b292524-d70c-4edb-9137-e9bc4bb41016',is_public=False,is_ilc=False)
```

```shell
curl -X 'GET' \
  'https://exposurelibrary.miuinsights.com/v1/elts?dataVersionUuid=4b292524-d70c-4edb-9137-e9bc4bb41016&isPublic=false&isIlc=false' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer 8kx6RC2dk0TjSByLZX5mUCC0EAkTDH077fmiufmN'
}'
```
> The above command returns this JSON with a description of the specified ELT :

```json
[
  {
    "uuid": "03807e71-9e03-459a-bb00-d7b15dff4bb3",
    "companyUuid": "c6c70ba8-1405-48f1-9c65-00b5a2d5cdb9",
    "isPublic": false,
    "createdBy": "61ca4afb-8792-4fe8-a385-d232264b56c3",
    "createdAt": "2022-04-28T22:51:40.837929Z",
    "modifiedBy": "61ca4afb-8792-4fe8-a385-d232264b56c3",
    "modifiedAt": "2022-04-28T22:51:40.837929Z",
    "description": "Test ELT",
    "dataVersionUuids": [
      "4b292524-d70c-4edb-9137-e9bc4bb41016"
    ],
    "perilUuid": "b5a2bd67-f6f2-433f-8a43-76d35b1da722",
    "regionUuid": "5b07643e-2bd8-4014-a837-569ab1ba1404",
    "subRegionResolutionUuid": "7581d3ae-600b-44b4-85d9-27e821867792",
    "subPerilUuids": [],
    "subRegionUuids": [],
    "lobUuids": [],
    "unitCode": "USD",
    "rowCount": 25152,
    "isIlc": false
  },
```

### Delete ELT with specific

Delete ELT UUID: This call deletes an existing ELT using its UUID.

```python
from commons.utils.clients import *
from apiclient.exposurelibrary.elt_client import *

Credentials = Clients.from_credentials(user_name=UserInfo.user_name, password=UserInfo.password, env=Environment.PROD)

Credentials.elt.delete("2fe56132-ac9b-4d1c-843d-8ddcdf7f6ac2")
```

```shell
curl -X 'DELETE' \
  'https://exposurelibrary.miuinsights.com/v1/elts/2fe56132-ac9b-4d1c-843d-8ddcdf7f6ac2' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer 8kx6RC2dk0TjSByLZX5mUCC0EAkTDH077fmiufmN''
```
> The above command returns this JSON with a description of the specified ELT :

```json

```

### Find ELT by providing specific ELT UUID

This call provides detailed description and information on a certain ELT.

```python
from commons.utils.clients import *
from apiclient.exposurelibrary.elt_client import *

Credentials = Clients.from_credentials(user_name=UserInfo.user_name, password=UserInfo.password, env=Environment.PROD)

Credentials.elt.get_by_uuid("73aa6c0d-adc7-4b23-86e6-f1364bfba093")
```

```shell
curl -X 'GET' \
  'https://exposurelibrary.miuinsights.com/v1/elts/73aa6c0d-adc7-4b23-86e6-f1364bfba093' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer 8kx6RC2dk0TjSByLZX5mUCC0EAkTDH077fmiufmN'
```
> The above command returns this JSON with a description of the specified ELT :

```json
{
  "uuid": "73aa6c0d-adc7-4b23-86e6-f1364bfba093",
  "companyUuid": "c6c70ba8-1405-48f1-9c65-00b5a2d5cdb9",
  "isPublic": false,
  "createdBy": "61ca4afb-8792-4fe8-a385-d232264b56c3",
  "createdAt": "2022-04-29T01:45:52.300050Z",
  "modifiedBy": "61ca4afb-8792-4fe8-a385-d232264b56c3",
  "modifiedAt": "2022-04-29T01:45:52.300050Z",
  "description": "Test ELT",
  "dataVersionUuids": [
    "4b292524-d70c-4edb-9137-e9bc4bb41016"
  ],
  "perilUuid": "b5a2bd67-f6f2-433f-8a43-76d35b1da722",
  "regionUuid": "5b07643e-2bd8-4014-a837-569ab1ba1404",
  "subRegionResolutionUuid": "7581d3ae-600b-44b4-85d9-27e821867792",
  "subPerilUuids": [],
  "subRegionUuids": [],
  "lobUuids": [],
  "unitCode": "USD",
  "rowCount": 35210,
  "isIlc": false
}
```

### Find ELT Data by providing specific ELT UUID

This call provides the  Event Loss table/Data for the ELT UUID provided. You can limit the nymber of rows returned by providing a limit and an offset

```python
from commons.utils.clients import *
from apiclient.exposurelibrary.elt_client import *

Credentials = Clients.from_credentials(user_name=UserInfo.user_name, password=UserInfo.password, env=Environment.PROD)

Credentials.elt.get_data_by_uuid("2fe56132-ac9b-4d1c-843d-8ddcdf7f6ac2", limit=10)
```

```shell
curl -X 'GET' \
  'https://exposurelibrary.miuinsights.com/v1/elts/73aa6c0d-adc7-4b23-86e6-f1364bfba093/data?limit=10' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer 8kx6RC2dk0TjSByLZX5mUCC0EAkTDH077fmiufmN'
```
> The above command returns this JSON object for every Event in the event loss table of the specified ELT :

```json
[
  {
    "eventId": "1510001",
    "rate": 0.26696619,
    "stdDevCorrelated": 401.13,
    "stdDevIndependent": 12968.51,
    "totalExposure": 22785298,
    "mean": 573.59
  },
  {
    "eventId": "1510002",
    "rate": 0.52179788,
    "stdDevCorrelated": 10948.2,
    "stdDevIndependent": 29428.75,
    "totalExposure": 838596086,
    "mean": 7680.38
  },
  {
    "eventId": "1510004",
    "rate": 0.334991912,
    "stdDevCorrelated": 37980.52,
    "stdDevIndependent": 116615.96,
    "totalExposure": 3525375374,
    "mean": 24237.18
  },
  {
    "eventId": "1510005",
    "rate": 0.22089557,
    "stdDevCorrelated": 19791.26,
    "stdDevIndependent": 165322.29,
    "totalExposure": 804412605.22,
    "mean": 22842.22
  },
  {
    "eventId": "1510006",
    "rate": 0.07194286,
    "stdDevCorrelated": 859.37,
    "stdDevIndependent": 5934.76,
    "totalExposure": 140057413,
    "mean": 369.63
  },
  {
    "eventId": "1510008",
    "rate": 0.165102656,
    "stdDevCorrelated": 158.73,
    "stdDevIndependent": 2308.2,
    "totalExposure": 118062674,
    "mean": 58.22
  },
  {
    "eventId": "1510009",
    "rate": 0.563560457,
    "stdDevCorrelated": 5189.05,
    "stdDevIndependent": 28288.6,
    "totalExposure": 792189552,
    "mean": 4732.52
  },
  {
    "eventId": "1510010",
    "rate": 0.421624885,
    "stdDevCorrelated": 22861.41,
    "stdDevIndependent": 47031.34,
    "totalExposure": 1627031981,
    "mean": 21455.5
  },
  ........
```
### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to delete

