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
| datasource | string or array | The datasource from which the data will be provided |
| trace_list | object          |                                                     |

### Example query object
TODO
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
      "now": "201903111200"
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

### Returns
TODO
```JSON

```
## get_site_geojson

### Parameters

| parameter | type            | description                                              |
|-----------|-----------------|----------------------------------------------------------|
| site_list | string or array | A valid site list expression                             |
| fields    | array           | Fields that will be returned in the response             |
| get_elev  | boolean         | If true, site elevation will be returned in the response |

### Returns
TODO
## get_datasources_by_site
TODO
### Parameters
TODO
## get_variable_list
TODO
### Parameters

| parameter  | type            | description                                     |
|------------|-----------------|-------------------------------------------------|
| site_list  | string or array | A valid site list expression                    |
| datasource | string          | The datasource from which to list the variables |

### Returns
TODO
## get_db_info
TODO
### Parameters
TODO
### Returns
TODO
## Site list expressions
TODO
## Data types and formats

**Booleans:** 0 or 1, `true` or `false` is also valid.
**Date format:** yyyymmddhhmmss For example: 11am on 12 January 2019 would be represented as 20190112110000.
