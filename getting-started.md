# Getting started

This guide outlines the basics of making a request to the NSW Water API and what can be expected in response. 

## Audience

This document is written for web and mobile application developers, but the basics are the same for anyone looking to request data from the API. It is assumed that the reader has familiarity with making HTTP requests from their programming language, or tool, of choice.

## Making a request

All requests to the NSW Water API use the following URL:

`https://realtimedata.waternsw.com.au/cgi/webservice.pl`

The specifics of the request are made by providing one required URL query parameter. There is one required query parameter and three optional query parameters.

### Required query parameter

Details of the request to the API are provided in a JSON object as the first parameter.

This object requires three parameters:

  1. `function` - The function that is called on the API backend
  2. `version` -  The version of the API(or function?) being called
  3. `parameters` - parameters being passed to the function
  
  All functions and their usage is provided in the [API reference](/api-reference.md).
  
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
  The JSON needs to have all spaces removed and provided in the URL as a URL query parameter. For example:
  
 ```
 https://realtimedata.waternsw.com.au/cgi/webservice.pl?{"function":"get_site_list","version":2,"params":{"site_list":"MATCH(210*)"}}
 ```

### Optional parameters

  1. **ver**
    - `2`: Modifies keys in the returned response are modified to remove prefixes that were present in version. **Recommended**
  2. **mime**
    - `csv`: Response has content type header set to CSV
  3. **format**
    - `csv`: Response returned in CSV format
    - `csvc`: Response returned in CSV format. Rows have trailing commas.

### Request methods

Requests to the NSW Water API can be made using either HTTP `GET` or `POST` methods.

For `GET` requests URL parameters are added to the URL to form specific requests. There is one required parameter and various option parameters.

For `POST` requests the parameters are added to the request body.

#### Browser XMLHttpRequests

Making XMLHttpRequests from the browser is not currently possible. The NSW Water API does not provide suitable headers to allow cross origin requests.

## Responses

### Successful responses

Successful responses return JSON by default. The returned JSON object contains some metadata about the response as well as the returned data. A successful response takes the following form:

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

  1. err_num: This will always be 0 to indicate response was successful.
  2. buff_required: The size in bytes of the response.
  3. buff_supplied: The bytes allocated to the response by the API backend.
  4. return: The data returned from the API in response to the query object in the request.

### Errors

Error codes are provided in the API response. `"err_num": 0` represents a request with no errors. If an error is present an `err_msg` key will be present with the value outlining the error message.

```JSON
{
    "err_num": 100,
    "err_msg": "Unknown \"function\" value [get_dsb_info]"
}
```

### Sites

TODO

### Datasources

TODO

### Variables

TODO

#### Rivers and streams

| Variable number | Name                            | Data type     |
|-----------------|---------------------------------|---------------|
| 10.00           | Rainfall (mm)                   | Daily total   |
| 100.00          | Level (Metres)                  | Instantaneous |
| 141.00          | Discharge (ML/d)                | Instantaneous |
| 2010.00         | Electrical conductivity (uS/cm) | Instantaneous |
| 2080.00         | Temperature (C)                 | Instantaneous |

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
| 20.80.00        | Water temp. (C)                                 |           |

### Quality codes

TODO
