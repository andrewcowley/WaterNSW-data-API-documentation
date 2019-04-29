# Getting started

This guide outlines how to make a request to the NSW Water API and what will be returned in response.

## Audience

This document is written for web and mobile application developers, however the principles are the same for anyone looking to request data from this API. It is assumed that the reader has familiarity with making HTTP requests from their programming language, or tool of choice. Examples provided in the guide are written in Javascript, specifically [Node.js](https://nodejs.org/).

## Make a request

There are five elements to a successful request.

### 1. Base URL

All requests to the NSW Water API use the following URL:

`https://realtimedata.waternsw.com.au/cgi/webservice.pl`

The specifics of the request are made by providing one required URL query parameter. There is one required query parameter and three optional query parameters.

### 2. Required query parameter

Details of the request to the API are provided in a JSON object as the first URL query parameter.

This object requires three top level keys:

  1. `function`_(string)_: This specifies the function that is called on the API backend. All functions and their usage are provided in the [API reference](/api-reference.md).
  2. `version`_(number)_:  The version of the function being called.
  3. `parameters`_(object)_: The parameters being passed to the function.
  
  For example a request to the [get_site_list](/api-reference.md#get_site_list) function:
  
  ```JSON
  {
    "function": "get_site_list",
    "version": 2,
    "params": {
      "site_list": "MATCH(210*)"
    }
  }
  ```
  When appending the JSON as a URL query parameter all spaces must be removed. In JavaScript [JSON.stringify()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify) will achieve this.
  
 ```JS
 const query =   {
    "function": "get_site_list",
    "version": 2,
    "params": {
      "site_list": "MATCH(210*)"
    }
  };
  
 const stringifiedQuery = JSON.stringify(query);
 ```

### 3. Optional URL query parameters

  1. `ver=2`: When the `ver` URL parameter isn't provided on the request URL some of the keys in the returned JSON are prefixed to work around JSON parsing in old browsers.
  2.  `mime=csv`: This URL parameter will cause the response to have its HTTP `content-type` header set to `text/csv`. **This will not change the format of the response from JSON to CSV.**
  3. **format**
    - `format=csv`: The response is returned in CSV format
    - `format=csvc`: The response returned in CSV format with rows have trailing commas.

### 4. Request HTTP methods

Requests to the NSW Water API can be made using either HTTP `GET` or `POST` methods.

For `GET` requests URL parameters are added to the URL to form requests. For `POST` requests the parameters are added to the request body.

### 5. Required `User-Agent` HTTP header

Requests to the API will fail with a HTTP 502 error unless a `User-Agent` header, with a non-empty string as a value, is provided. For example: `User-Agent: 'APIDocs'`. Some HTTP clients and libraries set a default `User-Agent` header. Others, such as the [Node.js `https` module](https://nodejs.org/api/https.html) need the `User-Agent` to be specified.

### Requests from the browser

Making a XMLHttpRequest/AJAX request from the browser is not possible as the NSW Water API does not support cross origin requests. JSONP can be used to work around the cross origin restrictions.

#### CSV Download
If the [optional URL parameters](/getting-started.md#3-optional-url-query-parameters) are set to return a CSV, instead of JSON, browsers will download the CSV file. This is useful for working with historical data as the data can be downloaded and then woked with locally.

## Responses

### Successful responses

Successful responses return JSON by default. The returned JSON object contains metadata about the response and the returned data. A successful response takes the following form:

```JSON
{
    "err_num": 0,
    "buff_required": 1790,
    "buff_supplied": 1879,
    "return": {
    }
}
```

A successful response has four top level parameters:

  1. `err_num`: Will be 0 to indicate a successful response.
  2. `buff_required`: The size in bytes of the response.
  3. `buff_supplied`: The bytes allocated to the response by the system.
  4. `return`: The data returned from the API in response to the query object in the request.

**The default `content-type` of the response is `text/html`**

### Errors

If there is an error in the client request 4XX series HTTP codes **are not returned**. Error codes are instead returned in the API response with a `200 OK` code. The exception to this is not providing a valid `User-Agent` header. This will result in a `502 Bad Gateway` error.

If an error is present an `err_msg` key will be present with the value outlining the error message.

```JSON
{
    "err_num": 100,
    "err_msg": "Unknown \"function\" value [get_dsb_info]"
}
```
#### Common error codes [WIP]

| Error code | Description                 |
|------------|-----------------------------|
| 0          | No error                    |
| 21         | Invalid date                |
| 22         | Invalid time                |
| 23         | End time before start time  |
| 80         | Invalid datasource          |
| 83         | Invalid site                |
| 84         | Invalid site list           |
| 100        | Invalid function parameter  |
| 120        | Invalid top level parameter |

### Sites

Each monitoring site has an id. Specific sites can be found by manually going through the list of sites on the WaterNSW website or can be targeted in various ways by a few different API methods.

### Data sources

Each site has a number of data sources associated with it. They are represented by short codes such as 'CP', 'A' or 'PROV'. It isn't always clear which data source is best to use when requesting data from a site. 'CP' is the best data source to try for most sites.

### Variables

A variable corresponds to a site measurement. For example 100.00 refers to the level of a river measured in metres. Some API requests require the variable range to be specified in the request.

```
{
  "varfrom": 100.00,
  "varto": 141.00
}

```

Responses use the `v` key to specify which measurement is being returned. In the following example `"v": 100.00` refers to the river/stream height in metres.

 ```JSON
 {
  "v": 100.00,
  "q": 125,
  "t": 2.4
 }
 ```

#### Rivers and streams

| Variable number | Name                            | Data type     |
|-----------------|---------------------------------|---------------|
| 10.00           | Rainfall (mm)                   | Daily total   |
| 100.00          | Level (M)                       | Instantaneous |
| 141.00          | Discharge (ML/d)                | Instantaneous |
| 2010.00         | Electrical conductivity (uS/cm) | Instantaneous |
| 2080.00         | Temperature (&deg;C)            | Instantaneous |

#### Dams

| Variable number | Name                | Data type     |
|-----------------|---------------------|---------------|
| 10.00           | Rainfall (mm)       | Daily total   |
| 130.00          | Reservoir Level (m) | Instantaneous |

#### Groundwater

| Variable number | Name                                            | Data type |
|-----------------|-------------------------------------------------|-----------|
| 110.00          | Bore water level below measuring point (Meters) |           |
| 110.00 - 115.00 | Groundwater Level - AHD (Meters)                |           |
| 20.80.00        | Water temp. (&deg;C)                            |           |

### Quality codes

Each data point is associated with a quality code. The quality code indicates if the data point has been reviewed or is the raw value from the telemetry.

|Quality code | Meaning                        |
|-------------|--------------------------------|
| 10          | Good                           |
| 15          | Water below threshold (no flow)|
| 20          | Fair                           |
| 30          | Poor                           |
| 60          | Estimate                       |
| 130         | Interim                        |
