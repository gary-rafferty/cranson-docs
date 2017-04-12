---
title: Cranons API Documentation

toc_footers:
  - <a href='https://github.com/gary-rafferty/cranson-app'>Cranson API</a>
  - <a href='https://github.com/gary-rafferty/cranson'>Cranson Gem</a>
  - <a href='https://github.com/gary-rafferty/cranson-docs'>Documentation Source</a>

includes:
  - errors

search: true
---

# Introduction to Cranson

Welcome to the Cranson API. You can use this API to access Fingal planning applications.  

We have provided a public RESTful API, that we hope will provide an intuitive way of exploring existing, and new planning applications.

As per the project [README](https://github.com/gary-rafferty/cranson-app), the purpose of the API is:

To provide an intuitive interface to query and retrieve planning applications.  
Ideally, consumers should able to programatically query things like  
- Show me all applications submitted last month.  
- Show me all pending applications within 5 kilometres of my house.  
- Show me recently decided applications.  
- Show me all changes / updates for a particular application.

For now, the only housing authority supported is Fingal, but we plan to add more in the future.  
We've identified datasets for Dublin City Council, Dun-Laoghaire Rathdown, and South County Dublin, so these authorities are on our roadmap. 

If you would like to help, please get in touch on [Github](https://github.com/gary-rafferty/cranson-app/issues/new).

# Plans

## Get All Planning Applications


```shell
curl "http://api.cranson.co/plans"
```

> The above command returns JSON structured like this:

```json
[
  {
    "id":14939,
    "status":"Decided",
    "decision_date":"2017-01-27",
    "description":"Two storey extension to existing two storey two bedroom dwelling...",
    "link":"http://planning.fingalcoco.ie/swiftlg/apas/run/WPHAPPDETAIL.DisplayURL?theApnID=FW16A/0147",
    "reference":"FW16A/0147",
    "registration_date":"2016-12-29",
    "address":"The Wren's Nest, R121, Westmanstown, Clonsilla, Dublin 15"
  }
  // snipped
]
```

This endpoint retrieves all plans, paginated in batches of 50.  
All enumerated responses use link-header pagination. Please use this to iterate over the paged responses.  
By default, plans are ordered by latest registration date.

### HTTP Request

`GET http://api.cranson.co/plans`

## Get All Planning Applications Registered In The Last Month


```shell
curl "http://api.cranson.co/plans/recently_registered"
```

> The above command returns JSON structured like this:

```json
[
  {
    "id":14939,
    "status":"Decided",
    "decision_date":"2017-01-27",
    "description":"Two storey extension to existing two storey two bedroom dwelling...",
    "link":"http://planning.fingalcoco.ie/swiftlg/apas/run/WPHAPPDETAIL.DisplayURL?theApnID=FW16A/0147",
    "reference":"FW16A/0147",
    "registration_date":"2016-12-29",
    "address":"The Wren's Nest, R121, Westmanstown, Clonsilla, Dublin 15"
  }
  // snipped
]
```

This endpoint retrieves all recently registered plans, paginated in batches of 50.  
All enumerated responses use link-header pagination. Please use this to iterate over the paged responses.  
By default, plans are ordered by latest registration date.

### HTTP Request

`GET http://api.cranson.co/plans/recently_registered`

## Get All Planning Applications Decided In The Last Month


```shell
curl "http://api.cranson.co/plans/recently_decided"
```

> The above command returns JSON structured like this:

```json
[
  {
    "id":14939,
    "status":"Decided",
    "decision_date":"2017-01-27",
    "description":"Two storey extension to existing two storey two bedroom dwelling...",
    "link":"http://planning.fingalcoco.ie/swiftlg/apas/run/WPHAPPDETAIL.DisplayURL?theApnID=FW16A/0147",
    "reference":"FW16A/0147",
    "registration_date":"2016-12-29",
    "address":"The Wren's Nest, R121, Westmanstown, Clonsilla, Dublin 15"
  }
  // snipped
]
```

This endpoint retrieves all plans decided in the last month, paginated in batches of 50.  
All enumerated responses use link-header pagination. Please use this to iterate over the paged responses.  
By default, plans are ordered by latest registration date.

### HTTP Request

`GET http://api.cranson.co/plans/recently_decided`


## Get a Specific Planning Application

```shell
curl "http://api.cranson.co/plans/14939"
```

> The above command returns JSON structured like this:

```json
  {
    "id":14939,
    "status":"Decided",
    "decision_date":"2017-01-27",
    "description":"Two storey extension to existing two storey two bedroom dwelling...",
    "link":"http://planning.fingalcoco.ie/swiftlg/apas/run/WPHAPPDETAIL.DisplayURL?theApnID=FW16A/0147",
    "reference":"FW16A/0147",
    "registration_date":"2016-12-29",
    "address":"The Wren's Nest, R121, Westmanstown, Clonsilla, Dublin 15",
    "audits": [
      {
        "changes": {"Current Status": ["Pending", "Decided"]},
        "changed_at": 2017-01-29""
      }
    ]
  }
```

This endpoint retrieves a specific planning application. In addition to the plan data, it also includes an audit log of changes over time.  
If there are any changes to display, we will include the original value, the updated value, and the date we retrieved the change.  
In the example above, the status of the application changed from pending to decided.

### HTTP Request

`GET http://api.cranson.co/plans/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the plan to retrieve

## Search Plans By Address

```shell
curl "http://api.cranson.co/plans/search?query=Clonsilla"
```

> The above command returns JSON structured like this:

```json
[  
  {
    "id":14939,
    "status":"Decided",
    "decision_date":"2017-01-27",
    "description":"Two storey extension to existing two storey two bedroom dwelling...",
    "link":"http://planning.fingalcoco.ie/swiftlg/apas/run/WPHAPPDETAIL.DisplayURL?theApnID=FW16A/0147",
    "reference":"FW16A/0147",
    "registration_date":"2016-12-29",
    "address":"The Wren's Nest, R121, Westmanstown, Clonsilla, Dublin 15"
  }
]
```

This endpoint retrieves all planning applications that have addresses containing `QUERY`.

### HTTP Request

`GET http://api.cranson.co/plans/search?query=<QUERY>`

### URL Parameters

Parameter | Description
--------- | -----------
QUERY | A string used to search against plan addresses.

## Search Plans Within N Kilometres of a LatLng

```shell
curl http://api.cranson.co/plans/within?kilometres=1&latlng=53.3841296,-6.0731679
```

> The above command returns JSON structured like this:

```json
[  
  {
    "id":14939,
    "status":"Decided",
    "decision_date":"2017-01-27",
    "description":"Two storey extension to existing two storey two bedroom dwelling...",
    "link":"http://planning.fingalcoco.ie/swiftlg/apas/run/WPHAPPDETAIL.DisplayURL?theApnID=FW16A/0147",
    "reference":"FW16A/0147",
    "registration_date":"2016-12-29",
    "address":"The Wren's Nest, R121, Westmanstown, Clonsilla, Dublin 15"
  }
]
```

This endpoint retrieves all planning applications within N kilometres of a given LatLng

### HTTP Request

`GET http://api.cranson.co/plans/within?kilometres=<N>&latlng=<LATLNG>`

### URL Parameters

Parameter | Description
--------- | -----------
N | An number of kilometres defining the search radius.
LATLNG | Comma seperated value of latitude,longitude.

## Get All Decided Plans 

```shell
curl http://api.cranson.co/plans/decided
```

> The above command returns JSON structured like this:

```json
[  
  {
    "id":14939,
    "status":"Decided",
    "decision_date":"2017-01-27",
    "description":"Two storey extension to existing two storey two bedroom dwelling...",
    "link":"http://planning.fingalcoco.ie/swiftlg/apas/run/WPHAPPDETAIL.DisplayURL?theApnID=FW16A/0147",
    "reference":"FW16A/0147",
    "registration_date":"2016-12-29",
    "address":"The Wren's Nest, R121, Westmanstown, Clonsilla, Dublin 15"
  }
]
```

This endpoint retrieves all decided planning applications. 

### HTTP Request

`GET http://api.cranson.co/plans/decided`

## Get All Invalid Plans 

```shell
curl http://api.cranson.co/plans/invalid
```

> The above command returns JSON structured like this:

```json
[  
  {
    "id":14939,
    "status":"invalid",
    "decision_date":"2017-01-27",
    "description":"Two storey extension to existing two storey two bedroom dwelling...",
    "link":"http://planning.fingalcoco.ie/swiftlg/apas/run/WPHAPPDETAIL.DisplayURL?theApnID=FW16A/0147",
    "reference":"FW16A/0147",
    "registration_date":"2016-12-29",
    "address":"The Wren's Nest, R121, Westmanstown, Clonsilla, Dublin 15"
  }
]
```

This endpoint retrieves all invalid planning applications. 

### HTTP Request

`GET http://api.cranson.co/plans/invalid`

## Get All Unknown status Plans 

```shell
curl http://api.cranson.co/plans/unknown
```

> The above command returns JSON structured like this:

```json
[  
  {
    "id":14939,
    "status":"unknown",
    "decision_date":"2017-01-27",
    "description":"Two storey extension to existing two storey two bedroom dwelling...",
    "link":"http://planning.fingalcoco.ie/swiftlg/apas/run/WPHAPPDETAIL.DisplayURL?theApnID=FW16A/0147",
    "reference":"FW16A/0147",
    "registration_date":"2016-12-29",
    "address":"The Wren's Nest, R121, Westmanstown, Clonsilla, Dublin 15"
  }
]
```

This endpoint retrieves all unknown planning applications. 

### HTTP Request

`GET http://api.cranson.co/plans/unknown`

## Get All Pending Plans 

```shell
curl http://api.cranson.co/plans/pending
```

> The above command returns JSON structured like this:

```json
[  
  {
    "id":14939,
    "status":"pending",
    "decision_date":"2017-01-27",
    "description":"Two storey extension to existing two storey two bedroom dwelling...",
    "link":"http://planning.fingalcoco.ie/swiftlg/apas/run/WPHAPPDETAIL.DisplayURL?theApnID=FW16A/0147",
    "reference":"FW16A/0147",
    "registration_date":"2016-12-29",
    "address":"The Wren's Nest, R121, Westmanstown, Clonsilla, Dublin 15"
  }
]
```

This endpoint retrieves all pending planning applications. 

### HTTP Request

`GET http://api.cranson.co/plans/pending`

## Get All On-Appeal Plans 

```shell
curl http://api.cranson.co/plans/on_appeal
```

> The above command returns JSON structured like this:

```json
[  
  {
    "id":14939,
    "status":"on_appeal",
    "decision_date":"2017-01-27",
    "description":"Two storey extension to existing two storey two bedroom dwelling...",
    "link":"http://planning.fingalcoco.ie/swiftlg/apas/run/WPHAPPDETAIL.DisplayURL?theApnID=FW16A/0147",
    "reference":"FW16A/0147",
    "registration_date":"2016-12-29",
    "address":"The Wren's Nest, R121, Westmanstown, Clonsilla, Dublin 15"
  }
]
```

This endpoint retrieves all on_appeal planning applications. 

### HTTP Request

`GET http://api.cranson.co/plans/on_appeal`
