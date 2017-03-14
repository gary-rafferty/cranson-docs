---
title: API Reference

language_tabs:
  - shell

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/gary-rafferty/cranson-docs'>Documentation Source</a>
  - <a href='https://github.com/gary-rafferty/cranson-app'>Cranson API</a>
  - <a href='https://github.com/gary-rafferty/cranson'>Cranson Gem</a>

includes:
  - errors

search: true
---

# Introduction to Cranson

Welcome to the Cranson API. You can use this API to access Fingal planning applications.  

We have provided a public RESTful API, that we hope will provide an intuitive way to explore existing, and new planning applications. 

As per the project [README](https://github.com/gary-rafferty/cranson-app), the purpose of the API is:

To expose an intuitive interface to query and retrieve planning applications.  
Ideally, consumers should able to programatically query things like  
- Show me all applications submitted last month.  
- Show me all pending applications within 5 kilometres of my house.  
- Show me recently decided applications.  


# Plans

## Get All Planning Applications


```shell
curl "api_endpoint_here/plans"
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

### HTTP Request

`GET api_endpoint_here/plans`

## Get a Specific Planning Application

```shell
curl "api_endpoint_here/plans/14939"
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
    "address":"The Wren's Nest, R121, Westmanstown, Clonsilla, Dublin 15"
  }
```

This endpoint retrieves a specific planning application.

### HTTP Request

`GET api_endpoint_here/plans/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the plan to retrieve

## Search Plans By Address

```shell
curl "api_endpoint_here/plans/search?query=Clonsilla"
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

`GET api_endpoint_here/plans/search?query=<QUERY>`

### URL Parameters

Parameter | Description
--------- | -----------
QUERY | A string used to search against plan addresses.

## Search Plans Within N Kilometres of a LatLng

```shell
curl api_endpoint_here/plans/within?kilometres=1&latlng=53.3841296,-6.0731679
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

`GET api_endpoint_here/plans/within?kilometres=<N>&latlng=<LATLNG>`

### URL Parameters

Parameter | Description
--------- | -----------
N | An number of kilometres defining the search radius.
LATLNG | Comma seperated value of latitude,longitude.

## Get All Decided Plans 

```shell
curl api_endpoint_here/plans/decided
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

`GET api_endpoint_here/plans/decided`

## Get All Invalid Plans 

```shell
curl api_endpoint_here/plans/invalid
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

`GET api_endpoint_here/plans/invalid`

## Get All Unknown status Plans 

```shell
curl api_endpoint_here/plans/unknown
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

`GET api_endpoint_here/plans/unknown`

## Get All Pending Plans 

```shell
curl api_endpoint_here/plans/pending
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

`GET api_endpoint_here/plans/pending`

## Get All On-Appeal Plans 

```shell
curl api_endpoint_here/plans/on_appeal
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

`GET api_endpoint_here/plans/on_appeal`
