---
title: Miu Contracts API

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - python


toc_footers:
  - <a href='https://www.miuinsights.com/docs/analysis'>Miu Contracts Swagger Documentation</a>

includes:
  - errors

search: true

code_clipboard: true

meta:
  - name: description
    content: Documentation for Miu Contracts API
---

# Introduction

Welcome. This guide is a general overview of the Miu micro-services and APIs.

The Miu APIs are REST APIs and use JSON format requests and responses.

In general, all programming languages that can access Restful services can be used to access Miu APIs. We recommend using Python since users can take advantage of the Miu Python API library. The library is comprehensive and was developed to expedite user integration.Clients can also choose from the following languages:

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

Quick guide on how to build a virtual environment in PyCharm that is fully compatible with our API library and how to install the Miu API python Library: 
 
1.	Create a new Miu Contracts dedicated environment in [PyCharm Community or Professional](https://www.jetbrains.com/pycharm/download/#section=windows).
2.	You can set up a virtual environment to install the dependencies for the Miu-API Client without it being affected by general Python updates in your main Python enviroment. You can set up your virtual environment with your current Python version.
4.	Copy the requirements file to the script folder under the location directory of your virtual environment. C:\Users\[user]\PyCharmProjects\Python2\venv\Scripts
5.	Open the Command Prompt in Windows and redirect to the above directory using the following script: Cd C:\Users\[user]\PyCharmProjects\Python2\venv\Scripts
6.	Run the following code to install requirements to the new virtual environment : pip install -r requirements.txt
7.	Run the following code to install miu-api client : pip install miu-api-client --extra-index-url=https://pypi.miuinsights.com/srwz2bogyPJO7NRcOA8cPO1Q0HXpnYyGfU55TibhVKV 
 

<aside class="notice">
It is important to keep your password secure! Please place your password in a separate file that you can always reference when initiating your session; Do not expose your password in every script.
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

Miu Contracts expects an API token with every API request to the server. 

`Authorization:WiHwMQeD580lL0bjTmr76maLe2EDJxDtaIn4TQgp `

<aside class="notice">
Access tokens are used in token-based authentication to allow an application to access an API. The application receives an access token after a user successfully authenticates and authorizes access, then passes the access token as a credential when it calls the target API. The passed token informs the API that the bearer of the token has been authorized to access the API and perform specific actions specified by the scope that was granted during authorization
</aside>


# Python Library

The Miu API client Python Library was developed to save our users the pain of developing all API calls from scratch. 

The API Python library organizes Miu Contract's objects into separate sections; this way of structuring things makes coding much more straightforward and scripts shorter. You can recursively expand the calls available for every Object by specifying nested calls after the dot. This document provides:

- A description and attributes for every Object
- Required and optional parameters for every call
- Quick codes that could simplify your use cases
- Python scripts for major workflows




# Exposure Library


In Miu Contracts, users can import Event Loss tables, Period Loss tables, or HD Period Loss tables. Clients can also create share factors based on ELT or HD-PLT ILCs (useful for ILWs) . Those objects get labeled as SF_ELT or SF_PLT.

When importing Event Loss tables for Peril-Regions modeled by RMS, EventIds in either ELTs or HD-PLTs are matched to the events under Miu Contracts' Library and risk data is automatically assigned to its respective Peril and Regions for any data version. EventId objects can be accessed using the sequence of calls that is covered in the next section. 

Users can import event loss tables (ELTs)  without associating them with RMS peril models. In conjunction with the ability to import YLTs, users can model contract losses upon event-based exposures that reflect custom or third-party views of risk. 










<aside class="notice">
Available Data versions for:  ELT: V17, V18 and V21  ||  HD-PLT: V1.0 and V2.0
</aside>

<aside class="notice">
When importing a third-party view of risk, select UNMD as your data version.
</aside>

## Event 

Under this section we find the calls to retrieve Event set Information from the Miu Contracts' EventInfo library. There is a unique Event-Info table for every Peril, Region, and Data-version combination. 


### Event Catalogue Object

> Event Catalog Object

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

| Attributes   | Description                                                 |
|--------------|-------------------------------------------------------------|
| Peril Uuid   | Universal Unique identifier for every Peril across regions  | 
| Peril Code   | Code identifier  for every Peril across regions             | 
| Region Uuid  | Universal Unique identifier  for every Region across perils |
| Region Code  | Code identifier  for every Region across perils             |
| Data Version | Data version associated with this catalogue                 |



### Get Event Catalogs  

This call lists all available Event catalogs. You can use them to identify what Models are available in your library by Peril, Region, or data version.



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
| Parameter | Description |
|-----------|-------------|
| -         | -           | 


### Event Object

> Event Object

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

| Attributes        | Description                                                 |
|-------------------|-------------------------------------------------------------|
| eventId           | Event's unique identifier                                   | 
| perilUuid         | Universal Unique identifier for every Peril across regions  | 
| perilCode         | Unique Peril code across all Regions                        |
| primaryRegionUuid | Unique Parent Region identifier across all Perils           | 
| primaryRegionCode | Unique Parent Region code across all Perils                 |
| dataVersionUuid   | Unique data version Identifier                              | 
| description       | Event description provided by RMS.                          |
| rate              | Default RMS rate for an event. Example LTR for NAHU         | 
| alternativeRate   | Alternative rate for an event. Example MTR for NAHU         |
| landFallInfo      | Available for every Landfall                                | 

<aside class="notice">
Events are inherited from parent regions. For example: the US and Mexico have the same Event info since they share the same Parent Region, North America.

Peril and Region codes are made of 2 digits for RMS Perils and 3 digits for custom Perils  
</aside>


### Get Event data.

By specifying Peril code, Region code, and Data version UUID, this call retrieves the Event Info table.

```python

import UserInfo
import UserInfo
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

> response

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



| Parameter         | Description                                         |
|-------------------|-----------------------------------------------------|
| perilCode         | Unique Peril code across all Regions                | 
| regioncode        | Unique Region code across all Perils                | 
| dataVersionUuid   | Event Info varies from one data version to another. | 


<aside class="notice">
Event info is inherited from parent regions example: North America is the parent region of the US, Canada, Mexico, and the Caribbean.
</aside>





### Get Event data by EventId:
This command returns a JSON with a detailed description of the stated EventId in all data versions.



```python
import UserInfo
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

| Parameter | Description                                  |
|-----------|----------------------------------------------|
| eventId   | Id provided by RMS for every event           | 


## Exposure

### Exposure Object


> Exposure Object

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


| Attributes              | Description                                                                                                           |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------|
| exposureUuid            | Universal Unique identifier for the exposure. Also called ELT-Uuid or PLT-Uuid depending on exposure type             | 
| companyUuid             | Universal Unique identifier of Company that was used to create the exposure, all public deals have an RMS companyUuid | 
| isPublic                | True if the exposure is public and shared by RMS as an ILC or part of 144A deals exposure                             |
| createdBy               | Universal Unique identifier of the user that created the exposure                                                     | 
| createdAt               | Date of creation                                                                                                      |
| exposureType            | Type of exposure, could be an ELT, PLT, HD_PL, SF_PLT or SF_ELT                                                       | 
| description             | Exposure's Description                                                                                                |
| dataVersionUuids        | Data-version with which the exposure was created, some exposures could have more than one data version                | 
| unitCode                | Currency code                                                                                                         |
| modelUuid               | Universal Unique identifier of Model used to create the exposure (Model is a combination of Peril/Region)             | 
| perilUuid               | Unique Peril identifier across all Regions                                                                            |
| regionUuid              | Unique Region identifier across all Perils                                                                            | 
| subRegionResolutionUuid | Universal Unique identifier of the subregion associated with this exposure.                                           |
| subPerilUuids           | Universal Unique identifier for sub perils assigned to this exposure.                                                 | 
| subRegionUuids          | Universal Unique identifiers of sub regions assigned to this exposure.                                                |
| lobUuids                | Universal Unique identifier for lines of businesses assigned to this exposure                                         | 
| isIlc                   | True if the exposure is an Industry Loss Curve shared by RMS                                                          |
| isShareFactor           | True if the exposure was created using the share factor tool                                                          | 
| startDate               | Start date of the exposure, only valid for PLTs and SF_PLTs                                                           |
| endDate                 | End date of the exposure, only valid for PLTs and SF_PLTs                                                             | 
| periodMin               | Starting Period number for a PLT or SF_PLT(usually set at 0)                                                          |
| periodMax               | Maximum Period Number for a PLT or SF_PLT.                                                                            | 


### Find Exposure 

This Call retrieves all Exposures available in the data library. Event loss tables, Period Loss Tables and Share factors. 

```python
import UserInfo
from commons.utils.clients import *
from apiclient.exposurelibrary.elt_client import *

Credentials = Clients.from_credentials(user_name=UserInfo.user_name, password=UserInfo.password, env=Environment.PROD)
Credentials.exposure.all(uuids=None,data_version_uuid='4b292524-d70c-4edb-9137-e9bc4bb41016',peril_uuid='4e2c16bc-1cf4-45e2-b7e5-86591b9802a2',
                         region_uuid='5b07643e-2bd8-4014-a837-569ab1ba1404',sub_region_resolution_uuid='7581d3ae-600b-44b4-85d9-27e821867792',
                        sub_peril_uuids=None,sub_region_uuids=None,lob_uuids=None,is_underlying_ilc=False,is_share_factor=False)
```
| Parameter                  | Description                                                                    |
|----------------------------|--------------------------------------------------------------------------------|
| uuids                      | When exposure Uuids are provided, call returns Exposure Object for all of them | 
| data_version_uuid          | Filters exposures by data version                                              | 
| peril_uuid                 | Filters exposures by data version                                              | 
| region_uuid                | Filters exposures by peril_Uuid                                                | 
| sub_region_resolution_uuid | Filters exposures by sub_region_resolution_uuid                                | 
| sub_peril_uuids            | Filters exposures by sub_peril_uuids                                           | 
| sub_region_uuids           | Filters exposures by sub_region_uuids                                          | 
| is_underlying_ilc          | is_underlying_ilc                                                              | 
| is_share_factor            | Filters exposures by exposures created as a share factor                       | 

<aside class="notice">
This call accepts one or a list of items for all the parameters mentioned above.
</aside>


```shell
curl -X 'GET' \
  'https://exposurelibrary.miuinsights.com/v1/exposures?dataVersionUuid=4b292524-d70c-4edb-9137-e9bc4bb41016&perilUuid=4e2c16bc-1cf4-45e2-b7e5-86591b9802a2&regionUuid=5b07643e-2bd8-4014-a837-569ab1ba1404&subRegionResolutionUuid=7581d3ae-600b-44b4-85d9-27e821867792&isUnderlyingIlc=false&isShareFactor=false&emptySubPerils=true' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer 8YvIkh61xaRL2T3oAtAShzqMeHfSPVkSAKiPHGog'
```


> Response

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



| Parameter | Description                                  |
|-----------|----------------------------------------------|
| eventId   | Id provided by RMS for every event           | 





### Find exposure's Peril & Region

This call returns the Peril/Region for an exposure Uuid.

```python
import UserInfo
from commons.utils.clients import *

pd.set_option('expand_frame_repr', False)

Credentials  = Clients.from_credentials(user_name=UserInfo.user_name, password=UserInfo.password, env=Environment.PROD)
Peri_Region = Credentials.exposure.peril_regions('fb1601a0-328c-4e8a-864d-1c157555559d')
```

```shell
curl -X 'GET' \
  'https://exposurelibrary.miuinsights.com/v1/exposures/perilsRegions?uuid=fb1601a0-328c-4e8a-864d-1c157555559d' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer 8fz8TyfbI0KI6y1BCjkMNs9LFHxZyBduTOMQsgFK'
```
> Response

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

An Event Loss Table (ELT) is an important RMS modelling concept. This table contains all simulated events (windstorms, earthquakes, etc.) present in RMS models and includes the corresponding losses that those events cause to a given security or client portfolio. The event identifiers are a constant set of IDs per peril region so that correlation between events can be captured and users can compare losses caused by the same events to different securities/portfolios.


### ELT Object

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

| Attributes              | Description                                                                                                      |
|-------------------------|------------------------------------------------------------------------------------------------------------------|
| uuid                    | Universal Unique identifier for the ELT.                                                                         | 
| companyUuid             | Universal Unique identifier of Company that was used to create the ELT, all public deals have an RMS companyUuid | 
| isPublic                | True if the ELT is public and shared by RMS as an ILC or part of 144A deals exposure                             |
| createdBy               | Universal Unique identifier of user that created the ELT                                                         | 
| createdAt               | Date of creation                                                                                                 |
| description             | ELT's Description                                                                                                |
| dataVersionUuids        | Data-version with which the ELT was created, some ELTs could have more than one data version                     | 
| unitCode                | Currency code                                                                                                    |
| perilUuid               | Unique Peril identifier across all Regions                                                                       |
| regionUuid              | Unique Region identifier across all Regions                                                                      | 
| subRegionResolutionUuid | Universal Unique identifier of the subregion associated with this ELT.                                           |
| subPerilUuids           | Universal Unique identifier for sub perils assigned to this ELT.                                                 | 
| subRegionUuids          | Universal Unique identifiers of sub regions assigned to this ELT.                                                |
| lobUuids                | Universal Unique identifier for lines of businesses assigned to this ELT                                         | 
| rowcount                | Number of rows; Number of events in the ELT                                                                      | 
| isIlc                   | True if the ELT is an Industry Loss curves shared by RMS                                                         |




### Find ELTs


```python
import UserInfo
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
> Response

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
| Parameter                 | Description                                                                        |
|---------------------------|------------------------------------------------------------------------------------|
| data_version_uuid         | Filters ELT library by data version                                                | 
| is_public                 | If true returns public ELTs shared by RMS as part of 144A deals or ILC if licensed | 
| is_ilc                    | If true returns ELTs built using ILc or ELT-ILC shared by RMS if licensed          | 


### Delete ELT 

Delete ELT UUID: This call deletes an existing ELT using its UUID.

```python
import UserInfo
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
> Response

```json

```
| Parameter | Description                       |
|-----------|-----------------------------------|
| ELT Uuid  | Universal Unique identifier for the ELT.    | 


### Find ELT by providing specific ELT UUID

This call provides detailed description and information for an ELT.

```python
import UserInfo
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
### ELT Data Object

> ELT Data Object

```json
[
  {
    "eventId": "1510001",
    "rate": 0.26696619,
    "stdDevCorrelated": 401.13,
    "stdDevIndependent": 12968.51,
    "totalExposure": 22785298,
    "mean": 573.59
  }
]
```

The ELT stores the following information for each event that generates a non-zero loss: 
- Event ID – the unique event identifier consistent across peril region
- Mean Loss – the amount of loss  Standard Deviation – measure of uncertainty 
- Standard Deviation: measure of uncertainty
- Exposure Value – this value represents the maximum possible loss
- Annual Rate – the probability of a given event occurring 



### Find ELT Data by providing specific ELT UUID

This call provides the  Event Loss table/Data for the ELT UUID provided. You can limit the nymber of rows returned by providing a limit and an offset

```python
import UserInfo
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


| Parameter | Description                              |
|-----------|------------------------------------------|
| ELT Uuid  | Universal Unique identifier for the ELT. | 
| Limit     | Limit number of rows returned            | 


## HD-PLT

An HD Period Loss Table (PLT) is a set of data consisting of:
Loss results generated by an HD model are stored in a period loss table (PLT). The PLT is a more generalized version of the year loss table (YLT), but unlike the YLT, it is not constrained to a one-year period. Each period within a PLT can span up to six consecutive years if the underlying exposure contains policies with dates ranging up to six years. For most portfolios, policies span only one year, and in these cases, a PLT is treated the same as a YLT.
In a PLT, the instances of an event ID in conjunction with the period weight informs primary uncertainty. The weight represents the likelihood that one period occurs rather than the other periods in the PLT. For non-earthquake HD models, all periods are equally weighted and are calculated as one (1) divided by the number of simulation periods used for the analysis. For earthquake models, the weight can vary by period and is derived during the development of the period event table (PET). The PET is the master list that includes which events happen in what period and on what day.
Every row in the PLT represents an event that causes damage, and therefore loss, to the exposure being analyzed. Secondary uncertainty, or the range of potential damage caused by the event, is not represented in the PLT using a specific field but is captured through the process of sampling the damage ratio from the underlying damage distribution. For more information about this process, see Ground Up Simulation.
The event is stamped with the date of the first day of the event and with the loss date that the policy pays out. The policy payout date is considered to be the day that the first location under the policy takes damage. For most perils the event and the loss date are the same, but for flood and wildfire models, these can differ.
The financial model takes the ground up PLT for each location coverage as an input.




# Contract
A Contract represents an individual ILS class or reinsurance layer (i.e. within a treaty or bond). There can be one or many contracts in a program.

## Contract Object

You can retrieve the Contract Object to view its properties, calculation template parameters, attached exposures, inured losses, and other metadata.

The structure varies from one Contract to another depending on the contract calculation template, the number of attached exposures, and the loss flow.


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
import UserInfo
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
| exposureUuid           | [Universal Unique identifier for the expusre](https://jdaif.github.io/slate/#exposure)                                             |
| latestRevisionOnly     | Filter by latest [revision](https://jdaif.github.io/slate/#program-revision-object) of every program                              | 


## Find a Contract

```python
import UserInfo
from commons.utils.clients import *
from apiclient.exposurelibrary.elt_client import *

Credentials = Clients.from_credentials(user_name=UserInfo.user_name, password=UserInfo.password, env=Environment.PROD)

Credentials.program.get_contract("4cbb2c8b-82d9-437a-9cfa-515a9dd91e77")

```

```shell

curl -X 'GET' \
  'https://contract.miuinsights.com/v2/contracts/4cbb2c8b-82d9-437a-9cfa-515a9dd91e77' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer 8fz8TyfbI0KI6y1BCjkMNs9LFHxZyBduTOMQsgFK'
```

> Response 

```json
{
  "name": "A",
  "verticalSeq": 0,
  "status": "OnRisk",
  "termCurrencyCode": "USD",
  "riskStartDate": "2021-07-01T00:00:00",
  "riskEndDate": "2025-06-30T23:59:59.999",
  "lossFlows": [
    {
      "lossType": "payout",
      "fromContractUuid": "b70eb13a-3c55-4f46-9d98-e87dc6847de5",
      "fromContract": "Class A-RP1"
    },
    {
      "lossType": "payout",
      "fromContractUuid": "1fa9e8dc-1d9d-49a0-9406-42f1b4dd9844",
      "fromContract": "Class A-RP4"
    },
    {
      "lossType": "payout",
      "fromContractUuid": "03f6913c-7ca2-48c0-8db8-4364ac914a7d",
      "fromContract": "Class A-RP2"
    },
    {
      "lossType": "payout",
      "fromContractUuid": "38f6bf53-69fe-475e-a1ca-49c0b6190e50",
      "fromContract": "Class A-RP3"
    }
  ],
  "exposures": [],
  "templateUuid": "aead0f2e-866a-4cc3-9a6b-72bed098bf01",
  "templateSubstitutions": {
    "InitialPayout": "0.0",
    "Attachment": "0",
    "Limit": "150000000",
    "Reinstatement": "0.0",
    "Principal": "150000000"
  },
  "uuid": "4cbb2c8b-82d9-437a-9cfa-515a9dd91e77",
  "isin": "US05826BAA44",
  "totalAmount": 150000000,
  "canParticipate": true,
  "metadata": []
}
```
| Parameter     | Description                       |
|---------------|-----------------------------------|
| Contract Uuid | Universal Unique identifier for a Contract. |



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

When a program object is retrieved, it may contain one or many [Program Revisions Objects](https://jdaif.github.io/slate/#program-revision-object)
The description for each program revision  returned by this call is less detailed than description obtained when calling the [Program Revisions Object](https://jdaif.github.io/slate/#program-revision-object) it does not include information about the Contracts or exposure.

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
The table below contains the attributes returned when calling a program object -- per revision

| attributes       | Description                                                                                                        |
|------------------|--------------------------------------------------------------------------------------------------------------------|
| uuid             | Program Uuid                                                                                                       | 
| revisionUuid     | Program Revision Uuid                                                                                              | 
| name             | Program name under that revision -could defer from one revision to another                                         |
| description      | Contains general description such as the source, year and cedant                                                   |
| status           | Draft/Finalized/Public specific to the entire program : [Program Status](https://jdaif.github.io/slate/#program)   |
| revisionStatus   | Draft/Finalized/Public specific to the program revision : [Program Status](https://jdaif.github.io/slate/#program) | 
| modifiedAt       | -                                                                                                                  | 
| modifiedBy       | Uuid of user that modified the program                                                                             |
| finalizedAt      | The date when the program revision was finalized                                                                   |
| finalizedBy      | Uuid of the user that finalized the revision                                                                       |
| companyUuid      | Specific to each company                                                                                           | 
| isPublic         | True/False if the program in general is public or not                                                              | 
| isPublicRevision | True/False if the program revision  is public or not                                                               |
| dataVersionUuids | Reflects the Data-versions of the exposure included in the program revision                                        |
## Program Revision Object

Program revision object lists 


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
| Attributes       | Description                                                                                                        |
|------------------|--------------------------------------------------------------------------------------------------------------------|
| uuid             | Program Uuid                                                                                                       | 
| revisionUuid     | Program Revision Uuid                                                                                              | 
| name             | Program name under that revision -could defer from one revision to another                                         |
| description      | Contains gerneral description such as the source                                                                   |
| status           | Draft/Finalized/Public specific to the entire program : [Program Status](https://jdaif.github.io/slate/#program)   |
| revisionStatus   | Draft/Finalized/Public specific to the program revision : [Program Status](https://jdaif.github.io/slate/#program) | 
| isPublic         | True/False if the program in general is public or not                                                              | 
| isPublicRevision | True/False if the program revision  is public or not                                                               |
| modifiedAt       | -                                                                                                                  | 
| modifiedBy       | Uuid of user that modified the program                                                                             |
| finalizedAt      | The date when the program revision was finalized                                                                   |
| finalizedBy      | Uuid of teh user that finalized the revision                                                                       |
| companyUuid      | Specific to each company                                                                                           | 
| inuringColumns   | Starting from 0 upward, each column would include a list of Contracts                                              | 
| contracts        | A list of [Contracts](https://jdaif.github.io/slate/#contract) under each column                                   |
| dataVersionUuids | Reflects the Dataversions of the exposure included in the program revision                                         |

### Inuring Columns & Loss Flow
Losses flow from left to right. Losses can inure from Contracts in one column to another but not within the same column.
What are Inuring Losses?
Inuring Losses consist of the Net Loss and Payout of a contract. They can be defined as Inputs to a subsequent contract
#### What is Net Loss?
Net Loss is the Loss remaining after the terms and conditions of a contract are applied. Net Loss data is in the form of a PLT.
#### What is Payout?
Payout is the Loss absorbed by the terms and conditions of a contract. Payout data is in the form of a PLT.

### Program Revisions Status

#### What are “Draft Programs”?

Programs with terms and conditions that are not confirmed should be left as “draft”. Draft programs can continue to be modified and edited. Each time you edit a program and save it, you will create a new version.


#### What are “Finalized Programs”?

Programs with terms and conditions that have been confirmed and signed should be “finalized”. Finalized programs can no longer be modified and will prevent further changes to be made.


#### What are “Public Programs”?

All the programs modelled by RMS that are available on the public market—i.e. 144a bonds.




## List all programs

This call retrieves all available programs in the deal library, user can filter by specifying the parameters below:

```python
import UserInfo
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
| Attributes      | Description                                            |
|-----------------|--------------------------------------------------------|
| status          | finalized/draft                                        | 
| public          | True/False                                             | 
| dataVersionUuid | Filter by Uuid                                         |
| uuid            | Program uuid                                           | 
| revisionUuid    | Program revision uuid                                  |
| cedenceType     | Programs with the given cedence type : Inward/outward  | 
| offset          | Offset the items returned                              |
| limit           | limit the number of items returned to a certain number | 
| sortBy          | Name, date modified ....                               |
| sortOrder       | asc/desc                                               | 
## Create a program

```python
Program_json= {

        "name": "Cat Bond 144a2",
        "revisionName": "6/10/2022, 5:32:13 PM",
        "description": {
            "source": "Original"
        },

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
                        "lossFlows": [

                        ],
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
                        "metadata": [

                        ]
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
                            }
                        ],
                        "exposures": [

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
                        "uuid": "9c3f1c9a-09b3-449f-825e-0a7807df85e3",
                        "totalAmount": 100000000,
                        "canParticipate": true,
                        "metadata": [

                        ]
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
import UserInfo
from commons.utils.clients import *
from apiclient.exposurelibrary.elt_client import *

Credentials = Clients.from_credentials(user_name=UserInfo.user_name, password=UserInfo.password, env=Environment.PROD)
Program = json.dumps(Program_json)

Credentials.program.create(Program)
```

```shell
curl -X 'POST' \
  'https://contract.miuinsights.com/v2/programs' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer KN8dy5b7OxuZR827EPKVp6SEepLHgQivy9Ec2JH8' \
  -d '{

        "name": "Cat Bond 144a2",
        "revisionName": "6/10/2022, 5:32:13 PM",
        "description": {
            "source": "Original"
        },

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
                        "lossFlows": [

                        ],
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
                        "metadata": [

                        ]
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
                            }
                        ],
                        "exposures": [

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
                        "uuid": "9c3f1c9a-09b3-449f-825e-0a7807df85e3",
                        "totalAmount": 100000000,
                        "canParticipate": true,
                        "metadata": [

                        ]
                    }
                ]
            }
        ],
        "dataVersionUuids": [
            "04446b5e-d16a-4023-b7e2-a9b519d801f3",
            "4b292524-d70c-4edb-9137-e9bc4bb41016"
        ],
        "isPltOnly": false

}'
```

| Parameter         | Description                                                                                                                             |
|-------------------|-----------------------------------------------------------------------------------------------------------------------------------------|
| name              | Program name: String                                                                                                                    | 
| public            | Program revision name: String                                                                                                           | 
| dataVersionUuid   | [Dataversion UUID](file:///C:/Users/jdaif/Documents/GitHub/slate/index.html?python#event): UUID                                         |
| source            | Original/Reset                                                                                                                          | 
| inuringColumns    | Contracts are listed under Inuring columns                                                                                              |
| contracts         | [Contracts](file:///C:/Users/jdaif/Documents/GitHub/slate/index.html?python#find-contracts) are listed under inuring columns            | 
| dataVersionUuids  | Offset the items returned                                                                                                               |
| isPltOnly         | limit the number of items returned to a certain number                                                                                  | 


## Get all program revision summary

Returns all private/public draft and private/public finalized program revisions within user's organization and all public finalized program revisions outside user's organization

```python
import UserInfo
from commons.utils.clients import *
from apiclient.exposurelibrary.elt_client import *

Credentials = Clients.from_credentials(user_name=UserInfo.user_name, password=UserInfo.password, env=Environment.PROD)
Service1.program.get_revisions_by_program_uuid("b857ae98-3dba-43e0-8627-fc365753727f")

```

```shell
curl -X 'GET' \
  'https://contract.miuinsights.com/v2/programs/b857ae98-3dba-43e0-8627-fc365753727f/revisions' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer HfUR2SL10frixvmy5BqcSUBgble2xv0X4EmSGV7m'
```
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
| Attributes       | Description                                                                                                        |
|------------------|--------------------------------------------------------------------------------------------------------------------|
| uuid             | Program Uuid                                                                                                       | 
| revisionUuid     | Program Revision Uuid                                                                                              | 
| name             | Program name under that revision -could defer from one revision to another                                         |
| description      | Contains gerneral description such as the source                                                                   |
| status           | Draft/Finalized/Public specific to the entire program : [Program Status](https://jdaif.github.io/slate/#program)   |
| revisionStatus   | Draft/Finalized/Public specific to the program revision : [Program Status](https://jdaif.github.io/slate/#program) | 
| isPublic         | True/False if the program in general is public or not                                                              | 
| isPublicRevision | True/False if the program revision  is public or not                                                               |
| modifiedAt       | -                                                                                                                  | 
| modifiedBy       | Uuid of user that modified the program                                                                             |
| finalizedAt      | The date when the program revision was finalized                                                                   |
| finalizedBy      | Uuid of teh user that finalized the revision                                                                       |
| companyUuid      | Specific to each company                                                                                           | 
| inuringColumns   | Starting from 0 upward, each column would include a list of Contracts                                              | 
| contracts        | A list of [Contracts](https://jdaif.github.io/slate/#contract) under each column                                   |
| dataVersionUuids | Reflects the Dataversions of the exposure included in the program revision                                         |


## Get the latest revision summary

```python
import UserInfo
from commons.utils.clients import *
from apiclient.exposurelibrary.elt_client import *

Credentials = Clients.from_credentials(user_name=UserInfo.user_name, password=UserInfo.password, env=Environment.PROD)
Service1.program.get_revisions_by_program_uuid("b857ae98-3dba-43e0-8627-fc365753727f")

```

```shell
curl -X 'GET' \
  'https://contract.miuinsights.com/v2/programs/b857ae98-3dba-43e0-8627-fc365753727f/revisions' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer HfUR2SL10frixvmy5BqcSUBgble2xv0X4EmSGV7m'
```

> Response


```json
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
  "isPublic": false,
  "isPublicRevision": false,
  "modifiedAt": "2022-06-28T05:36:13.222719Z",
  "modifiedBy": "323da914-7c9b-4a26-9110-8e0439df160f",
  "finalizedAt": "2022-06-28T05:36:42.800079Z",
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
          "uuid": "c5e61008-6060-4058-979f-cdca5bcba5cb",
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
              "exposureType": "PLT"
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
          "uuid": "3b802f32-bf78-4df1-96d6-2bb72d3f1c58",
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
              "fromContractUuid": "3b802f32-bf78-4df1-96d6-2bb72d3f1c58",
              "fromContract": "Cat Bond 144a Flood",
              "primitiveBody": "Scale by 1.05"
            },
            {
              "lossType": "payout",
              "fromContractUuid": "c5e61008-6060-4058-979f-cdca5bcba5cb",
              "fromContract": "Cat Bond 144a WS"
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
          "uuid": "05ea549f-1b90-4c30-b7af-338e549cbce7",
          "totalAmount": 100000000,
          "canParticipate": true,
          "metadata": []
        },
        {
          "name": "C",
          "verticalSeq": 1,
          "status": "Written",
          "termCurrencyCode": "USD",
          "riskStartDate": "2022-01-01T00:00:00",
          "riskEndDate": "2022-12-31T23:59:59.999",
          "lossFlows": [
            {
              "lossType": "payout",
              "fromContractUuid": "c5e61008-6060-4058-979f-cdca5bcba5cb",
              "fromContract": "Cat Bond 144a WS"
            },
            {
              "lossType": "payout",
              "fromContractUuid": "3b802f32-bf78-4df1-96d6-2bb72d3f1c58",
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
          "uuid": "7e5a759a-603d-4ae0-991c-da1747335781",
          "totalAmount": 100000000,
          "canParticipate": true,
          "metadata": []
        },
        {
          "name": "B",
          "verticalSeq": 2,
          "status": "Written",
          "termCurrencyCode": "USD",
          "riskStartDate": "2022-01-01T00:00:00",
          "riskEndDate": "2022-12-31T23:59:59.999",
          "lossFlows": [
            {
              "lossType": "payout",
              "fromContractUuid": "c5e61008-6060-4058-979f-cdca5bcba5cb",
              "fromContract": "Cat Bond 144a WS"
            },
            {
              "lossType": "payout",
              "fromContractUuid": "3b802f32-bf78-4df1-96d6-2bb72d3f1c58",
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
          "uuid": "a5201441-a5bf-42dc-ab85-2a6595e05f05",
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
  "isShared": false,
  "metadata": [],
  "isPltOnly": false
}
```

| Attributes       | Description                                                                                                        |
|------------------|--------------------------------------------------------------------------------------------------------------------|
| uuid             | Program Uuid                                                                                                       | 
| revisionUuid     | Program Revision Uuid                                                                                              | 
| name             | Program name under that revision -could defer from one revision to another                                         |
| description      | Contains gerneral description such as the source                                                                   |
| status           | Draft/Finalized/Public specific to the entire program : [Program Status](https://jdaif.github.io/slate/#program)   |
| revisionStatus   | Draft/Finalized/Public specific to the program revision : [Program Status](https://jdaif.github.io/slate/#program) | 
| isPublic         | True/False if the program in general is public or not                                                              | 
| isPublicRevision | True/False if the program revision  is public or not                                                               |
| modifiedAt       | -                                                                                                                  | 
| modifiedBy       | Uuid of user that modified the program                                                                             |
| finalizedAt      | The date when the program revision was finalized                                                                   |
| finalizedBy      | Uuid of teh user that finalized the revision                                                                       |
| companyUuid      | Specific to each company                                                                                           | 
| inuringColumns   | Starting from 0 upward, each column would include a list of Contracts                                              | 
| contracts        | A list of [Contracts](https://jdaif.github.io/slate/#contract) under each column                                   |
| dataVersionUuids | Reflects the Dataversions of the exposure included in the program revision                                         |

## Delete specific program revision
```python
import UserInfo
from commons.utils.clients import *
from apiclient.exposurelibrary.elt_client import *

Credentials = Clients.from_credentials(user_name=UserInfo.user_name, password=UserInfo.password, env=Environment.PROD)
Credentials.program.delete_revision("2b7912db-1274-46a7-8fa2-2fbcd65a55a8")

```

```shell
curl -X 'DELETE' \
  'https://contract.miuinsights.com/v2/programs/revisions/2b7912db-1274-46a7-8fa2-2fbcd65a55a8' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer HfUR2SL10frixvmy5BqcSUBgble2xv0X4EmSGV7m'
```

> Response

| Parameter             | Description                                      |
|-----------------------|--------------------------------------------------|
| Program Revision Uuid | Universal Unique identifier per program revision |

## Delete a program
Deletes regardless of public status

```python
import UserInfo
from commons.utils.clients import *
from apiclient.exposurelibrary.elt_client import *

Credentials = Clients.from_credentials(user_name=UserInfo.user_name, password=UserInfo.password, env=Environment.PROD)
Credentials.program.delete("07deb9d1-b4c3-4402-9cba-24b568484f0a")

```

```shell
curl -X 'DELETE' \
  'https://contract.miuinsights.com/v2/programs/07deb9d1-b4c3-4402-9cba-24b568484f0a' \
  -H 'accept: */*' \
  -H 'Authorization: Bearer HfUR2SL10frixvmy5BqcSUBgble2xv0X`4EmSGV7m'
```

```JSON


```



| Parameter     | Description                             |
|---------------|-----------------------------------------|
| Program  Uuid | Universal Unique identifier per program |


# Portfolio

## Portfolio Object
Similar to programs, portfolios have one or more portfolio revisions. The portfolio Object returns a list of different Portfolio revisions.

> Portfolio Object 

```json
[
  {
    "uuid": "531dfe38-455a-4807-ad8e-c1e20d470b03",
    "portfolioUuid": "601cf6db-8bc7-4bc7-bc0d-3c222a2a69ac",
    "dataVersionUuids": [
      "04446b5e-d16a-4023-b7e2-a9b519d801f3",
      "4b292524-d70c-4edb-9137-e9bc4bb41016"
    ],
    "createdBy": "323da914-7c9b-4a26-9110-8e0439df160f",
    "modifiedBy": "323da914-7c9b-4a26-9110-8e0439df160f",
    "createdAt": "2022-07-19T02:30:44.590104Z",
    "modifiedAt": "2022-07-19T02:30:44.590104Z",
    "metadata": []
  },
  {
    "uuid": "03520503-5926-46d1-ad57-54df22cabfcd",
    "portfolioUuid": "601cf6db-8bc7-4bc7-bc0d-3c222a2a69ac",
    "dataVersionUuids": [
      "04446b5e-d16a-4023-b7e2-a9b519d801f3",
      "4b292524-d70c-4edb-9137-e9bc4bb41016"
    ],
    "createdBy": "323da914-7c9b-4a26-9110-8e0439df160f",
    "modifiedBy": "323da914-7c9b-4a26-9110-8e0439df160f",
    "createdAt": "2022-07-19T02:33:47.577860Z",
    "modifiedAt": "2022-07-19T02:33:47.577860Z",
    "metadata": []
  },
  {
    "uuid": "712377ea-9f08-466e-8207-c1c21ea1d42a",
    "portfolioUuid": "601cf6db-8bc7-4bc7-bc0d-3c222a2a69ac",
    "dataVersionUuids": [
      "04446b5e-d16a-4023-b7e2-a9b519d801f3",
      "4b292524-d70c-4edb-9137-e9bc4bb41016"
    ],
    "createdBy": "323da914-7c9b-4a26-9110-8e0439df160f",
    "modifiedBy": "323da914-7c9b-4a26-9110-8e0439df160f",
    "createdAt": "2022-07-19T02:34:04.061515Z",
    "modifiedAt": "2022-07-19T02:34:04.061515Z",
    "metadata": []
  },
  {
    "uuid": "008fa0da-780b-4c72-943b-ea60a4f84b90",
    "portfolioUuid": "601cf6db-8bc7-4bc7-bc0d-3c222a2a69ac",
    "dataVersionUuids": [
      "04446b5e-d16a-4023-b7e2-a9b519d801f3",
      "4b292524-d70c-4edb-9137-e9bc4bb41016"
    ],
    "createdBy": "323da914-7c9b-4a26-9110-8e0439df160f",
    "modifiedBy": "323da914-7c9b-4a26-9110-8e0439df160f",
    "createdAt": "2022-07-19T02:34:03.633399Z",
    "modifiedAt": "2022-07-19T02:34:03.633399Z",
    "metadata": []
  }
]
```
| Attributes       | Description                                                         |
|------------------|---------------------------------------------------------------------|
| uuid             | Portfolio Revision Uuid                                             | 
| portfolioUuid    | Portfolio Uuid                                                      | 
| dataVersionUuids | Data versions of Contracts assigned to the Portfolio                |
| createdBy        | Uuid of Portfolio creator                                           |
| modifiedBy       | Uuid of Portfolio Portfolio modifier or Revision creator            |
| createdAt        | Date of creation of Portfolio                                       | 
| modifiedAt       | Date of modification of Portfolio or creation of Portfolio revision | 


## Portfolio Revision Object


> Portfolio Revision Object 

```json
{
  "portfolioUuid": "601cf6db-8bc7-4bc7-bc0d-3c222a2a69ac",
  "name": "Cat Bond 144a",
  "modifiedAt": "2022-07-19T02:34:04.054860Z",
  "revisionModifiedAt": "2022-07-19T02:30:44.590104Z",
  "modifiedBy": "323da914-7c9b-4a26-9110-8e0439df160f",
  "revisionModifiedBy": "323da914-7c9b-4a26-9110-8e0439df160f",
  "createdAt": "2022-07-19T02:30:44.590104Z",
  "createdBy": "323da914-7c9b-4a26-9110-8e0439df160f",
  "companyUuid": "efa36b93-3200-40a7-afe6-709a2a565c1a",
  "dataVersionUuids": [
    "04446b5e-d16a-4023-b7e2-a9b519d801f3",
    "4b292524-d70c-4edb-9137-e9bc4bb41016"
  ],
  "contractsByProgram": [
    {
      "programRevisionUuid": "d25fcc79-8457-486d-b2ef-924d2af1a66d",
      "programName": "Cat Bond 144a",
      "programRevisionName": "6/27/2022, 10:36:13 PM",
      "programRevisionSource": "Original",
      "dataVersionUuids": [
        "04446b5e-d16a-4023-b7e2-a9b519d801f3",
        "4b292524-d70c-4edb-9137-e9bc4bb41016"
      ],
      "isPublic": false,
      "contracts": [
        {
          "uuid": "9eebd83c-7a62-44ca-8440-4dcf17b699ce",
          "name": "A",
          "termCurrencyCode": "USD",
          "participation": 100000000,
          "canParticipate": true,
          "riskStartDate": "2022-01-01T00:00:00",
          "riskEndDate": "2022-12-31T23:59:59.999",
          "totalAmount": 100000000,
          "isLatestFinalizedRevision": true
        },
        {
          "uuid": "776d7916-8f1a-48d8-bc92-63f5356f9a1a",
          "name": "B",
          "termCurrencyCode": "USD",
          "participation": 100000000,
          "canParticipate": true,
          "riskStartDate": "2022-01-01T00:00:00",
          "riskEndDate": "2022-12-31T23:59:59.999",
          "totalAmount": 100000000,
          "isLatestFinalizedRevision": true
        }
      ]
    }
  ],
  "metadata": [],
  "isPltOnly": false
}
```
| Attributes         | Description                                                                                                                                                                |
|--------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| portfolioUuid      | Universal Unique identifier of a Portfolio                                                                                                                                 | 
| name               | Portfolio name                                                                                                                                                             | 
| modifiedAt         | Date of modification of Portfolio                                                                                                                                          |
| revisionModifiedAt | Date of modification of Portfolio Revision                                                                                                                                 |
| modifiedBy         | Uuid of Portfolio revision creator/ Portfolio modifier                                                                                                                     |
| createdAt          | Date of creation of Portfolio                                                                                                                                              | 
| createdBy          | Uuid of user that created the portfolio                                                                                                                                    | 
| dataVersionUuids   | Uuids for data versions of Contracts included in the Portfolio Revision                                                                                                    |
| contractsByProgram | List of [Contracts](https://jdaif.github.io/slate/?python#contract) included in the Portfolio grouped by [program revision](https://jdaif.github.io/slate/?python#program) |
| metadata           | -                                                                                                                                                                          | 
| isPltOnly          | True if Portfolio revision contains PLT exposure only                                                                                                                      | 
#### contractsByProgram


> contractsByProgram Object 

```json
 [
    {
      "programRevisionUuid": "d25fcc79-8457-486d-b2ef-924d2af1a66d",
      "programName": "Cat Bond 144a",
      "programRevisionName": "6/27/2022, 10:36:13 PM",
      "programRevisionSource": "Original",
      "dataVersionUuids": [
        "04446b5e-d16a-4023-b7e2-a9b519d801f3",
        "4b292524-d70c-4edb-9137-e9bc4bb41016"
      ],
      "isPublic": false,
      "contracts": [
        {
          "uuid": "9eebd83c-7a62-44ca-8440-4dcf17b699ce",
          "name": "A",
          "termCurrencyCode": "USD",
          "participation": 100000000,
          "canParticipate": true,
          "riskStartDate": "2022-01-01T00:00:00",
          "riskEndDate": "2022-12-31T23:59:59.999",
          "totalAmount": 100000000,
          "isLatestFinalizedRevision": true
        },
        {
          "uuid": "776d7916-8f1a-48d8-bc92-63f5356f9a1a",
          "name": "B",
          "termCurrencyCode": "USD",
          "participation": 100000000,
          "canParticipate": true,
          "riskStartDate": "2022-01-01T00:00:00",
          "riskEndDate": "2022-12-31T23:59:59.999",
          "totalAmount": 100000000,
          "isLatestFinalizedRevision": true
        }
      ]
    }
]

```
| Attributes            | Description                                                                                             |
|-----------------------|---------------------------------------------------------------------------------------------------------|
| programRevisionUuid   | [Program Revision UUid](https://jdaif.github.io/slate/?python#program-revision-object)                  | 
| programName           | [Program Name](https://jdaif.github.io/slate/?python#program-object)                                    | 
| programRevisionName   | [Program Revision Name](https://jdaif.github.io/slate/?python#program-revision-object)                  |
| programRevisionSource | Original/Reset [Program Revision source](https://jdaif.github.io/slate/?python#program-revision-object) |
| dataVersionUuids      | Uuids for data versions of Contracts included in the Program Revision                                   |
| isPublic              | True if Program is public                                                                               | 
| contracts             | List of available [Contracts](https://jdaif.github.io/slate/?python#contract)                           | 

## Find portfolio

```python
import UserInfo
from commons.utils.clients import *
from apiclient.exposurelibrary.elt_client import *

Credentials = Clients.from_credentials(user_name=UserInfo.user_name, password=UserInfo.password, env=Environment.PROD)
Credentials.portfolio.all(program_revision_uuid="d25fcc79-8457-486d-b2ef-924d2af1a66d",portfolio_uuids="601cf6db-8bc7-4bc7-bc0d-3c222a2a69ac")

```

```shell
curl -X 'GET' \
  'https://contract.miuinsights.com/v2/portfolios?programRevisionUuid=d25fcc79-8457-486d-b2ef-924d2af1a66d&uuid=601cf6db-8bc7-4bc7-bc0d-3c222a2a69ac&dataVersionUuid=4b292524-d70c-4edb-9137-e9bc4bb41016' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer QC6f6uhFdykBmmT9wXBDfTpACyScORaTtLnIVmkg'
```

> Response 


```JSON
[
  {
    "uuid": "601cf6db-8bc7-4bc7-bc0d-3c222a2a69ac",
    "revisionUuid": "712377ea-9f08-466e-8207-c1c21ea1d42a",
    "name": "Cat Bond 144a",
    "companyUuid": "efa36b93-3200-40a7-afe6-709a2a565c1a",
    "dataVersionUuids": [
      "4b292524-d70c-4edb-9137-e9bc4bb41016"
    ],
    "metadata": [],
    "createdBy": "323da914-7c9b-4a26-9110-8e0439df160f",
    "createdAt": "2022-07-19T02:30:44.590104Z",
    "modifiedBy": "323da914-7c9b-4a26-9110-8e0439df160f",
    "modifiedAt": "2022-07-19T02:34:04.054860Z",
    "isPltOnly": false
  }
]

```


| Parameter             | Description                                                              |
|-----------------------|--------------------------------------------------------------------------|
| Program Revision Uuid | Filters down Portfolio Library to Portfolios containing Program Revision |
| Portfolio  Uuid       | Filter Portfolio Library by Portfolio Uuids                              |
| Data version  Uuid    | Filter Portfolio Library by data versions                                |

## Find latest portfolio revision
```python
import UserInfo
from commons.utils.clients import *
from apiclient.exposurelibrary.elt_client import *

Credentials = Clients.from_credentials(user_name=UserInfo.user_name, password=UserInfo.password, env=Environment.PROD)
Credentials.portfolio.get_latest_revision("601cf6db-8bc7-4bc7-bc0d-3c222a2a69ac")

```

```shell
curl -X 'GET' \
  'https://contract.miuinsights.com/v2/portfolios/601cf6db-8bc7-4bc7-bc0d-3c222a2a69ac/revisions/latest' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer QC6f6uhFdykBmmT9wXBDfTpACyScORaTtLnIVmkg'
```


> Response 


```JSON
{
  "uuid": "712377ea-9f08-466e-8207-c1c21ea1d42a",
  "portfolioUuid": "601cf6db-8bc7-4bc7-bc0d-3c222a2a69ac",
  "dataVersionUuids": [
    "04446b5e-d16a-4023-b7e2-a9b519d801f3",
    "4b292524-d70c-4edb-9137-e9bc4bb41016"
  ],
  "createdBy": "323da914-7c9b-4a26-9110-8e0439df160f",
  "modifiedBy": "323da914-7c9b-4a26-9110-8e0439df160f",
  "createdAt": "2022-07-19T02:34:04.061515Z",
  "modifiedAt": "2022-07-19T02:34:04.061515Z",
  "metadata": []
}

```



| Parameter       | Description                                 |
|-----------------|---------------------------------------------|
| Portfolio  Uuid | Universal Unique identifier per portfolio   |


## Find portfolio revisions

```python
import UserInfo
from commons.utils.clients import *
from apiclient.exposurelibrary.elt_client import *

Credentials = Clients.from_credentials(user_name=UserInfo.user_name, password=UserInfo.password, env=Environment.PROD)
Credentials.portfolio.get_revisions("601cf6db-8bc7-4bc7-bc0d-3c222a2a69ac")

```

```shell
curl -X 'GET' \
  'https://contract.miuinsights.com/v2/portfolios/601cf6db-8bc7-4bc7-bc0d-3c222a2a69ac/revisions' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer QC6f6uhFdykBmmT9wXBDfTpACyScORaTtLnIVmkg'
```

> Response 


```JSON
[
  {
    "uuid": "531dfe38-455a-4807-ad8e-c1e20d470b03",
    "portfolioUuid": "601cf6db-8bc7-4bc7-bc0d-3c222a2a69ac",
    "dataVersionUuids": [
      "04446b5e-d16a-4023-b7e2-a9b519d801f3",
      "4b292524-d70c-4edb-9137-e9bc4bb41016"
    ],
    "createdBy": "323da914-7c9b-4a26-9110-8e0439df160f",
    "modifiedBy": "323da914-7c9b-4a26-9110-8e0439df160f",
    "createdAt": "2022-07-19T02:30:44.590104Z",
    "modifiedAt": "2022-07-19T02:30:44.590104Z",
    "metadata": []
  },
  {
    "uuid": "008fa0da-780b-4c72-943b-ea60a4f84b90",
    "portfolioUuid": "601cf6db-8bc7-4bc7-bc0d-3c222a2a69ac",
    "dataVersionUuids": [
      "04446b5e-d16a-4023-b7e2-a9b519d801f3",
      "4b292524-d70c-4edb-9137-e9bc4bb41016"
    ],
    "createdBy": "323da914-7c9b-4a26-9110-8e0439df160f",
    "modifiedBy": "323da914-7c9b-4a26-9110-8e0439df160f",
    "createdAt": "2022-07-19T02:34:03.633399Z",
    "modifiedAt": "2022-07-19T02:34:03.633399Z",
    "metadata": []
  }
]

```



| Parameter       | Description                                |
|-----------------|--------------------------------------------|
| Portfolio  Uuid | Universal Unique identifier per portfolio  |

## Find Portfolio Revision

```python
import UserInfo
from commons.utils.clients import *
from apiclient.exposurelibrary.elt_client import *

Credentials = Clients.from_credentials(user_name=UserInfo.user_name, password=UserInfo.password, env=Environment.PROD)
Credentials.portfolio.get_by_revision_uuid("531dfe38-455a-4807-ad8e-c1e20d470b03")

```

```shell
curl -X 'GET' \
  'https://contract.miuinsights.com/v2/portfolios/revisions/531dfe38-455a-4807-ad8e-c1e20d470b03' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer QC6f6uhFdykBmmT9wXBDfTpACyScORaTtLnIVmkg'
```

> Response 



```JSON
{
  "portfolioUuid": "601cf6db-8bc7-4bc7-bc0d-3c222a2a69ac",
  "name": "Cat Bond 144a",
  "modifiedAt": "2022-07-19T02:34:04.054860Z",
  "revisionModifiedAt": "2022-07-19T02:30:44.590104Z",
  "modifiedBy": "323da914-7c9b-4a26-9110-8e0439df160f",
  "revisionModifiedBy": "323da914-7c9b-4a26-9110-8e0439df160f",
  "createdAt": "2022-07-19T02:30:44.590104Z",
  "createdBy": "323da914-7c9b-4a26-9110-8e0439df160f",
  "companyUuid": "efa36b93-3200-40a7-afe6-709a2a565c1a",
  "dataVersionUuids": [
    "04446b5e-d16a-4023-b7e2-a9b519d801f3",
    "4b292524-d70c-4edb-9137-e9bc4bb41016"
  ],
  "contractsByProgram": [
    {
      "programRevisionUuid": "d25fcc79-8457-486d-b2ef-924d2af1a66d",
      "programName": "Cat Bond 144a",
      "programRevisionName": "6/27/2022, 10:36:13 PM",
      "programRevisionSource": "Original",
      "dataVersionUuids": [
        "04446b5e-d16a-4023-b7e2-a9b519d801f3",
        "4b292524-d70c-4edb-9137-e9bc4bb41016"
      ],
      "isPublic": false,
      "contracts": [
        {
          "uuid": "9eebd83c-7a62-44ca-8440-4dcf17b699ce",
          "name": "A",
          "termCurrencyCode": "USD",
          "participation": 100000000,
          "canParticipate": true,
          "riskStartDate": "2022-01-01T00:00:00",
          "riskEndDate": "2022-12-31T23:59:59.999",
          "totalAmount": 100000000,
          "isLatestFinalizedRevision": true
        },
        {
          "uuid": "776d7916-8f1a-48d8-bc92-63f5356f9a1a",
          "name": "B",
          "termCurrencyCode": "USD",
          "participation": 100000000,
          "canParticipate": true,
          "riskStartDate": "2022-01-01T00:00:00",
          "riskEndDate": "2022-12-31T23:59:59.999",
          "totalAmount": 100000000,
          "isLatestFinalizedRevision": true
        }
      ]
    }
  ],
  "metadata": [],
  "isPltOnly": false
}

```



| Parameter               | Description                                          |
|-------------------------|------------------------------------------------------|
| Portfolio Revision Uuid | Universal Unique identifier per portfolio revision   |

## Create portfolio



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
| Attributes            | Description                                                           |
|-----------------------|-----------------------------------------------------------------------|
| analysisUuid          | Universal Unique identifier for analysis                              | 
| analysisName          | Analysis Name                                                         | 
| jobCreationDate       | Date of submission of analysis                                        |
| jobStartDate          | Start Date-time of analysis                                           | 
| jobEndDate            | Start Date-time of analysis                                           |
| companyUuid           | Universal Unique identifier of the company that created the analysis  | 
| userUuid              | Universal Unique identifier of the user that created the analysis     |
| status                | FINISHED/Waiting/Canceled                                             | 
| analysisType          | simulated vs Deterministic                                            |
| startDate             | Simulation date-time start                                            | 
| endDate               | Simulation date-time end                                              | 
| periodStart           | Usually set at 0                                                      | 
| periodEnd             | Number of simulated Periods                                           | 
| stochasticYltUuids    | Universal Unique identifiers of YLTs used in the simulation           | 
| programUuid           | [Program Uuid]() if the analysis was run on a program                 | 
| programRevisionUuid   | [Program Revision Uuid]() if the analysis was run on a program        | 
| portfolioUuid         | [Portfolio Uuid]() if the analysis was run on a Portfolio             | 
| portfolioRevisionUuid | [Portfolio Revision Uuid]() if the analysis was run on a Portfolio    | 
| cplts                 | A list of the CPLTs genearted by the analysis                         | 
| currencySetUuid       | Currency set selected for currency exchange when running the analysis | 
| complexityScore       | Score generated by the Financial Engine to allocate cluster size      | 
| totalContracts        | Total number of Contracts in the analysis                             | 
| outputs               | A list of the CPLTs genearted by the analysis                         | 
| currencyCode          | Output Currency selected when running the analysis                    | 



## Find analysis
When we run an analysis, a JSON that contains all the descriptions for that analysis gets created. This JSON contains information such as analysis name, start date, analysis end date, profiles used, the Uuid of the CPLTs generated for that analysis, and others.
Below are some codes that return organized structured pieces of that JSON.


```python
import UserInfo
from commons.utils.clients import *
from apiclient.exposurelibrary.elt_client import *

Credentials = Clients.from_credentials(user_name=UserInfo.user_name, password=UserInfo.password, env=Environment.PROD)
Credentials.analysis.get_analysis_by_uuid('31d6a477-fcc2-4d2f-bb4c-71d9d7aa393b')

```

```shell
curl -X 'GET' \
  'https://analysis.miuinsights.com/v3/analyses/31d6a477-fcc2-4d2f-bb4c-71d9d7aa393b' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer QC6f6uhFdykBmmT9wXBDfTpACyScORaTtLnIVmkg'
```

> Response 


```JSON
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



| Parameter      | Description                               |
|----------------|-------------------------------------------|
| analysis  Uuid | Universal Unique identifier by analysis   |


## Get CPLT
In Miu Contracts, the analysis runs on a Portfolio or a Program; each is a combination of one or many Contracts(Could be thousands). The result table(CPLT) lists the events in each simulated analysis period, the occurrence date, and the corresponding gross loss. Those losses get broken down to the underlying exposure level for each event. And so every row produced would have the following:

### CPLT Data Object

> Response 



```JSON
{
    "cpltUuid": "c65d8ed0-7834-4f28-a8ff-01b4043b113f",
    "date": "2022-09-28T00:00:01",
    "eventId": 2873023,
    "exposureUuid": "99c2a627-1cc0-4581-b1e0-3cb72e9d788d",
    "periodNumber": 1,
    "payout": 100000000,
    "lossQuantile": 0.410706755006686
  }

```
| Attributes   | Description                                                                                              |
|--------------|----------------------------------------------------------------------------------------------------------|
| cpltUuid     | Universal Unique identifier for a CPLT                                                                   |
| date         | Date-time of the loss occurrence                                                                         |
| eventId      | -                                                                                                        |
| exposureUuid | Uuid of the [Exposure](https://jdaif.github.io/slate/?python#exposure) that contained the event          |
| periodNumber | Simulation Period that produced that Loss                                                                |
| payout       | Value amount of the loss                                                                                 |
| lossQuantile | Loss Quantile from the YLT                                                                               |


### Get CPLT by Analysis 

```python
import UserInfo
from commons.utils.clients import *
from apiclient.exposurelibrary.elt_client import *

Credentials = Clients.from_credentials(user_name=UserInfo.user_name, password=UserInfo.password, env=Environment.PROD)
Credentials.analysis.get_cplt_data('31d6a477-fcc2-4d2f-bb4c-71d9d7aa393b')

```

```shell
curl -X 'GET' \
  'https://analysis.miuinsights.com/v3/analyses/31d6a477-fcc2-4d2f-bb4c-71d9d7aa393b' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer QC6f6uhFdykBmmT9wXBDfTpACyScORaTtLnIVmkg'
```

> Response 


```JSON
[
  {
    "cpltUuid": "c65d8ed0-7834-4f28-a8ff-01b4043b113f",
    "date": "2022-09-28T00:00:01",
    "eventId": 2873023,
    "exposureUuid": "99c2a627-1cc0-4581-b1e0-3cb72e9d788d",
    "periodNumber": 1,
    "payout": 100000000,
    "lossQuantile": 0.410706755006686
  },
  {
    "cpltUuid": "343000f2-3a3a-4c1b-a16f-d365a64e6619",
    "date": "2022-09-28T00:00:01",
    "eventId": 2873023,
    "exposureUuid": "99c2a627-1cc0-4581-b1e0-3cb72e9d788d",
    "periodNumber": 1,
    "payout": 100000000,
    "lossQuantile": 0.410706755006686
  },
  {
    "cpltUuid": "1d5b3c13-21c9-47c6-a907-09f05f7bbd44",
    "date": "2022-09-28T00:00:01",
    "eventId": 2873023,
    "exposureUuid": "99c2a627-1cc0-4581-b1e0-3cb72e9d788d",
    "periodNumber": 1,
    "payout": 100000000,
    "lossQuantile": 0.410706755006686
  }
]

```



| Parameter      | Description                               |
|----------------|-------------------------------------------|
| analysis  Uuid | Universal Unique identifier by analysis   |


<aside class="success">
In this json, the CPLT data output was limited to 1 period
</aside>

### Get CPLT by CPLT Uuid

Instead of retrieving the CPLT for the entire analysis, we can limit it to a specific contract by providing its CPLT Uuid


```python
import UserInfo
from commons.utils.clients import *
from apiclient.exposurelibrary.elt_client import *

Credentials = Clients.from_credentials(user_name=UserInfo.user_name, password=UserInfo.password, env=Environment.PROD)
Credentials.analysis.get_cplt_data_via_uuid('31d6a477-fcc2-4d2f-bb4c-71d9d7aa393b')

```

```shell
curl -X 'GET' \
  'https://analysis.miuinsights.com/v3/cplts/343000f2-3a3a-4c1b-a16f-d365a64e6619/data?periodStart=1&periodEnd=1&includeExposureMetadata=false' \
  -H 'accept: application/json' \
  -H 'Authorization: Bearer QC6f6uhFdykBmmT9wXBDfTpACyScORaTtLnIVmkg'
```

> Response 


```JSON
[
  {
    "cpltUuid": "343000f2-3a3a-4c1b-a16f-d365a64e6619",
    "date": "2022-09-28T00:00:01",
    "eventId": 2873023,
    "exposureUuid": "99c2a627-1cc0-4581-b1e0-3cb72e9d788d",
    "periodNumber": 1,
    "payout": 100000000,
    "lossQuantile": 0.410706755006686
  }
]

```



| Parameter  | Description                              |
|------------|------------------------------------------|
| CPLT  Uuid | Universal Unique identifier by analysis  |


<aside class="success">
In this json, the CPLT data output was limited to 1 period
</aside>

# Key Uuids
Below are some useful Uuids for major Perils,Regions and Data-versions:


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

# Quick Python Codes

Since API calls require the use of Uuid instead of codes, the functions below facilitate the transition between Uuid and code for the most commonly used Uuids:

## Get Peril Uuid

Get Peril Uuid from Peril code.

```python

def Get_Peril_Uuid(Peril):
    Peril_Uuid = Credentials.peril.all()
    Peril_Uuid = pd.DataFrame(json.loads(Peril_Uuid.text))
    Peril_Uuid = Peril_Uuid[Peril_Uuid['code']==Peril]
    return Peril_Uuid['uuid']
```
## Get Region Uuid

Get Region Uuid from Region code.

```python
def Get_Region_Uuid(Region):
    Region_Uuid1 = Credentials.region.all(is_sub_region=True,include_deleted=False,exclude_bottom_regions=True)
    Region_Uuid2 = Credentials.region.all(is_sub_region=False, include_deleted=False, exclude_bottom_regions=True)
    Region_Uuid1 = pd.DataFrame(json.loads(Region_Uuid1.text))
    Region_Uuid1 = Region_Uuid1[['uuid','description','code']]
    Region_Uuid2 = pd.DataFrame(json.loads(Region_Uuid2.text))
    Region_Uuid2 = Region_Uuid2[['uuid', 'description','code']]
    Region_Uuid = pd.concat([Region_Uuid1,Region_Uuid2])
    Region_Uuid = Region_Uuid[Region_Uuid['code']==Region]
    return Region_Uuid['uuid']
```
## Get Data Version Uuid

Get Data Version Uuid from Data Version code.

```python
def Get_data_version_Uuid(version):
    version_Uuid = Credentials.data_version.all(include_deleted=False)
    version_Uuid = pd.DataFrame(json.loads(version_Uuid.text))
    version_Uuid = version_Uuid[version_Uuid['description']==version]
    return version_Uuid['uuid']
```

## Get sub Region Resolution Uuid

Get sub Region Resolution Uuid using sub Region Resolution, ex: State, country, etc.


```python
def Get_sub_region_resolution_uuid(SBR):
    SBR_Uuid = Credentials.resolution.all()
    SBR_Uuid = pd.DataFrame(json.loads(SBR_Uuid.text))
    SBR_Uuid = SBR_Uuid[SBR_Uuid['description']==SBR]
    return SBR_Uuid['uuid']
```
## Get Region Name

Get region name using Region Uuid

```python
def Get_Region_name(Region_Uuid):
    Region_name = Credentials.region.get_via_uuid(Region_Uuid)
    Region_name = json.loads(Region_name.text)
    Region_name =Region_name['description']
    return Region_name
```
## Get Peril Name

Get Peril name using Peril Uuid

```python
def Get_Peril_name(Peril_Uuid):
    Peril_name = Credentials.peril.get_via_uuid(Peril_Uuid)
    Peril_name = json.loads(Peril_name.text)
    Peril_name =Peril_name['description']
    return Peril_name
```

## Get LOB name

Get LOB name using LOB Uuid

```python
def Get_LOB_name(LOB_Uuid):
    LOB_name = Credentials.lob.get_via_uuid(LOB_Uuid)
    LOB_name = json.loads(LOB_name.text)
    return LOB_name['description']
```

# Common Workflows

Now that we covered all Objects and basic calls, below we have some common workflows that utilize a sequence of calls or an iteration of the same call to achieve some of the most common workflows.

## Get Portfolio table and create new Portfolio

When we create a portfolio manually in the UI or through the API, we can retrieve the metadata for this Portfolio and create a report or create a new portfolio using the Contract UUIDs and participation shares.

```python
import UserInfo
from commons.utils.clients import *
import pandas as pd
import json
pd.set_option('expand_frame_repr', False)

Credentials = Clients.from_credentials(user_name=UserInfo.user_name, password=UserInfo.password, env=Environment.PROD)

def Get_contract_dic(Contract_dic):
    uuid= Contract_dic.get('uuid')
    name = Contract_dic.get('name')
    participation = Contract_dic.get('participation')
    isin = Contract_dic.get('isin')
    return uuid, name, participation, isin

def Get_spread(program_revision):
    Program = Credentials.program.get_by_revision_uuid(program_revision)
    Program = json.loads(Program.text)
    notes= Program['program']['notes']
    return notes

def Get_Portfolio_table(Portfolio_revision_Uuid):
    Portfolio = Credentials.portfolio.get_by_revision_uuid(Portfolio_revision_Uuid)
    Portfolio = json.loads(Portfolio.text)
    Portfolio = pd.DataFrame(Portfolio['contractsByProgram'])
    Portfolio = Portfolio.explode('contracts')
    Portfolio = Portfolio[['programRevisionUuid','programName','programRevisionResetYear','contracts','dataVersionUuids']]
    Portfolio['contracts'] = pd.DataFrame(Portfolio['contracts'].map(lambda x:Get_contract_dic(x)))
    Portfolio[['uuid', 'name', 'participation', 'isin']] =Portfolio['contracts'].apply(lambda x:pd.Series(x))
    Portfolio =Portfolio[['programRevisionUuid','programName','programRevisionResetYear','uuid','name','isin','participation']]
    Portfolio['notes'] = pd.DataFrame(Portfolio['programRevisionUuid'].map(lambda x:Get_spread(x)))
    return Portfolio


# The function below takes the Contract Uuid and the participation from a dataframe and creates a new Portfolio:
# Parameters are
# Portfolio name
# Revision name
# Table with Contract Uuids and participation

def Create_Portfolio(Portfolio,Portfolio_name,Revision_name):
    Portfolio = Portfolio[['uuid', 'participation']]
    Portfolio = Portfolio.to_json(orient="records")
    Portfolio = json.loads(Portfolio)
    Portfolio_Json ={
        "name": Portfolio_name,
        "portfolioRevisionName": Revision_name,
        "contracts": Portfolio
    }
    Portfolio_Json =json.dumps(Portfolio_Json)
    Credentials.portfolio.create(Portfolio_Json)

Portfolio = Get_Portfolio_table("b8d9a144-738e-4159-81f0-066968d10ef7")
Portfolio_name= 'Portfolio Test'
Revision_name = 'Revision Test 1'
Create_Portfolio(Portfolio)


```

## Get Portfolio table and create new Portfolio

When we create a portfolio manually in the UI or through the API, we can retrieve the metadata for this Portfolio and create a report or create a new portfolio using the Contract UUIDs and participation shares.


### Get_Analysis_Info 
By providing the analysis_Uuid, this call returns a data frame that contains information about the analysis, including portfolio UUID, portfolio revision UUID, risk start date, risk end date, analysis start and end time, and others.


```python
import UserInfo
from commons.utils.clients import *
import pandas as pd
import json
pd.set_option('expand_frame_repr', False)


Credentials  = Clients.from_credentials(user_name=UserInfo.user_name, password=UserInfo.password, env=Environment.PROD)
def Get_Analysis_Info(analysis_Uuid):
    Analysis = Credentials.analysis.get_analysis_by_uuid(analysis_Uuid)
    Analysis = json.loads(Analysis.text)
    Analysis_Info_1 =pd.DataFrame(list(Analysis.items())[:14])
    Analysis_Info_2 =pd.DataFrame(list(Analysis.items())[15:18])
    Analysis_Info = Analysis_Info_1.append(Analysis_Info_2)
    Analysis_Info =Analysis_Info.rename(columns={0:'Object',1:'Description'})
    return Analysis_Info
analysis_Uuid = '31d6a477-fcc2-4d2f-bb4c-71d9d7aa393b'
Analysis_Name=Get_analysis_name(analysis_Uuid)
Analysis_Info =Get_Analysis_Info(analysis_Uuid)
Analysis_Info.to_csv("Analysis_Info_"+Analysis_Name+".csv")

```

Response
                 Object                                        Description
0          analysisUuid               31d6a477-fcc2-4d2f-bb4c-71d9d7aa393b
1          analysisName                                      Cat Bond 144a
2       jobCreationDate                        2022-06-11T00:33:13.736628Z
3          jobStartDate                        2022-06-11T00:33:13.736636Z
4            jobEndDate                        2022-06-11T00:39:21.233987Z
5           companyUuid               efa36b93-3200-40a7-afe6-709a2a565c1a
6              userUuid               323da914-7c9b-4a26-9110-8e0439df160f
7                status                                           FINISHED
8          analysisType                                          SIMULATED
9             startDate                                2022-01-01T00:00:00
10              endDate                            2022-12-31T23:59:59.999
11          periodStart                                                  1
12            periodEnd                                              10000
13   stochasticYltUuids             [d95d92d3-f7aa-4918-adf1-e15beea0d3cf]
0           programUuid               b857ae98-3dba-43e0-8627-fc365753727f
1   programRevisionUuid               ba298bd4-96c6-42ad-af1b-36f58cf33f33
2                 cplts  [{'uuid': 'c65d8ed0-7834-4f28-a8ff-01b4043b113...


### Get_Analysis_CPLT_Info  
Get_Analysis_CPLT_Info – F1.2: This function returns a table containing the CPLTUUID and description for each CPLT generated by the analysis


```python
import UserInfo
from commons.utils.clients import *
import pandas as pd
import json
pd.set_option('expand_frame_repr', False)


Credentials  = Clients.from_credentials(user_name=UserInfo.user_name, password=UserInfo.password, env=Environment.PROD)

def Get_Analysis_CPLT_INFO(analysis_Uuid):
    Analysis = Credentials.analysis.get_analysis_by_uuid(analysis_Uuid)
    Analysis = json.loads(Analysis.text)
    Analysis_Name = Analysis.get('analysisName')
    Analysis_CPLT =Analysis.get('cplts')
    Analysis_CPLT =pd.DataFrame(Analysis_CPLT)
    return Analysis_CPLT

def Get_analysis_name(analysis_Uuid):
    Analysis = Credentials.analysis.get_analysis_by_uuid(analysis_Uuid)
    Analysis = json.loads(Analysis.text)
    Analysis_Name = Analysis.get('analysisName')
    return Analysis_Name

analysis_Uuid = '31d6a477-fcc2-4d2f-bb4c-71d9d7aa393b'
Analysis_Name=Get_analysis_name(analysis_Uuid)
Analysis_CPLT_INFO = Get_Analysis_CPLT_INFO(analysis_Uuid)
Analysis_CPLT_INFO.to_csv("Analysis_CPLT_Info_"+Analysis_Name+".csv")
```

Response

                                   uuid                              ipltUuid                   programRevisionUuid                          contractUuid termCurrencyCode  totalAmount
0  c65d8ed0-7834-4f28-a8ff-01b4043b113f  34ecbcea-dd8b-46f3-a3c9-0123fbf21de6  ba298bd4-96c6-42ad-af1b-36f58cf33f33  44c6043b-8877-47bb-9c38-509933c985e7              USD  100000000.0
1  628367f0-5bf7-44a1-9bbf-2cf31ae51e42  2a46626f-90f7-41c4-b6e8-4ccab3ac9501  ba298bd4-96c6-42ad-af1b-36f58cf33f33  69c63942-a586-4c49-b3e4-411f82ec6aba              USD   50000000.0
2  343000f2-3a3a-4c1b-a16f-d365a64e6619  e3f226db-e26e-4ec1-8239-6ca64972e3d1  ba298bd4-96c6-42ad-af1b-36f58cf33f33  9c3f1c9a-09b3-449f-825e-0a7807df85e3              USD  100000000.0
3  1d5b3c13-21c9-47c6-a907-09f05f7bbd44  13002faf-c70e-4ae5-a06b-1c8947bee02f  ba298bd4-96c6-42ad-af1b-36f58cf33f33  c6deec63-6b23-49e8-a61b-4c2d90c1f1f8              USD  100000000.0


### Get_Analysis_YLT 

This call returns a list with the UUIDs of the stochastic/scenario/Real-time profiles used in the analysis. The function links these UUIDs to another call and returns the description and Peril/Region of every YLT


```python
import UserInfo
from commons.utils.clients import *
import pandas as pd
import json
pd.set_option('expand_frame_repr', False)


Credentials  = Clients.from_credentials(user_name=UserInfo.user_name, password=UserInfo.password, env=Environment.PROD)

def Get_Analysis_YLTS(analysis_Uuid):
    Analysis = Credentials.analysis.get_analysis_by_uuid(analysis_Uuid)
    Analysis = json.loads(Analysis.text)
    Analysis_YLT = Analysis.get('stochasticYltUuids')
    Analysis_YLT =pd.DataFrame(Analysis_YLT)
    Analysis_YLT =Analysis_YLT.rename({0:'uuid'}, axis='columns')
    YLTs= Credentials.yltlibrary.get_by_data_version(data_version=Analysis.get('dataVersionUuid'))
    YLTs= pd.DataFrame(json.loads(YLTs.text))
    Analysis_YLT= Analysis_YLT.merge(YLTs,on='uuid',how='left')
    Analysis_YLT= Analysis_YLT[['uuid','perilCode','regionCode','description','typeCode']]
    return Analysis_YLT

def Get_analysis_name(analysis_Uuid):
    Analysis = Credentials.analysis.get_analysis_by_uuid(analysis_Uuid)
    Analysis = json.loads(Analysis.text)
    Analysis_Name = Analysis.get('analysisName')
    return Analysis_Name

### Calling the functions above and saving them into CSVs
analysis_Uuid = '31d6a477-fcc2-4d2f-bb4c-71d9d7aa393b'
Analysis_Name=Get_analysis_name(analysis_Uuid)
Analysis_YLTS = Get_Analysis_YLTS(analysis_Uuid)
Analysis_YLTS.to_csv("CPLT_"+Analysis_Name+".csv")
```

Response
                                   uuid perilCode regionCode           description typeCode
0  d95d92d3-f7aa-4918-adf1-e15beea0d3cf        WS         US  RMS Historical Rates       ST