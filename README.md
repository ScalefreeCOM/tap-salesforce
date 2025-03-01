# tap-salesforce customized by [Scalefree International GmbH](https://www.scalefree.com)

[<img src="https://user-images.githubusercontent.com/78537603/191483803-8cd4fc72-54a1-45f6-ab39-d798ec83e4c9.jpg" width=50% align=right>](https://www.scalefree.com){:target="_blank" rel="noopener"}

[![PyPI version](https://badge.fury.io/py/tap-mysql.svg)](https://badge.fury.io/py/tap-salesforce)
[![CircleCI Build Status](https://circleci.com/gh/singer-io/tap-salesforce.png)](https://circleci.com/gh/singer-io/tap-salesforce.png)
# Scalefree specific Updates
This tap is modified to additionally extract the salesforce metadata provided by the .describe() function of the API. This metadata is loaded into streams called "\_\_meta\_\_{original_stream_name}", e.g. "__meta__Account". 
If you have any questions, feel free to contact us!

# Quickstart
[Singer](https://www.singer.io/) tap that extracts data from a [Salesforce](https://www.salesforce.com/) database and produces JSON-formatted data following the [Singer spec](https://github.com/singer-io/getting-started/blob/master/SPEC.md).

```bash
$ mkvirtualenv -p python3 tap-salesforce
$ pip install tap-salesforce
$ tap-salesforce --config config.json --discover
$ tap-salesforce --config config.json --properties properties.json --state state.json
```



## Install the tap

```
> pip install tap-salesforce
```

## Create a Config file

```
{
  "client_id": "secret_client_id",
  "client_secret": "secret_client_secret",
  "refresh_token": "abc123",
  "start_date": "2017-11-02T00:00:00Z",
  "api_type": "BULK",
  "select_fields_by_default": true
}
```

The `client_id` and `client_secret` keys are your OAuth Salesforce App secrets. The `refresh_token` is a secret created during the OAuth flow. For more info on the Salesforce OAuth flow, visit the [Salesforce documentation](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_web_server_oauth_flow.htm). Additionnaly, if the Salesforce Sandbox is to be used to run the tap, the parameter `"is_sandbox": true` must be passed to the config.

The `start_date` is used by the tap as a bound on SOQL queries when searching for records.  This should be an [RFC3339](https://www.ietf.org/rfc/rfc3339.txt) formatted date-time, like "2018-01-08T00:00:00Z". For more details, see the [Singer best practices for dates](https://github.com/singer-io/getting-started/blob/master/BEST_PRACTICES.md#dates).

The `api_type` is used to switch the behavior of the tap between using Salesforce's "REST" and "BULK" APIs. When new fields are discovered in Salesforce objects, the `select_fields_by_default` key describes whether or not the tap will select those fields by default.

## Run Discovery

To run discovery mode, execute the tap with the config file.

```
> tap-salesforce --config config.json --discover > properties.json
```

## Sync Data

To sync data, select fields in the `properties.json` output and run the tap.

```
> tap-salesforce --config config.json --properties properties.json [--state state.json]
```

Copyright &copy; 2017 Stitch
