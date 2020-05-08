# json-traffic
JSON schema for sharing traffic data.

The following document describes schemata for 
aggregated and timeseries data.

## Timeseries Data

Timeseries data of traffic is a list of samples with a timestamp.
The sampled data is aggregated over a given window (`aggregate_interval` seconds).
Knowing the interval, we can check if the samples have any missing data.

The sources should be identified by their ixf_ixid and should be unique.

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


