# API reference

## get_site_list

A list of monitoring sites that match a provided site list expression.

### Parameters

| parameter | type            | description                   |
|-----------|-----------------|-------------------------------|
| site_list | string or array | A valid site list expression  |

### Returns
TODO
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
