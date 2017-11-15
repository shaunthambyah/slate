---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href='https://competeshark.com/contact'>Contact Sales for an API key</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Competeshark API. Competeshark provides a complete set of API endpoints for extracting competitive insights.

We've provided some code samples in the dark area to the right to get you started. You'll notice there are a number of language choices, you can switch between each by clicking on the language tab on the top.

Have some feedback or questions that aren't covered in the documentation? Just send us an email [dev@competeshark.com](mailto:dev@competeshark.com)

# Authentication

> To authorize, use this code:

```shell
# Simply pass the Authorization header with each request
curl "https://go.competeshark.com/api/v1/some_api_endpoint"
  -u "api:YOUR_GENERATED_API_KEY"
```
```shell
# Alternatively you may encode the api key as base64 and pass it as a header
curl "https://go.competeshark.com/api/v1/some_api_endpoint"
  -H "Authorization: Basic YXBpOllPVVJfR0VORVJBVEVEX0FQSV9LRVk=
```

> Make sure your replace `YOUR_GENERATED_API_KEY` with your own valid API key.

Competeshark uses API keys to authorize access to its API endpoints. You can create and manage API keys from our Integrations feature [https://go.competeshark.com/integrations] (https://go.competeshark.com/integrations)

All API endpoints are secured using a basic auth scheme with `api` as the username and your API key as the password.

If you need to, you may construct and send the basic auth headers yourself. To do this perform the following steps:

1. build a string in the form `api:YOUR_GENERATED_API_KEY`
2. Base64 encode the string
3. Supply an `Authorization` header with content `Basic` followed by the Base64 encoded string. For example, the string `api:YOUR_GENERATED_API_KEY` encodes to `YXBpOllPVVJfR0VORVJBVEVEX0FQSV9LRVk=` in Base64, so you would make the request as follows in CURL.

<code>curl "https://go.competeshark.com/api/v1/some_api_endpoint" -H "Authorization: Basic YXBpOllPVVJfR0VORVJBVEVEX0FQSV9LRVk=</code>

You may have a number of API keys for various integrations. API Keys should be kept private, if you feel a key has been comprimised, simply delete the comprimised key and generate a new one. Don't forget to the replace the API key in your integration.

<aside class="notice">
You must replace <code>YOUR_GENERATED_API_KEY</code> with your own valid API key.
</aside>

# LANDSCAPES

## Get All Landscapes

```shell
curl "https://go.competeshark.com/api/v1/landscapes"
  -u "api:YOUR_GENERATED_API_KEY"
```

> This will return a JSON array of landscapes:

```json
[
  {
    "id": "59f925d0f8894e5a020041a7",
    "name": "My Landscape 1",
  },
  {
    "id": "59d455c8f8894e896e0041a8",
    "name": "My Landscape 2",
  }
  ...
]
```

This endpoint retrieves all available landscapes for your account.

### HTTP Request

`GET https://go.competeshark.com/api/v1/landscapes`


<aside class="success">
Don't forget your Authorization header!
</aside>

# PERFORMANCE

## Get Competitor load times

```shell
curl "https://go.competeshark.com/api/v1/performance?start=1510669397&end=1510761397&landscape=59d455c8f8894e896e0041a8"
  -u "api:YOUR_GENERATED_API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "url": "http://google.com",
    "name": "Google",
    "id": "59d455c8f8894e896e0041a7",
    "timestamps": [
      1510617600,
      1510704000,
      1510790400
    ],
    "loadTimes": [
      -1,
      3.2,
      3.3
    ]
  },
  {
    "url": "http://bing.com",
    "name": "Bing",
    "id": "59d5ed3df8894e866e0041ab",
    "timestamps": [
      1510617600,
      1510704000,
      1510790400
    ],
    "loadTimes": [
      1.2,
      0.5,
      0.7
    ]
  ...
]
```

Retrieve the load times for all competitors in a given landscape. 

This endpoint will automatically normalise the time period specified into 24-hour day precision represented in the output as unix timestamps at midight of all days over the given period. If more than one performance result exists in the 24 hour period, an average of all results is provided for a given day.

Landscapes may be enumurated to obtain their ID's by using the [landscapes](#landscapes) endpoint

### HTTP Request

`GET https://go.competeshark.com/api/v1/performance?start=<start_timestamp>&end=<end_timestamp>&landscape=<landscape_id>`

### URL Parameters

Parameter | Mandatory? | Description
--------- | ----------- | -----------
start_timestamp | No | The start of the period from which to retrive performance data in the form of a unix timestamp
end_timestamp | No | The end of the period from which to retrive performance data in the form of a unix timestamp
landscape_id | Yes | The ID if the landscape from which to retrieve the performance data


