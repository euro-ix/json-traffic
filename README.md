# json-traffic
JSON schema for sharing traffic data.

The following document describes schemata for 
aggregated and timeseries data.

## Timeseries Data

Timeseries data of traffic is a list of samples with a timestamp.
The sampled data is aggregated over a given window (`aggregate_interval` seconds).
Knowing the interval, we can check the integrity of the series.

The sources should be identified by their ixf_ixid and should be unique.

The samples arn n-tuples of

  - `timestamp` (ISO 8601)
  - `packets_in`
  - `packets_out`
  - `octets_in`
  - `octets_out`


### Example
    {
        "version": "1.0",
        "created_at": "2001-10-23T23:30:12Z",
        "next_update_at":  "2001-10-23T23:45:12Z", 
        "sources": {
            "<ixf_ixid>": {
                "url": "https://...",
                "title": "IX LAN 1",
                "aggregate_interval": 300,
            },
        }, 
        "samples": {
            "<ixf_ixid>": [
                ["2001-10-23T23:42:10Z", 23, 42, 12897,  481],
            ]
        }
    }

### Schema

[schema/json-traffic-timeseries-v1.json](schema/json-traffic-timeseries-v1.json)

## Aggregate Data

This is a schema for aggregated data for the ixp. It should should be serverd separatly
from the timeseries data.


### Example
    {
        "version": "1.0",
        "created_at": "2001-10-23T23:30:12Z",
        "next_update_at":  "2001-10-23T23:45:12Z", 
        "sources": {
            "<ixf_ixid>": {
                "url": "https://...",
                "title": "IXP LAN 1 (1 Day)",
                "aggregate_interval": 86400,
            },
        }, 
        "statistics": {
            "<ixf_ixid>": {
                "current_packets_in": 1730224,
                "current_packets_out": 17456,
                "current_octets_in": 1734882240,
                "current_octets_out": 173220,
                "average_packets_in": 18470161,
                "average_packets_out": 305805818,
                "average_octets_in": 18470161,
                "average_octets_out": 305805818,
                "maximum_packets_in": 431179242464,
                "maximum_packets_out": 431870526584,
                "maximum_octets_in": 431179242464,
                "maximum_octets_out": 431870526584,
                "maximum_in_at": "2020-05-07T14:40:00Z",
                "maximum_out_at": "2020-05-07T14:40:00Z"
        }
    }

### Schema

[schema/json-traffic-aggregated-v1.json](schema/json-traffic-aggregated-v1.json)

