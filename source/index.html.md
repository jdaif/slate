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

> To import Miu API Python library, you will need to import both commonsutils.clients and apiclient.exposurelibrary.elt_client


```python
from commons.utils.clients import *
from apiclient.exposurelibrary.elt_client import *

Credentials = Clients.from_credentials(user_name=UserInfo.user_name, password=UserInfo.password, env=Environment.PROD)
```




> Make sure to replace `UserInfo` with your credentials.

Quick guide on how to build a virtual environment in pycharm that is fully compatible with our API library and how to install the Miu API python Library: 
 
1.	Create a new Miu Contracts dedicated environment in pycharm.
2.	You can set up a virtual environment to install the dependencies for the Miu-API python without it being affected by general Python updates in your main Python enviroment. You can set up your virtual environment with your current Python version.
4.	Copy the requirements file to the script folder under the location directory of your virtual environment. C:\Users\[user]\PycharmProjects\Python2\venv\Scripts
5.	Open the Command Prompt in Windows and redirect to the above directory using the following script: Cd C:\Users\[user]\PycharmProjects\Python2\venv\Scripts
6.	Run the following code to install requirements to the new virtual environment : pip install -r requirements.txt
7.	Run the following code to install miu-api client : pip install miu-api-client --extra-index-url=https://pypi.miuinsights.com/srwz2bogyPJO7NRcOA8cPO1Q0HXpnYyGfU55TibhVKV 
 

<aside class="notice">
It is important to keep your password secure! Please place your password in a separate file that you can always reference when initiating your session; Do not expose your password in every script
</aside>

# Authentication

> To authorize,use this code:



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

MIU Contracts expects an API token to be included in with every API requests to the server in a header that looks like the following:

`Authorization:WiHwMQeD580lL0bjTmr76maLe2EDJxDtaIn4TQgp `

<aside class="notice">
Borrowed:Access tokens are used in token-based authentication to allow an application to access an API. The application receives an access token after a user successfully authenticates and authorizes access, then passes the access token as a credential when it calls the target API. The passed token informs the API that the bearer of the token has been authorized to access the API and perform specific actions specified by the scope that was granted during authorization
</aside>

# Exposure Library


Now you can import Event Loss tables, Period Loss tables, or HD Period Loss tables. Clients can also create share factors such as an ELT or an HD PLT tagged as SF_ELT and SF_PLT. All those Loss table types fall under the exposure category.
When importing Loss tables for Peril-Regions modeled by RMS, ELTs, and HD-PLTs are matched to the Event library in Miu Contracts and assigned their respective Peril and Regions for the corresponding data version. Below are the API calls included in this section.




[MIU Exposure](https://www.miuinsights.com/docs/exposurelibrary)

- Event Catalogs: Returns all available Event info catalogs by Peril, Region, and data version 
- Event Data: This call retrieves Event info data by Peril/Region/Data version combination or simply by an EventId  
- Exposures: A series of Get and Post calls to retrieve, share or edit one or all available exposures by Peril, Region, or type.  
- ELT Event Loss Table: A series of Get, Post, and Delete calls to retrieve, share or edit one or all available ELTs by Peril, Region.
- PLT Period Loss Tables: A series of Get, Post, and Delete calls to retrieve, share or edit one or all available PLTs by Peril, Region.
- HD-PLT RMs models HD: A series of Get, Post, and Delete calls to retrieve, share or edit one or all available HD-PLTs by Peril, Region.
- SF-ELT: A series of Get, Post, and Delete calls to create, retrieve, share or edit one or all available ELTs by Peril, Region.
- SF-PLT: A series of Get, Post, and Delete calls to create, retrieve, share or edit one or all available HD-PLTs by Peril, Region.



<aside class="notice">
Available Data versions for:  ELT: V17, V18 and V21  ||  HD-PLT: V1.0 and V2.0
</aside>

## Event 

Under this section:
Calls to retrieve Event set Information from the central library. There is a unique Event-Info table for every Peril, Region, and Data-version. A catalog of all available Peril Region and Data-versions combinations is accessible through the Find event catalogs call in
 [MIU Exposure](https://www.miuinsights.com/docs/exposurelibrary)

> Event Object

```json

  {
    "perilUuid": "b5a2bd67-f6f2-433f-8a43-76d35b1da722",
    "perilCode": "CS",
    "regionUuid": "cb19d52b-a19c-4e56-970f-568f7881be56",
    "regionCode": "NA",
    "dataVersionUuid": "4b292524-d70c-4edb-9137-e9bc4bb41016"
  }

```

Catalog Object includes:

| Parameter    | Description |
|--------------|-------------|
| Peril Uuid   | -           | 
| Peril Code   | -           | 
| Region Uuid  | -           |
| Region Code  | -           |
| Data Version | -           |




Key Code/Uuid:


| Peril Code | Uuid                                 |
|------------|--------------------------------------|
| WS         | e1978b0b-8cde-4ada-8943-c82fae79a569 | 
| EQ         | cae66c3b-8665-4366-ba33-dae34eec426b | 
| WT         | 4e2c16bc-1cf4-45e2-b7e5-86591b9802a2 |
| SC         | b5a2bd67-f6f2-433f-8a43-76d35b1da722 |

| Region Code | Uuid                                 |
|-------------|--------------------------------------|
| US          | 5b07643e-2bd8-4014-a837-569ab1ba1404 | 
| JP          | 4742837d-f60f-4a08-bbf0-94d79c9aae86 | 
| MX          | 51b4d101-56c4-4ba3-b348-6db353d42e93 |
| EU          | 65215ad1-9ab6-485f-b0f2-0d4ee3df8a11 |


| Data Version | Uuid                                 |
|--------------|--------------------------------------|
| V21.0        | 4b292524-d70c-4edb-9137-e9bc4bb41016 | 
| V18.0        | ca9d8219-776e-4024-b6be-1247f4e28150 | 
| V 1.0        | 04446b5e-d16a-4023-b7e2-a9b519d801f3 |
| UNMD         | c59980b8-1e1f-4280-ae5f-d277d428ac6a | 



### Get Event Catalogs  

This command lists the Event info databases for all modeled Peril/Region; the response includes perilUuid, perilCode, regionUuid, regionCode, and dataVersionUuid for every Event dataset in RMS Catalogue
> Response

```json
[
  {
    "perilUuid": "b5a2bd67-f6f2-433f-8a43-76d35b1da722",
    "perilCode": "CS",
    "regionUuid": "cb19d52b-a19c-4e56-970f-568f7881be56",
    "regionCode": "NA",
    "dataVersionUuid": "4b292524-d70c-4edb-9137-e9bc4bb41016"
  },
  {
    "perilUuid": "cae66c3b-8665-4366-ba33-dae34eec426b",
    "perilCode": "EQ",
    "regionUuid": "44d3cb7e-b70c-40a4-856e-03b739b86ab2",
    "regionCode": "IL",
    "dataVersionUuid": "4b292524-d70c-4edb-9137-e9bc4bb41016"
  }]

  
```

| Parameter    | Description |
|--------------|-------------|
| Peril Uuid   | -           | 
| Peril Code   | -           | 
| Region Uuid  | -           |
| Region Code  | -           |
| Data Version | -           |

```python
from commons.utils.clients import *
from apiclient.exposurelibrary.elt_client import *

Credentials = Clients.from_credentials(user_name=UserInfo.user_name, password=UserInfo.password, env=Environment.PROD)

Credentials.event_catalog.all()
```

```shell
curl -X 'GET' \
  'https://exposurelibrary.miuinsights.com/v1/eventCatalogs' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer aM6JruRuSiCARpMFZtbXjS2N2q9tGK0oyWIBf9ja'
```
> Response



### Get Event data.

By specifying Peril code, Region code, and Data version UUID, this call retrieves the Event Info table.


> Parameters

```json
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
  }

  
```



| Parameter         | Description                  |
|-------------------|------------------------------|
| eventId           | -                            | 
| perilUuid         | -                            | 
| perilCode         | -                            |
| primaryRegionUuid | Uuid of Parent Region        | 
| primaryRegionCode | Code of Parent Region        |
| dataVersionUuid   | -                            | 
| description       | -                            |
| rate              | LTR rate for WS              | 
| alternativeRate   | MTR rate for WS              |
| landFallInfo      | Available for every Landfall | 

<aside class="notice">
Primary regions are parent regions within the region hierarchy. North America is a parent region to the US which is a parent region to all 50 states.
</aside>

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
> RESPONSE


### Get Event data by EventId:

The above command returns a JSON with a detailed description of the specified EventId under every RMS data version.

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
> RESPONSE

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
  }]
  
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
  }]
  
```

Executing this call assigns a new data version to the exposures mentioned in the list.
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
  }]
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
  }]

```
### URL Parameters
# Contract
A Contract represents an individual ILS class or reinsurance layer (i.e. within a treaty or bond). There can one or many contracts in a program.

## Contract Object
This is an object representing the Contract details. You can retrieve it to see the properties of your Contract and its structure.
The structure varies from one Contract to another depending on the contract calculation template, number of attached exposures, and the loss flow.

> Contract Object

```json

{
  "name": "A",
  "verticalSeq": 0,
  "status": "Written",
  "termCurrencyCode": "USD",
  "riskStartDate": "2022-01-01T00:00:00",
  "riskEndDate": "2022-12-31T23:59:59.999",
  "lossFlows": [
    {
      "lossType": "payout",
      "fromContractUuid": "f2bce488-c2f9-4296-9cd0-315ea9d80fb2",
      "fromContract": "Cat Bond 144a Flood",
      "primitiveBody": "Scale by 1.05"
    },
    {
      "lossType": "payout",
      "fromContractUuid": "9d5bd5fb-fa61-4cf2-8deb-249bdadab91b",
      "fromContract": "Cat Bond 144a WS"
    }
  ],
    "exposures": [
    {
      "uuid": "99c2a627-1cc0-4581-b1e0-3cb72e9d788d",
      "exposureType": "ELT",
      "scalingFactor": 1
    }
  ],
  "templateUuid": "48fed8e6-141b-472e-8146-b0ce7452c79d",
  "templateSubstitutions": {
    "InitialPayout": "0.0",
    "AggregateLimit": "100000000",
    "AggregateAttachment": "0",
    "Reinstatement": "0.0",
    "AggregateErosion": "0.0",
    "Principal": "100000000"
  },
  "uuid": "bfacd979-850f-4c78-9c4b-4fbcc929c980",
  "totalAmount": 100000000,
  "canParticipate": true,
  "metadata": []
}
```

| Parameter             | Description                                                                                           |
|-----------------------|-------------------------------------------------------------------------------------------------------|
| name                  | Contract Name                                                                                         | 
| VerticalSeq           | Location of Contract in the column(Tower)                                                             | 
| Status                | [program status](https://jdaif.github.io/slate/#program) Draft, Finalized, Public                     |
| termCurrencyCode      | Currency used to produce results for the template                                                     |
| riskStartDate         | Format yyyy-mm-ddThh:ss:mm                                                                            |
| riskEndDate           | Format yyyy-mm-ddThh:ss:mm                                                                            | 
| lossFlows             | [LossFlow](https://jdaif.github.io/slate/#inuring<br/>-columns-amp-loss-flow)                         | 
| exposures             | Exposures added to the Contract, includes the uuid of the exposure, exposure typle and scaling factor |
| templateUuid          | [Contract Templates](https://jdaif.github.io/slate/#contract-templates)                               |
| templateSubstitutions | Different for each contract, [Contract Templates](https://jdaif.github.io/slate/#contract-templates)  |
| uuid                  | Contract Name                                                                                         | 
| totalAmount           | Location of Contract in the column(Tower)                                                             | 
| canParticipate        | Turned off for sub-Contracts, and ON for final parent Contracts where investor can participate        |
| metadata              | -                                                                                                     |


## Find Contracts
To find Contracts by program revision, uuid, program status, isPublic status, ISIN or to filter by latest revision or exposure uuid, you can use this call.

```python
from commons.utils.clients import *
from apiclient.exposurelibrary.elt_client import *

Credentials = Clients.from_credentials(user_name=UserInfo.user_name, password=UserInfo.password, env=Environment.PROD)

Credentials.program.get_contracts(contract_uuids=None,program_revision_uuids="4fec4be4-01fa-4284-b083-3b3f99931e3c",can_participate=True,program_status='Finalized',has_secondary_contract_id=None,exposure_uuids=None,is_public=False,latest_revision_only=False)

```


```shell
# With shell, you can just pass the correct header with each request
curl -X 'GET' \
  'https://contract.miuinsights.com/v2/contracts?programRevisionUuid=4fec4be4-01fa-4284-b083-3b3f99931e3c&canParticipate=true&programStatus=Finalized&isPublic=false&hasSecondaryContractId=false&terminal=true&latestRevisionOnly=true' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer gKsMWElli6R7qgJstIFcLGO1LS0gBaM8tKFb75yr'
```

> Response 

```json
[
  {
    "uuid": "0bec92dd-96d0-40b7-bf11-56469306604b",
    "programUuid": "b857ae98-3dba-43e0-8627-fc365753727f",
    "programCompanyUuid": "efa36b93-3200-40a7-afe6-709a2a565c1a",
    "programName": "Cat Bond 144a",
    "programRevisionUuid": "4fec4be4-01fa-4284-b083-3b3f99931e3c",
    "programRevisionDataVersionUuids": [
      "04446b5e-d16a-4023-b7e2-a9b519d801f3",
      "4b292524-d70c-4edb-9137-e9bc4bb41016"
    ],
    "programRevisionName": "Revision 3",
    "programRevisionSource": "Original",
    "programStatus": "Finalized",
    "name": "A",
    "termCurrencyCode": "USD",
    "canParticipate": true,
    "totalAmount": 100000000,
    "riskStartDate": "2022-01-01T00:00:00",
    "riskEndDate": "2022-12-31T23:59:59.999",
    "isPublic": false,
    "isLatestFinalizedRevision": true
  },
  {
    "uuid": "3ffa49b0-c4e3-4394-a2af-e86dbe0e2442",
    "programUuid": "b857ae98-3dba-43e0-8627-fc365753727f",
    "programCompanyUuid": "efa36b93-3200-40a7-afe6-709a2a565c1a",
    "programName": "Cat Bond 144a",
    "programRevisionUuid": "4fec4be4-01fa-4284-b083-3b3f99931e3c",
    "programRevisionDataVersionUuids": [
      "04446b5e-d16a-4023-b7e2-a9b519d801f3",
      "4b292524-d70c-4edb-9137-e9bc4bb41016"
    ],
    "programRevisionName": "Revision 3",
    "programRevisionSource": "Original",
    "programStatus": "Finalized",
    "name": "B",
    "termCurrencyCode": "USD",
    "canParticipate": true,
    "totalAmount": 100000000,
    "riskStartDate": "2022-01-01T00:00:00",
    "riskEndDate": "2022-12-31T23:59:59.999",
    "isPublic": false,
    "isLatestFinalizedRevision": true
  }
]
```

Parameters:

| Parameter              | Description                                                                                                                       |
|------------------------|-----------------------------------------------------------------------------------------------------------------------------------|
| uuid                   | You can provide the uuid, same as call [Find a Contract](https://jdaif.github.io/slate/#find-a-contract)                          | 
| programRevisionUuid    | Retrieves all Contracts available under a certain [program revision](https://jdaif.github.io/slate/#program-revision-object) Uuid | 
| canParticipate         | Filter those where investor can participate                                                                                       |
| programStatus          | -                                                                                                                                 | 
| isPublic               | Filter contracts to those made public by RMS (144a bond public deal library)                                                      |
| isin                   | provide a collection of isin numbers                                                                                              | 
| hasSecondaryContractId | -                                                                                                                                 |
| terminal               | Whether to return only terminal contracts (contracts that no other contract has dependency on)                                    | 
| exposureUuid           | MTR rate for WS                                                                                                                   |
| latestRevisionOnly     | Filter by latest [revision](https://jdaif.github.io/slate/#program-revision-object) of every program                              | 




## Find a Contract

## Create a contract

## Contract Templates
Contract Templates represent the most common types of bonds and treaties in the market. Terms and conditions vary depending on the template. 
### First and Subsequent

Uuid for FS template is aead0f2e-866a-4cc3-9a6b-72bed098bf01

The class triggers with each event that has an index value in excess of the attachment point.

Summary of the example below:

100,000,000 principal proportionally covering 100,000,000 excess 100,000 with 2 reinstatement and 0.0 initial payout

> First and subsequent template Object

```json
 "templateUuid" : "aead0f2e-866a-4cc3-9a6b-72bed098bf01",
  "templateSubstitutions": {
    "InitialPayout": "0.0",
    "Attachment": "100000",
    "Limit": "100000000",
    "Reinstatement": "2",
    "Principal": "100000000"
  }
```

### Aggregate

Uuid for Aggregate template is 48fed8e6-141b-472e-8146-b0ce7452c79d

The class triggers when the total loss arising from all events exceeds the aggregate attachment point.


Summary of the example below:

100,000,000 principal proportionally covering 100,000,000 excess 0 aggregate loss with 0.0 reinstatement and 0.0 initial payout and 0.0 aggregate erosion

> First and subsequent template Object

```json

 "templateUuid" : "48fed8e6-141b-472e-8146-b0ce7452c79d",
  "templateSubstitutions": {
    "InitialPayout": "0.0",
    "AggregateLimit": "100000000",
    "AggregateAttachment": "0",
    "Reinstatement": "0.0",
    "AggregateErosion": "0.0",
    "Principal": "100000000"
  }

```

### Kth event

Uuid for Aggregate template is 532d7517-2e7b-434d-84fc-6f05151760a5

The class is on-risk after a specified number of triggering events. A triggering event has an index value in excess of the trigger amount


Summary of the example below:

Kth event protection with 100,000,000 principal starting with event 2 proportionally covering 100,000,000 aggregate loss with occurrence terms 25,000,000 excess 100,000 and qualified event trigger of 100,000 and 0.0 initial payout and 0.0 qualified events

> First and subsequent template Object

```json

"templateUuid": "532d7517-2e7b-434d-84fc-6f05151760a5",
  "templateSubstitutions": {
    "EventLimit": "25000000",
    "EventAttachment": "100000",
    "InitialPayout": "0.0",
    "QualifiedEventTrigger": "100000",
    "Principal": "100000000",
    "AggregateLimit": "100000000",
    "QualifiedEvents": "0.0",
    "K": "2"
  }

```


# Program 

Users can create and analyze ILS program risk. A program is a collection of ILS classes—often with a defined inuring order. For example:

What are “Draft Programs”?

Programs with terms and conditions that are not confirmed should be left as “draft”. 
Draft programs can continue to be modified and edited. Each time you edit a 
program and save it, you will create a new version.

What are “Finalized Programs”?
Programs with terms and conditions that have been confirmed and signed should be 
“finalized”. Finalized programs can no longer be modified and will prevent further 
changes to be made.

What are “Public Programs”?

All the programs modelled by RMS that are available on the public market—i.e. 144a 
bonds.

## Program Object

When a program object is retrieved, it may contain one or many [Program Revisions](https://jdaif.github.io/slate/#program-revision-object)
The description contained in the program of each revision defer from the more detailed description obtained when calling the [Program Revisions Object](https://jdaif.github.io/slate/#program-revision-object)

```json
[
  {
    "uuid": "b857ae98-3dba-43e0-8627-fc365753727f",
    "revisionUuid": "ba298bd4-96c6-42ad-af1b-36f58cf33f33",
    "name": "Cat Bond 144a",
    "revisionName": "6/10/2022, 5:32:13 PM",
    "description": {
      "source": "Original"
    },
    "status": "Finalized",
    "revisionStatus": "Finalized",
    "modifiedAt": "2022-06-11T00:32:36.427851Z",
    "modifiedBy": "323da914-7c9b-4a26-9110-8e0439df160f",
    "finalizedAt": "2022-06-11T00:32:56.539555Z",
    "finalizedBy": "323da914-7c9b-4a26-9110-8e0439df160f",
    "companyUuid": "efa36b93-3200-40a7-afe6-709a2a565c1a",
    "isPublic": false,
    "isPublicRevision": false,
    "dataVersionUuids": [
      "04446b5e-d16a-4023-b7e2-a9b519d801f3",
      "4b292524-d70c-4edb-9137-e9bc4bb41016"
    ],
    "metadata": [],
    "hasErrors": false,
    "isPltOnly": false
  },
  {
    "uuid": "b857ae98-3dba-43e0-8627-fc365753727f",
    "revisionUuid": "4fec4be4-01fa-4284-b083-3b3f99931e3c",
    "name": "Cat Bond 144a",
    "revisionName": "Revision 3",
    "description": {
      "source": "Original"
    },
    "status": "Finalized",
    "revisionStatus": "Finalized",
    "modifiedAt": "2022-06-11T21:40:10.793038Z",
    "modifiedBy": "323da914-7c9b-4a26-9110-8e0439df160f",
    "finalizedAt": "2022-06-11T21:40:38.718464Z",
    "finalizedBy": "323da914-7c9b-4a26-9110-8e0439df160f",
    "companyUuid": "efa36b93-3200-40a7-afe6-709a2a565c1a",
    "isPublic": false,
    "isPublicRevision": false,
    "dataVersionUuids": [
      "04446b5e-d16a-4023-b7e2-a9b519d801f3",
      "4b292524-d70c-4edb-9137-e9bc4bb41016"
    ],
    "metadata": [],
    "hasErrors": false,
    "isPltOnly": false
  },
  {
    "uuid": "b857ae98-3dba-43e0-8627-fc365753727f",
    "revisionUuid": "6ec89120-79cb-4721-b175-4afda88e0fee",
    "name": "Cat Bond 144a",
    "revisionName": "Revision 4",
    "description": {
      "source": "Original"
    },
    "status": "Finalized",
    "revisionStatus": "Finalized",
    "modifiedAt": "2022-06-28T05:36:13.222719Z",
    "modifiedBy": "323da914-7c9b-4a26-9110-8e0439df160f",
    "finalizedAt": "2022-06-28T05:36:42.800079Z",
    "finalizedBy": "323da914-7c9b-4a26-9110-8e0439df160f",
    "companyUuid": "efa36b93-3200-40a7-afe6-709a2a565c1a",
    "isPublic": false,
    "isPublicRevision": false,
    "dataVersionUuids": [
      "04446b5e-d16a-4023-b7e2-a9b519d801f3",
      "4b292524-d70c-4edb-9137-e9bc4bb41016"
    ],
    "metadata": [],
    "hasErrors": false,
    "isPltOnly": false
  }
]


```
The table below contains the parameters returned when calling a program object -- per revision

| Parameter           | Description                                                                                                        |
|---------------------|--------------------------------------------------------------------------------------------------------------------|
| uuid                | Program Uuid                                                                                                       | 
| revisionUuid        | Program Revision Uuid                                                                                              | 
| name                | Program name under that revision -could defer from one revision to another                                         |
| description         | Contains gerneral description such as the source                                                                   |
| status              | Draft/Finalized/Public specific to the entire program : [Program Status](https://jdaif.github.io/slate/#program)   |
| revisionStatus      | Draft/Finalized/Public specific to the program revision : [Program Status](https://jdaif.github.io/slate/#program) | 
| modifiedAt          | -                                                                                                                  | 
| modifiedBy          | Uuid of user that modified the program                                                                             |
| finalizedAt         | The date when the program revision was finalized                                                                   |
| finalizedBy         | Uuid of teh user that finalized the revision                                                                       |
| companyUuid         | Specific to each company                                                                                           | 
| isPublic            | True/False if the program in general is public or not                                                              | 
| isPublicRevision    | True/False if the program revision  is public or not                                                               |
| dataVersionUuids    | Reflects the Dataversions of the exposure included in the program revision                                         |
## Program Revision Object

Every program revision object contains a more detailed description that defines the deal's structure. 


```json
{
  "errors": [],
  "program": {
    "uuid": "b857ae98-3dba-43e0-8627-fc365753727f",
    "revisionUuid": "ba298bd4-96c6-42ad-af1b-36f58cf33f33",
    "name": "Cat Bond 144a",
    "revisionName": "6/10/2022, 5:32:13 PM",
    "description": {
      "source": "Original"
    },
    "status": "Finalized",
    "revisionStatus": "Finalized",
    "isPublic": false,
    "isPublicRevision": false,
    "modifiedAt": "2022-06-11T00:32:36.427851Z",
    "modifiedBy": "323da914-7c9b-4a26-9110-8e0439df160f",
    "finalizedAt": "2022-06-11T00:32:56.539555Z",
    "finalizedBy": "323da914-7c9b-4a26-9110-8e0439df160f",
    "companyUuid": "efa36b93-3200-40a7-afe6-709a2a565c1a",
    "inuringColumns": [
      {
        "contracts": [
          {
            "name": "Cat Bond 144a WS",
            "verticalSeq": 0,
            "status": "Written",
            "termCurrencyCode": "USD",
            "riskStartDate": "2022-01-01T00:00:00",
            "riskEndDate": "2022-12-31T23:59:59.999",
            "lossFlows": [],
            "exposures": [
              {
                "uuid": "99c2a627-1cc0-4581-b1e0-3cb72e9d788d",
                "exposureType": "ELT",
                "scalingFactor": 1
              }
            ],
            "templateUuid": "aead0f2e-866a-4cc3-9a6b-72bed098bf01",
            "templateSubstitutions": {
              "InitialPayout": "0.0",
              "Attachment": "100000",
              "Limit": "100000000",
              "Reinstatement": "2",
              "Principal": "100000000"
            },
            "uuid": "44c6043b-8877-47bb-9c38-509933c985e7",
            "totalAmount": 100000000,
            "canParticipate": true,
            "metadata": []
          },
          {
            "name": "Cat Bond 144a Flood",
            "verticalSeq": 1,
            "status": "Written",
            "termCurrencyCode": "USD",
            "riskStartDate": "2022-01-01T00:00:00",
            "riskEndDate": "2022-12-31T23:59:59.999",
            "lossFlows": [],
            "exposures": [
              {
                "uuid": "bb3a8d3e-04ff-4d4f-ba69-f7cd80e5e133",
                "exposureType": "PLTHD"
              }
            ],
            "templateUuid": "aead0f2e-866a-4cc3-9a6b-72bed098bf01",
            "templateSubstitutions": {
              "InitialPayout": "0.0",
              "Attachment": "250000",
              "Limit": "100000000",
              "Reinstatement": "0.0",
              "Principal": "50000000"
            },
            "uuid": "69c63942-a586-4c49-b3e4-411f82ec6aba",
            "totalAmount": 50000000,
            "canParticipate": true,
            "metadata": []
          }
        ]
      },
      {
        "contracts": [
          {
            "name": "A",
            "verticalSeq": 0,
            "status": "Written",
            "termCurrencyCode": "USD",
            "riskStartDate": "2022-01-01T00:00:00",
            "riskEndDate": "2022-12-31T23:59:59.999",
            "lossFlows": [
              {
                "lossType": "payout",
                "fromContractUuid": "44c6043b-8877-47bb-9c38-509933c985e7",
                "fromContract": "Cat Bond 144a WS"
              },
              {
                "lossType": "payout",
                "fromContractUuid": "69c63942-a586-4c49-b3e4-411f82ec6aba",
                "fromContract": "Cat Bond 144a Flood"
              }
            ],
            "exposures": [],
            "templateUuid": "48fed8e6-141b-472e-8146-b0ce7452c79d",
            "templateSubstitutions": {
              "InitialPayout": "0.0",
              "AggregateLimit": "100000000",
              "AggregateAttachment": "0",
              "Reinstatement": "0.0",
              "AggregateErosion": "0.0",
              "Principal": "100000000"
            },
            "uuid": "9c3f1c9a-09b3-449f-825e-0a7807df85e3",
            "totalAmount": 100000000,
            "canParticipate": true,
            "metadata": []
          },
          {
            "name": "B",
            "verticalSeq": 1,
            "status": "Written",
            "termCurrencyCode": "USD",
            "riskStartDate": "2022-01-01T00:00:00",
            "riskEndDate": "2022-12-31T23:59:59.999",
            "lossFlows": [
              {
                "lossType": "payout",
                "fromContractUuid": "44c6043b-8877-47bb-9c38-509933c985e7",
                "fromContract": "Cat Bond 144a WS"
              },
              {
                "lossType": "payout",
                "fromContractUuid": "69c63942-a586-4c49-b3e4-411f82ec6aba",
                "fromContract": "Cat Bond 144a Flood"
              }
            ],
            "exposures": [],
            "templateUuid": "aead0f2e-866a-4cc3-9a6b-72bed098bf01",
            "templateSubstitutions": {
              "InitialPayout": "0.0",
              "Attachment": "0",
              "Limit": "100000000",
              "Reinstatement": "0.0",
              "Principal": "100000000"
            },
            "uuid": "c6deec63-6b23-49e8-a61b-4c2d90c1f1f8",
            "totalAmount": 100000000,
            "canParticipate": true,
            "metadata": []
          }
        ]
      }
    ],
    "dataVersionUuids": [
      "04446b5e-d16a-4023-b7e2-a9b519d801f3",
      "4b292524-d70c-4edb-9137-e9bc4bb41016"
    ],

    "isPltOnly": false
  }
}
```
| Parameter             | Description                                                                                                        |
|-----------------------|--------------------------------------------------------------------------------------------------------------------|
| uuid                  | Program Uuid                                                                                                       | 
| revisionUuid          | Program Revision Uuid                                                                                              | 
| name                  | Program name under that revision -could defer from one revision to another                                         |
| description           | Contains gerneral description such as the source                                                                   |
| status                | Draft/Finalized/Public specific to the entire program : [Program Status](https://jdaif.github.io/slate/#program)   |
| revisionStatus        | Draft/Finalized/Public specific to the program revision : [Program Status](https://jdaif.github.io/slate/#program) | 
| isPublic              | True/False if the program in general is public or not                                                              | 
| isPublicRevision      | True/False if the program revision  is public or not                                                               |
| modifiedAt            | -                                                                                                                  | 
| modifiedBy            | Uuid of user that modified the program                                                                             |
| finalizedAt           | The date when the program revision was finalized                                                                   |
| finalizedBy           | Uuid of teh user that finalized the revision                                                                       |
| companyUuid           | Specific to each company                                                                                           | 
| inuringColumns        | Starting from 0 upward, each column would include a list of Contracts                                              | 
| contracts             | A list of [Contracts](https://jdaif.github.io/slate/#contract) under each column                                   |
| dataVersionUuids      | Reflects the Dataversions of the exposure included in the program revision                                         |

### Inuring Columns & Loss Flow
Losses can inure from Contracts in one column to another. Losses flow from left to right. Losses can not inure from Contracts to others under the same column.

What are Inuring Losses?

Inuring Losses consist of the Net Loss and Payout of a contract. They can be defined 
as Inputs to a subsequent contract

What is Net Loss?

Net Loss is the loss remaining after the terms and conditions of a contract are 
applied. Net Loss data is in the form of a PLT.

What is Payout?

Payout is the loss absorbed by the terms and conditions of a contract. Payout data is 
in the form of a PLT.


## List all programs

This call retrieves all available programs in the deal library, user can filter by specifying the parameters below:

```python
from commons.utils.clients import *
from apiclient.exposurelibrary.elt_client import *

Credentials = Clients.from_credentials(user_name=UserInfo.user_name, password=UserInfo.password, env=Environment.PROD)
all_programs_v21 =Credentials.program.all(public=True,data_version_uuid="4b292524-d70c-4edb-9137-e9bc4bb41016") 
#Code below takes the text Json response and transforms it to a dataframe
all_programs_v21 = json.loads(all_programs_v21.text)
all_programs_v21 =pd.DataFrame(all_programs_v21)
```

```shell
curl -X 'GET' \
  'https://contract.miuinsights.com/v2/programs?status=finalized&public=true&limit=3&sortBy=NAME&sortOrder=asc' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer 5gcaX7DNAXpRgOX50X8ZSO8jZJKGR11nozDYpirt'
```

```json
[
  {
    "uuid": "2f2a1a79-ca42-4558-8103-354308ae6f89",
    "revisionUuid": "44e85985-71a3-4b31-8734-9ad0f3b8710d",
    "name": "2001 Cat Re Ltd. 2020-1",
    "revisionName": "Post-Close v21 Updated",
    "description": {
      "source": "Original",
      "year": 2020,
      "cedant": "Allied World Assurance Company Holdings"
    },
    "status": "Finalized",
    "revisionStatus": "Finalized",
    "modifiedAt": "2022-02-14T23:13:01.436742Z",
    "modifiedBy": "8ed9bf0c-4b1c-413a-a126-9155f4d0b48e",
    "finalizedAt": "2022-02-14T23:13:35.086569Z",
    "finalizedBy": "8ed9bf0c-4b1c-413a-a126-9155f4d0b48e",
    "companyUuid": "efa36b93-3200-40a7-afe6-709a2a565c1a",
    "isPublic": true,
    "isPublicRevision": true,
    "dataVersionUuids": [
      "4b292524-d70c-4edb-9137-e9bc4bb41016"
    ],
    "metadata": [],
    "isPltOnly": false
  },
  {
    "uuid": "ae91a5e2-bee5-4994-9e35-8073a373edc0",
    "revisionUuid": "10512c2e-f48b-4d77-a484-394b13ee40be",
    "name": "2001 Cat Re Ltd. 2020-1 Pre Close",
    "description": {
      "source": "Original",
      "year": 2020,
      "cedant": "Allied World Assurance Company Holdings"
    },
    "status": "Finalized",
    "revisionStatus": "Finalized",
    "modifiedAt": "2020-11-04T16:22:20.663769Z",
    "modifiedBy": "ccb19eab-42c8-4719-b4a3-7462367188fa",
    "finalizedAt": "2020-11-05T10:09:56.151694Z",
    "finalizedBy": "d69361fd-d4bc-48bf-986b-ba4d18c04a8c",
    "companyUuid": "efa36b93-3200-40a7-afe6-709a2a565c1a",
    "isPublic": true,
    "isPublicRevision": true,
    "dataVersionUuids": [
      "ca9d8219-776e-4024-b6be-1247f4e28150"
    ],
    "metadata": [],
    "isPltOnly": false
  },
  {
    "uuid": "9e24d1c2-82d5-460c-9011-d7dd5c85fbf0",
    "revisionUuid": "1ac28d83-9098-4268-b3ed-010edaf63e9f",
    "name": "3264 Re Ltd. 2020-1",
    "revisionName": "Reset 2021 v21",
    "description": {
      "source": "Reset",
      "year": 2021,
      "cedant": "Hannover Ruck SE"
    },
    "status": "Finalized",
    "revisionStatus": "Finalized",
    "modifiedAt": "2022-01-11T23:27:52.880965Z",
    "modifiedBy": "8ed9bf0c-4b1c-413a-a126-9155f4d0b48e",
    "finalizedAt": "2022-01-11T23:27:53.143731Z",
    "finalizedBy": "8ed9bf0c-4b1c-413a-a126-9155f4d0b48e",
    "companyUuid": "efa36b93-3200-40a7-afe6-709a2a565c1a",
    "isPublic": true,
    "isPublicRevision": true,
    "dataVersionUuids": [
      "4b292524-d70c-4edb-9137-e9bc4bb41016"
    ],
    "metadata": [],
    "isPltOnly": false
  }
]

```
| Parameter         | Description                                            |
|-------------------|--------------------------------------------------------|
| status            | finalized/draft                                        | 
| public            | True/False                                             | 
| dataVersionUuid   | Filter by Uuid                                         |
| uuid              | Program uuid                                           | 
| revisionUuid      | Program revision uuid                                  |
| cedenceType       | Programs with the given cedence type : Inward/outward  | 
| offset            | Offset the items returned                              |
| limit             | limit the number of items returned to a certain number | 
| sortBy            | Name, date modified ....                               |
| sortOrder         | asc/desc                                               | 
## Create a program


## Get all program revision summary

## Get the latest revision summary

## Delete specific program revision

## Delete a program

## Update program revision name

## Finalize a program

# Portfolio

## Portfolio Object

## Portfolio Revision Object

## Find portfolio

## Find latest portfolio revision

## Find portfolio revision

## Create portfolio

## Edit portfolio

## Update portfolio name

## Get exposure contained in portfolio

## 

# Analysis 

Miu uses a simulation methodology that produces a sequence of event losses during a simulated investment period and supports the modelling of complex financial structures.

With Miu Contracts, you can import also pre-simulated losses and run them along.


## Analysis Object

This is an object representing the analysis details. You can retrieve it to see the properties of your analysis, 

Object structure varies between program and portfolio analysis
> Analysis Object

```json
{
  "analysisUuid": "31d6a477-fcc2-4d2f-bb4c-71d9d7aa393b",
  "analysisName": "Cat Bond 144a",
  "jobCreationDate": "2022-06-11T00:33:13.736628Z",
  "jobStartDate": "2022-06-11T00:33:13.736636Z",
  "jobEndDate": "2022-06-11T00:39:21.233987Z",
  "companyUuid": "efa36b93-3200-40a7-afe6-709a2a565c1a",
  "userUuid": "323da914-7c9b-4a26-9110-8e0439df160f",
  "status": "FINISHED",
  "analysisType": "SIMULATED",
  "startDate": "2022-01-01T00:00:00",
  "endDate": "2022-12-31T23:59:59.999",
  "periodStart": 1,
  "periodEnd": 10000,
  "stochasticYltUuids": [
    "d95d92d3-f7aa-4918-adf1-e15beea0d3cf"
  ],
  "dataVersionUuid": "4b292524-d70c-4edb-9137-e9bc4bb41016",
  "programUuid": "b857ae98-3dba-43e0-8627-fc365753727f",
  "programRevisionUuid": "ba298bd4-96c6-42ad-af1b-36f58cf33f33",
  "cplts": [
    {
      "uuid": "c65d8ed0-7834-4f28-a8ff-01b4043b113f",
      "ipltUuid": "34ecbcea-dd8b-46f3-a3c9-0123fbf21de6",
      "programRevisionUuid": "ba298bd4-96c6-42ad-af1b-36f58cf33f33",
      "contractUuid": "44c6043b-8877-47bb-9c38-509933c985e7",
      "termCurrencyCode": "USD",
      "totalAmount": 100000000
    },
    {
      "uuid": "628367f0-5bf7-44a1-9bbf-2cf31ae51e42",
      "ipltUuid": "2a46626f-90f7-41c4-b6e8-4ccab3ac9501",
      "programRevisionUuid": "ba298bd4-96c6-42ad-af1b-36f58cf33f33",
      "contractUuid": "69c63942-a586-4c49-b3e4-411f82ec6aba",
      "termCurrencyCode": "USD",
      "totalAmount": 50000000
    },
    {
      "uuid": "343000f2-3a3a-4c1b-a16f-d365a64e6619",
      "ipltUuid": "e3f226db-e26e-4ec1-8239-6ca64972e3d1",
      "programRevisionUuid": "ba298bd4-96c6-42ad-af1b-36f58cf33f33",
      "contractUuid": "9c3f1c9a-09b3-449f-825e-0a7807df85e3",
      "termCurrencyCode": "USD",
      "totalAmount": 100000000
    },
    {
      "uuid": "1d5b3c13-21c9-47c6-a907-09f05f7bbd44",
      "ipltUuid": "13002faf-c70e-4ae5-a06b-1c8947bee02f",
      "programRevisionUuid": "ba298bd4-96c6-42ad-af1b-36f58cf33f33",
      "contractUuid": "c6deec63-6b23-49e8-a61b-4c2d90c1f1f8",
      "termCurrencyCode": "USD",
      "totalAmount": 100000000
    }
  ],
  "complexityScore": 60,
  "totalContracts": 4,
  "currencySetUuid": "10dde323-735b-457f-a64b-1fe8a45d31f0",
  "inputs": [],
  "outputs": [
    "EPCURVES",
    "ANALYSIS_METRICS",
    "PERIL_REGION_METRICS"
  ],
  "currencyCode": "USD"
}

```
| Parameter           | Description                                                  |
|---------------------|--------------------------------------------------------------|
| analysisUuid        | -                                                            | 
| analysisName        | -                                                            | 
| jobCreationDa te    | -                                                            |
| jobStartDate        | Uuid of Parent Region                                        | 
| jobEndDate          | Code of Parent Region                                        |
| companyUuid         | -                                                            | 
| userUuid            | -                                                            |
| status              | LTR rate for WS                                              | 
| analysisType        | MTR rate for WS                                              |
| startDate           | Available for every Landfall                                 | 
| endDate             | Available for every Landfall                                 | 
| periodStart         | Available for every Landfall                                 | 
| periodEnd           | Available for every Landfall                                 | 
| stochasticYltUuids  | Available for every Landfall                                 | 
| programUuid         | Available for every Landfall                                 | 
| programRevisionUuid | Available for every Landfall                                 | 
| cplts               | Available for every Landfall                                 | 
| currencySetUuid     | [CPLT](https://jdaif.github.io/slate/#get-cplt-by-analysis ) | 



## Run analysis

## Resubmit analysis

## Find analysis

## Delete Analysis

## Get persisted metrics

## Get EP curves

## Get CPLT

### Get CPLT by Analysis 

### Get CPLT by Contract