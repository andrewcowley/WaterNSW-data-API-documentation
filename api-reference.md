# API reference

## get_site_list

A list of monitoring sites that match a provided site list expression.

### Parameters

| parameter | type            | description                   |
|-----------|-----------------|-------------------------------|
| site_list | string or array | A valid site list expression  |

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

### Notes

An array of matching sites.

## get_latest_ts_values

### Paramters

| parameter  | type            | description                                         |
|------------|-----------------|-----------------------------------------------------|
| site_list  | string or array | A valid site list expression                        |
| datasource | string or array | The datasource from which the data will be provided |
| trace_list | array           |                                                     |

### Returns
TODO
## get_sites_by_datasource

### Paramters

| parameter   | type            | description                         |
|-------------|-----------------|-------------------------------------|
| datasources | array           | An array of one or more datasources |

### Returns
TODO
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
