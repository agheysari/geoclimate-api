# geoclimate-api
A RESTful API to serve climate forecasts by **SIGLAB/Geoclimate AI-based Framework**.

## Connection
The API currently supports HTTP POST requests. The server listens to the requests sent to:
> `api.geoclimate.ca:443`

Currently JSON requests are supported.

## Request types

Currently two types of requests are supported:

`timeseries`: To fetch time series for a point over the study area.

`instance`: To fetch values over the entire study area (or a cropped patch) at a given time over the study period.

## Examples

An example of `timeseries' request:
```json
{
    "experiment" : "nunavik_era5land_rcp45_monthly_regrid",
    "type": "timeseries",
    "var": "ts",
    "lat": 55.2,
    "lon": -60,
    "time_start": "2006-01-01",
    "time_end": "2050-01-01"
}
```

An example of `instance' request:
```json
{
    "experiment" : "nunavik_era5land_rcp45_monthly_regrid",
    "type": "instance",
    "var": "ts",
    "top": 55.6,
    "bottom": 55,
    "left": -60.6,
    "right": -59.6,
    "time": "2006-01-01"
}
```


## Request Keys

`experiment`: Please refer to the list of experiments.

`type`: Request type. Currently supported: `timeseries` or `instance`

`var`: Climate variable, use CMIP6 notation. Please refer to the experiment documentation for the list of variables.


### Request keys specific to `timeseries` type:

`lat`: Latitude of the data point in decimal format. It should match the coordinates of a point over the grid. Interpolation is not supported at this time. Please refer to the experiment description for grid boundaries and resolution.

`lon`: Longitude of the data point in decimal format. It should match the coordinates of a point over the grid. Interpolation is not supported at this time. Please refer to the experiment description for grid boundaries and resolution.

`time_start`: The beginning of the time series in ISO 8601 format (YYYY-MM-DD).

`time_end`: The end of the time series in ISO 8601 format (YYYY-MM-DD).


### Request keys specific to `instance` type:

`top`: The decimal latitude of the north boundary.

`bottom`: The decimal latitude of the south boundary.

`left`: The decimal longitude of the west boundary.

`right`: The decimal longitude of the east boundary.

`time`: The time of the instance in ISO 8601 format (YYYY-MM-DD). Interpolation is not supported at this time. Please refer to the experiment description for temporal range and resolution.
