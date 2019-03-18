# API reference

## get_site_list

A list of monitoring sites that match a provided site list expression.

### Parameters

| parameter | type            | description                   |
|-----------|-----------------|-------------------------------|
| site_list | string or array | A valid site list expression  |

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

### Returns
An array of matching sites

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

[Live example on Repl.it](https://repl.it/@AndrewCowley/getsitelist-example)

## get_latest_ts_values

### Paramters

| parameter  | type            | description                                         |
|------------|-----------------|-----------------------------------------------------|
| site_list  | string or array | A valid site list expression                        |
| datasource | string or array | The datasource from which the data will be provided             |
| trace_list | object          |                                                                 |
|            | varfrom         | Variable number to start from.                                  |
|            | varto           | Variable number to go to.                                       |
|            | accum_period    | *(optional)* In minutes. Default is 0                           |
|            | accum_partial   |                                                                 |
|            | daystart        | *(optional)* HH:mm Defaults to midnight                         |
|            | loopback        | *(optional)* The number of minutes to look back for last value. |
|            | anyqual         | *(optional)* If 0 the last quality data point will be returned. If 1 the last data point will be returned regardless of quality|
|            | now             | *(optional)* Lookback starts from current time. Can be overridden with this value. |

### Example query object

```JSON
{
  "function": "get_latest_ts_values",
  "version": 2,
  "params": {
    "site_list": "MATCH(203019)",
    "datasource": "CP",
    "tracelist": {
      "varfrom": 100.00,
      "varto": 100.00,
      "accum_period": 0,
      "accum_partial": 0,
      "output_time": "start",
      "daystart": 0900,
      "loopback": 120,
      "anyqual": 0,
      "now": 201903111200
    }
  }
}
```

### Returns
TODO
```JSON

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

### Returns

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

### Returns

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

[Live example on Repl.it](https://repl.it/@AndrewCowley/getsitegeojson-example)

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
```JSON
```
### Parameters

| parameter  | type            | description                                     |
|------------|-----------------|-------------------------------------------------|
| site_list  | string or array | A valid site list expression                    |
| datasource | string          | The datasource from which to list the variables |

### Returns
TODO
```JSON
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
TODO
```JSON
```
## Data types and formats

**Booleans:** 0 or 1, `true` or `false` is also valid.
**Date format:** yyyymmddhhmmss For example: 11am on 12 January 2019 would be represented as 20190112110000.
