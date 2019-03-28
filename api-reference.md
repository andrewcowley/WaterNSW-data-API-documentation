# API reference

- [get_site_list](#get_site_list)
- [get_latest_ts_values](#get_latest_ts_values)
- [get_sites_by_datasource](#get_sites_by_datasource)
- [get_site_geojson](#get_site_geojson)
- [get_datasources_by_site](#get_datasources_by_site)
- [get_variable_list](#get_variable_list)
- [get_db_info](#get_db_info)

## get_site_list

A list of monitoring sites that match a provided [site list expression](#site-list-expressions).

View and run this [Node.js example](https://repl.it/@AndrewCowley/getsitelist-example) on Repl.it

### Parameters

| parameter | type            | required | description                                             |
|-----------|-----------------|----------|---------------------------------------------------------|
| site_list | string          | Yes      | A valid [site list expression](#site-list-expressions)  |

### Example query object

```JSON
{
  "function": "get_site_list",
  "version": 1,
  "params": {
    "site_list": "MATCH(20301*)"
  }
}
```

### Example response

```JSON
{
  "error_num":0,
  "buff_required":244,
  "return":{
    "sites": [ "203010", "20301004", "20301018", "20301019", "20301020", "20301021", "20301022", "20301023", "203011", "203012", "203013", "203014", "203015", "203016", "203017", "203018", "203019"]
    },
  "buff_supplied":1000
}
```

## get_latest_ts_values

Returns the latest values in the timeseries for the specified sites and variables.

### Paramters

| parameter  | type             | required  | description                                         |
|------------|------------------|-----------|-----------------------------------------------------|
| site_list  | string           | Yes       | A valid site list expression                        |
| datasource | string or array  | Yes       | The datasource from which the data will be provided |
| trace_list | object           | Yes       | See [trace_list object](#trace_list-object) below.  |

#### trace_list object

| parameter      | type    | required  | description                                         |
|----------------|---------|-----------|-----------------------------------------------------|
| varfrom        | number  | Yes       | Variable number to start from.                      |
| varto          | number  | Yes       | Variable number to go to.                           |
| accum_period   | number  | No        | In minutes. Default is 0                            |
| accum_partial  | number  | No        | Defaults to 0. If 0 the last accumulated period is used. If 1 the last two accumulated periods are used. |
| daystart       | number  | No        | HH:mm Defaults to midnight                          |
| lookback       | number  | No        | The number of minutes to look back for last value.  |
| anyqual        | number  | No        |0: last quality data point will be returned. If 1 last data point will be returned regardless of quality|
| now            | boolean | No        | Lookback starts from current time. Can be overridden with this value. |

### Example query object

```JSON
{
   "function":"get_latest_ts_values",
   "version":2,
   "params":{
      "site_list":"203014",
      "datasource":"CP",
      "trace_list":[
         {
            "varfrom":100,
            "varto":100
         },
         {
            "varfrom":"141",
            "varto":"141"
         }
      ]
   }
}
```

### Response

```JSON
{
   "error_num":0,
   "buff_required":367,
   "return":{
      "203014":[
         {
            "values":[
               {
                  "time_end":"",
                  "v":"0.888",
                  "q":130,
                  "p":"",
                  "trend":"0",
                  "time":"20190319130000",
                  "time_start":""
               }
            ],
            "varto":"100.00",
            "varfrom":"100.00"
         },
         {
            "values":[
               {
                  "time_end":"",
                  "v":"89.438",
                  "q":140,
                  "p":"",
                  "trend":"-",
                  "time":"20050224040000",
                  "time_start":""
               }
            ],
            "varto":"141.00",
            "varfrom":"141.00"
         }
      ]
   },
   "buff_supplied":1000
}
```
## get_sites_by_datasource

### Paramters

| parameter   | type            | description                         |
|-------------|-----------------|-------------------------------------|
| datasources | array           | An array of one or more datasources |

### Example query object

```JSON
{
  "function": "get_sites_by_datasource",
  "": 1,
  "params" : {
    "datasources": ["CP"]
  }
}
```

### Response

```JSON
{
  "error_num":0,
  "buff_required":43276,
  "return":{
    "datasources":[
      {
        "datasource":"CP",
        "sites":["012001", "012002"...]
      }
    ]
  },
  "buff_supplied": 45439
}
```
## get_site_geojson

[Node.js example on Repl.it](https://repl.it/@AndrewCowley/getsitegeojson-example)

### Parameters

| parameter | type            | description                                              |
|-----------|-----------------|----------------------------------------------------------|
| site_list | string or array | A valid site list expression                             |
| fields    | array           | Fields that will be returned in the response             |
| get_elev  | boolean         | If true, site elevation will be returned in the response |

### Example query object

```JSON
{
  "function": "get_site_geojson",
  "version": 2,
  "params": {     
    "site_list": '',
    "get_elev": 1,
    "fields": ['zone']
  }
}
```

### Response

```JSON
{
   "error_num":0,
   "buff_required":242,
   "return":{
      "features":[
         {
            "properties":{
               "zone":56
            },
            "geometry":{
               "coordinates":[
                  152.1713,
                  -28.6448
               ],
               "type":"Point"
            },
            "id":"204006",
            "type":"Feature"
         }
      ],
      "type":"FeatureCollection"
   },
   "buff_supplied":1000
}
```

## get_datasources_by_site
TODO
```JSON
```
### Parameters
TODO
```JSON
```
## get_variable_list
TODO

### Parameters

| parameter  | type            | description                                     |
|------------|-----------------|-------------------------------------------------|
| site_list  | string or array | A valid site list expression                    |
| datasource | string          | The datasource from which to list the variables |

### Example query object

```JSON
{
   "function":"get_variable_list",
   "version":1,
   "params":{
      "site_list":"204006",
      "datasource":"CP"
   }
}
```
### Response

```
{
   "error_num":0,
   "buff_required":1433,
   "return":{
      "sites":[
         {
            "site_details":{
               "timezone":"10.0",
               "short_name":"PEEL @ TAMWORTH",
               "name":"PEEL RIVER AT TAMWORTH"
            },
            "variables":[
               {
                  "period_end":"20190318180000",
                  "period_start":"19930720151500",
                  "subdesc":"",
                  "variable":"100.00",
                  "units":"Metres",
                  "name":"Stream Water Level"
               },
               ...
            ],
            "site":"419009"
         }
      ]
   },
   "buff_supplied":1504
}
```
## get_db_info

### Parameters
| parameter       | type            | description                                                                                                                                                                                                            |
|-----------------|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| table_name      | string          | The table name from the database. E.g. 'site'                                                                                                                                                                          |
| return_type     | string          | Specifies the data structure returned. Values are either 'hash' or 'array                                                                                                                                              |
| filter_values   |                 | (*optional*)                                                                                                                                                                                                           |
| field_list      | array           | (*optional*) An array of field names to return from the database                                                                                                                                                       |
| sitelist_filter | sitelist filter | (*optional*) A valid sitelist filter expression                                                                                                                                                                        |
| geo_filter      | array           | (*optional*) Filter based on latitude and longitude. Circle: ['lat', 'lng], Rectangle: [['top left lat', 'top_left_long'], ['bottom_right_lat, bottom_right_long']] Region: [[lat, long], [lat, long], [lat, long]...] |
| complex_filter  |                 | (*optional*) Filter the results based on the values of fields.                                                                                                                                                         |
| raw_db_filter   |                 | (*optional*) TODO                                                                                                                                                                                                      |
| order           | string          | (*optional*) Which field to order the results by                                                                                                                                                                       |
| start_from      |                 | (*optional*)                                                                                                                                                                                                           |
| return_limit    |                 | (*optional*) Limits the number of rows returned                                                                                                                                                                        |
| decodes         |                 | ???                                                                                                                                                                                                                    |### Returns
TODO
```JSON
```
## Site list expressions

A site list expression is a way of specifying a list of sites as a parameter to an API function. The simplest site expression is one specific site id.
```
...
"site_list": "210102"
...
```

## Data types and formats

**Booleans:** 0 or 1, `true` or `false` is also valid.
**Date format:** yyyymmddhhmmss For example: 11am on 12 January 2019 would be represented as 20190112110000.
