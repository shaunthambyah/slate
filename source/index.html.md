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

# landscapes

## All Landscapes

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

# landscapeDetails

## Details of a landscape

```shell
curl "https://go.competeshark.com/api/v1/landscapeDetails?landscape=59d455c8f8894e896e0041a8"
  -u "api:YOUR_GENERATED_API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "url": "http://brand_a.com",
    "name": "Brand A",
    "id": "59d455c8f8894e896e0041a9",
    "primary": true,
    "result": {
      "lastProcessedScreenshot": "https://imgcdn.competeshark.com/unsafe/5a167b0bf8894ec53e0041af1511422751010185800.png",
      "lastScannedScreenshot": "https://go.competeshark.com/images/5a1692aef8894e03400041b9.png"
    }
  },
  {
    "url": "http://brand_b.com/some_url",
    "name": "Brand B",
    "id": "59d5ed3df8894e866e0041ac",
    "primary": false,
    "result": {
      "lastProcessedScreenshot": "https://imgcdn.competeshark.com/unsafe/59e59e26f8894e78340041ac1508220481089095300.png",
      "lastScreenshot": "https://go.competeshark.com/images/59edae8af8894e8d090041b4.png"
    }
  }
  ...
]
```

Provides a list of sites assosciated with a given Landscape ID. Each ID returned is in turn a unique reference for additional requests relative to each site/url.

Landscapes may be enumurated to obtain their ID's by using the [landscapes](#landscapes) endpoint

### HTTP Request

`GET https://go.competeshark.com/api/v1/landscapeDetails?landscape=<landscape_id>`

### URL Parameters

Parameter | Mandatory? | Description
--------- | ----------- | -----------
landscape_id | Yes | The ID of the landscape from which to retrieve the list of sites/urls

### Returns

An array of Site objects

### Return values

value | Type |Description
--------- | ----------- | -----------
url | String | The URL of a given site
name | String | The friendly name of a given URL as defined on the Companies screen
id | String | The Unique identifier for this site
Primary | Boolean | True if the URL is defined as primary for this landscape on the Companies screen. False if not. There can only be one Primary per landscape
result | Object | Object containing the last processed screenshot and capture timestamp and last unprocessed screenshot and capture timestamp 
 | lastProcessedScreenshot | The screenshot of the last post processed capture
 | lastScreenshot | The most recent sceenshot of this site/url

# updates

## Update summaries for a site

```shell
curl "https://go.competeshark.com/api/v1/updates?start=1510669397&end=1510761397&site=59d5ed3df8894e866e0041ac"
  -u "api:YOUR_GENERATED_API_KEY"
```

> The above command returns JSON structured like this:

```json
[
{
    "timestamp": 1511422768,
    "id": "5a167b30f8894ec53e0041cf",
    "name": "Brand A",
    "url": "http://brand_a.com",
    "loadTime": 8615,
    "previousLoadTime": 8866,
    "changeCategories": [
      "Content"
    ],
    "favourite": false,
    "screenshots": {
      "before": "https://imgcdn.competeshark.com/unsafe/59f02cb4f8894e41290041c61511422738018598000.png",
      "after": "https://imgcdn.competeshark.com/unsafe/5a167b0bf8894ec53e0041af1511422751010185800.png",
      "beforeThumb": "https://imgcdn.competeshark.com/unsafe/59f02cb6f8894e41290041cf1511422748052167800.png",
      "afterThumb": "https://imgcdn.competeshark.com/unsafe/5a167b0bf8894ec53e0041b71511422763059568800.png"
    },
    "averageLoadTimeForPeriod": 8973.2
  },
  {
    "timestamp": 1508912353,
    "id": "59f02ce1f8894e41290041d1",
    "name": "Brand A",
    "url": "http://brand_a.com",
    "loadTime": 8866,
    "previousLoadTime": 11036,
    "changeCategories": [
      "Content",
      "Experiment"
    ],
    "favourite": false,
    "screenshots": {
      "before": "https://imgcdn.competeshark.com/unsafe/59eee832f8894e7e0a0041c01508912287079851100.png",
      "after": "https://imgcdn.competeshark.com/unsafe/59f02c97f8894e41290041af1508912310036864500.png",
      "beforeThumb": "https://imgcdn.competeshark.com/unsafe/59eee834f8894e7e0a0041c61508912308035898600.png",
      "afterThumb": "https://imgcdn.competeshark.com/unsafe/59f02c97f8894e41290041b71508912347078501400.png"
    },
    "averageLoadTimeForPeriod": 8973.2
  }
  ...
]
```

Provides a list of updates for a given site by site ID within the specified time period. If no time period is specified, then all available updates are returned. Each ID returned is in turn a unique reference for additional requests relative to each result.

Sites may be enumurated to obtain their ID's by using the [landscape details](#landscapedetails) endpoint

### HTTP Request

`GET https://go.competeshark.com/api/v1/updates?start=<start_timestamp>&end=<end_timestamp>&site=<site_id>`

### URL Parameters

Parameter | Mandatory? | Description
--------- | ----------- | -----------
start_timestamp | No | The start of the period from which to retrive updates in the form of a unix timestamp
end_timestamp | No | The end of the period from which to retrive updates in the form of a unix timestamp
site_id | Yes | The ID of the site from which to retrieve the list of sites/urls

### Returns

An array of Result objects

### Return values

value | Type |Description
--------- | ----------- | -----------
timestamp | Integer | The unix timestamp of this update in GMT
id | String | The Unique identifier for this update
name | String | The friendly name of this site as defined on the Companies screen
url | String | The URL of this site
loadTime | Integer | The load time of this update
previousLoadTime | Integer | The load time of the last update for this site
changeCategories | Array | A combined array of both system defined and user defined categories for this update
favourite | Boolean | True if this update has been marked as a favourite on the Updates screen, false if not
screenshots | Object | Object containing links to the before and after screenshots (and thumbnails) for this update 
 | before | Screenshot of the site before this update was captured
 | after | Screenshot of the site at the time of the update
 | beforeThumb | Thumbnail of the before screenshot
 | afterThumb | Thumbnail of the after screenshot

# updateDetails

## Details of an update

```shell
curl "https://go.competeshark.com/api/v1/updateDetails?update=59f02ce1f8894e41290041d1"
  -u "api:YOUR_GENERATED_API_KEY"
```

> The above command returns JSON structured like this:

```json
{
  "swipe": "https://go.competeshark.com/public/59f02ce1f8894e41290041d1",
  "screenshots": {
    "before": "https://imgcdn.competeshark.com/unsafe/59eee791f8894e4b0a0041c61508829207085294800.png",
    "after": "https://imgcdn.competeshark.com/unsafe/59eee812f8894e7e0a0041ae1508829237000223800.png",
    "difference": "https://imgcdn.competeshark.com/unsafe/59eee80ff8894e7e0a0041a81508829252053491400.png"
  },
  "addedLinks": [
    {
      "href": "http://brand-a.com/added_link_1",
      "text": "Added link 1",
      "state": "added"
    },
    {
      "href": "http://brand-a.com/added_link_2",
      "text": "Added link 2",
      "state": "added"
    },
    ...
  ],
  "removedLinks": [
    {
      "href": "http://brand-a.com/removed_link_1",
      "text": "Removed link 1",
      "state": "removed"
    },
    {
      "href": "http://brand-a.com/removed_link_2",
      "text": "Removed link 2",
      "state": "removed"
    },
    ...
  ],
  "changedLinks": [
    {
      "href": "http://brand-a.com/changed_link_1",
      "text": "Changed Link 1",
      "state": "changed"
    },
    {
      "href": "http://brand-a.com/changed_link_2",
      "text": "Changed link 2",
      "state": "changed"
    },
    ...
  ],
  "addedHeaders": {
    "h1": [
      {
        "text": "Added header 1",
        "state": "added"
      },
      {
        "text": "Added header 2",
        "state": "added"
      },
      ...
    ],
    "h2": [],
    "h3": [],
    "h4": [],
    "h5": [],
    "h6": []
  },
  "removedHeaders": {
    "h1": [
      {
        "text": "Removed header 1",
        "state": "removed"
      },
      {
        "text": "Removed header 2",
        "state": "removed"
      }
    ],
    "h2": [],
    "h3": [],
    "h4": [],
    "h5": [],
    "h6": []
  },
  "seo": [
    {
      "type": "Description",
      "content": "Description content added",
      "state": "added"
    },
    {
      "type": "Description",
      "content": "Description content changed",
      "state": "changed"
    },
    ...
  ]
}
```

Provides detailed information on the given update.

Updates may be enumurated to obtain their ID's by using the [updates](#updates) endpoint

### HTTP Request

`GET https://go.competeshark.com/api/v1/updateDetails?update=<update_id>`

### URL Parameters

Parameter | Mandatory? | Description
--------- | ----------- | -----------
update_id | Yes | The ID of the update from which to retrieve the details

### Returns

Update result object

### Return values

value | Type |Description
--------- | ----------- | -----------
swiper | String | Link to the publically available swipe URL for this update
screenshots | Object | Object containing links to the before and after screenshots (and thumbnails) for this update 
 | before | Screenshot of the site before this update was captured
 | after | Screenshot of the site at the time of the update
 | difference | Differenced image of the before vs after screenshot
addedLinks | Array | Array of links that have been added in this update
 | href | The link added
 | text | The text anchor of the added link
 | state | Added
removedLinks | Array | Array of links that have been removed in this update
 | href | The link removed
 | text | The text anchor of the removed link
 | state | Removed
changedLinks | Array | Array of links that have been changed in this update
 | href | The link changed
 | text | The text anchor of the changed link
 | state | Changed
addedHeaders | Array | Array of headers that have been added in this update (broken down by h1 -> h6)
 | h1 | H1 links added, array of objects containing "text" (text value of header tag) and "state" (added)
 | h2 | H2 links added, array of objects containing "text" (text value of header tag) and "state" (added)
 | h3 | H3 links added, array of objects containing "text" (text value of header tag) and "state" (added)
 | h4 | H4 links added, array of objects containing "text" (text value of header tag) and "state" (added)
 | h5 | H5 links added, array of objects containing "text" (text value of header tag) and "state" (added)
 | h6 | H6 links added, array of objects containing "text" (text value of header tag) and "state" (added)
removedHeaders | Array | Array of headers that have been removed in this update (broken down by h1 -> h6)
 | h1 | H1 links removed, array of objects containing "text" (text value of header tag) and "state" (removed)
 | h2 | H2 links removed, array of objects containing "text" (text value of header tag) and "state" (removed)
 | h3 | H3 links removed, array of objects containing "text" (text value of header tag) and "state" (removed)
 | h4 | H4 links removed, array of objects containing "text" (text value of header tag) and "state" (removed)
 | h5 | H5 links removed, array of objects containing "text" (text value of header tag) and "state" (removed)
 | h6 | H6 links removed, array of objects containing "text" (text value of header tag) and "state" (removed)
seo | Array | Array of SEO changes that have been captured in this update
 | type | The meta or title tag being optimised
 | content | The content of the tag
 | state | Changed/added/removed

# performance

## Competitor load times

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
  }
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
landscape_id | Yes | The ID of the landscape from which to retrieve the performance data

### Returns

An array of Sites containing their load times

### Return values

value | Type |Description
--------- | ----------- | -----------
url | String | The URL of a given site
name | String | The friendly name of a given URL as defined on the Companies screen
id | String | The Unique identifier for this site
timestamps | Array | Array of timestamps taken at midnight GMT starting from the midnight timestamp immediately after start_timestamp including every midnight timestamp until the midnight timestamp immediately preceeding end_timestamp. These timestamps represent a 24hour day. All loadtimes are averaged within that 24 hour period.
loadTimes | Array | Array of load times corresponding to the timestamp of the equivalent index. Valid load times are in seconds in single precision and non-negative. Where no load time is available for a given timestamp, -1 is returned to indicate no value is available for that day as 0 is a valid value.

# changeCategories

## Available change tags

```shell
curl "https://go.competeshark.com/api/v1/changeCategories?landscape=59d455c8f8894e896e0041a8"
  -u "api:YOUR_GENERATED_API_KEY"
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": "58007323c048cb457701f39d",
    "label": "Content",
    "source": "system"
  },
  {
    "id": "58007317c048cb814201f39a",
    "label": "Optimisation",
    "source": "system"
  }
  ...
]
```

Retrieve a list of all the available change categories/tags for a given landscape.

Some change categorisation (price, offer, experiment etc) is done by Competeshark. These will be listed with a source value of "system" in the output. Other categorisation of changes can be done by a user within the competeshark console via the updates screen, these tags will be listed as "user". Users have the ability to add as many custom tags as they wish to changes and these tags will be reflected across the landscape, but will not transfer to other landscapes. User and System tags are used for the change insights functionality.

Landscapes may be enumurated to obtain their ID's by using the [landscapes](#landscapes) endpoint

### HTTP Request

`GET https://go.competeshark.com/api/v1/changeCategories?landscape=<landscape_id>`

### URL Parameters

Parameter | Mandatory? | Description
--------- | ----------- | -----------
landscape_id | Yes | The ID of the landscape from which to retrieve the categortisation tags

### Returns

An array of categorisation tags

### Return values

value | Type |Description
--------- | ----------- | -----------
id | String | The Unique identifier for this categorisation tag
label | String | The friendly name of this categorisation tag
source | String | "system" if generated by competeshark, "user" if added to this landscape by a user

# changeCount

## Category count for a change

```shell
curl "https://go.competeshark.com/api/v1/changeCount?start=1509953917&end=1512545917&landscape=59c21456c048cba03e1a8eff"
  -u "api:YOUR_GENERATED_API_KEY"
```

> The above command returns JSON structured like this:

```json
[
    {
        "url": "http://somebrand.com",
        "name": "Some Brand",
        "id": "5732ec1bc048cbac1997949f",
        "changeCategories": [
            {
                "id": "58007376c048cb707601f39d",
                "label": "Design",
                "source": "system",
                "count": 0
            },
            {
                "id": "58007368c048cb0c4f01f39b",
                "label": "Product",
                "source": "system",
                "count": 10
            },
            {
                "id": "5800735bc048cba31501f398",
                "label": "Pricing",
                "source": "system",
                "count": 0
            },
            {
                "id": "5800733dc048cb0c4f01f399",
                "label": "Offer",
                "source": "system",
                "count": 24
            },
            {
                "id": "58007330c048cb347701f39e",
                "label": "Experiment",
                "source": "system",
                "count": 0
            },
            {
                "id": "58007323c048cb457701f39d",
                "label": "Content",
                "source": "system",
                "count": 8
            },
            {
                "id": "58007317c048cb814201f39a",
                "label": "Optimisation",
                "source": "system",
                "count": 1
            }
        ]
    },
    ...
  ]
```

Retrieve a list of sites in the given landscape with change counts for each over the specified period

This endpoint summarises the counts of all changes fior a landscape over the specified period. Where user change categories exist for the landscape, they are also listed and counted here. This endpoint is representive of the content type analysis feature within change insights of the competeshark console.

Landscapes may be enumurated to obtain their ID's by using the [landscapes](#landscapes) endpoint

### HTTP Request

`GET https://go.competeshark.com/api/v1/changeCount?start=<start_timestamp>&end=<end_timestamp>&landscape=<landscape_id>`

### URL Parameters

Parameter | Mandatory? | Description
--------- | ----------- | -----------
start_timestamp | No | The start of the period from which to retrive change count data in the form of a unix timestamp
end_timestamp | No | The end of the period from which to retrive change count data in the form of a unix timestamp
landscape_id | Yes | The ID of the landscape from which to retrieve the change count data


### Returns

An array of sites containing their change counts

### Return values

value | Type |Description
--------- | ----------- | -----------
url | String | The URL of a given site
name | String | The friendly name of a given URL as defined on the Companies screen
id | String | The Unique identifier for this site
changeCategories | Array | Array of change categories 
 | id | the change category ID 
 | label | the friendly name of the change category
 | source | system if this change category is generated by competeshark, user if this is a user generated change category
 | count | the count of these changes over the specified period


# changeFrequency

## Frequency of change tags

```shell
curl "https://go.competeshark.com/api/v1/changeFrequency?start=1509953917&end=1512545917&category=58007323c048cb457701f39d&landscape=59c21456c048cba03e1a8eff"
  -u "api:YOUR_GENERATED_API_KEY"
```

> The above command returns JSON structured like this:

```json
[
    {
        "url": "",
        "name": "All competitors",
        "id": "0",
        "timestamps": [
            1509926400,
            1510012800,
            1510099200,
            1510185600
        ],
        "count": [
            0,
            2,
            0,
            1
        ]
    },
    {
        "url": "http://branda.com",
        "name": "Brand A",
        "id": "59d455c8f8894e896e0041a9",
        "timestamps": [
            1509926400,
            1510012800,
            1510099200,
            1510185600
        ],
        "count": [
            0,
            1,
            0,
            1
        ]
    },
    {
        "url": "http://brandb.com",
        "name": "Brand B",
        "id": "59d5ed3df8894e866e0041ac",
        "timestamps": [
            1509926400,
            1510012800,
            1510099200,
            1510185600
        ],
        "count": [
            0,
            1,
            0,
            0
        ]
    },
```
Retrieve the occurance of change categorisation tags for a given timestamp 

This endpoint will automatically normalise the time period specified into 24-hour day precision represented in the output as unix timestamps at midight of all days over the given period. Counts correspond to the given timestamp and provide a total of all changes that contain the speficied change categorisation tag for that timestamp. If no categorisation tag is provided, then a count of all catgegorisation tags is returned. 

The first item in the result set is a count of all competitors to provide a landscape view.

Landscapes may be enumurated to obtain their ID's by using the [landscapes](#landscapes) endpoint
Categories may be enumurated to obtain their ID's by using the [changeCategories](#changeCategories) endpoint

### HTTP Request

`GET https://go.competeshark.com/api/v1/changeFrequency?start=<start_timestamp>&end=<end_timestamp>&category=<category_id>&landscape=<landscape_id>`

### URL Parameters

Parameter | Mandatory? | Description
--------- | ----------- | -----------
start_timestamp | No | The start of the period from which to retrive change frequency data in the form of a unix timestamp
end_timestamp | No | The end of the period from which to retrive change frequency data in the form of a unix timestamp
category_id | No | The ID of the change category from which to retrieve the change frequency data
landscape_id | Yes | The ID of the landscape from which to retrieve the change frequency data

### Returns

An array of Sites containing their change frequency with the first element a summary of the entire landscape as a cumulative total

### Return values

value | Type |Description
--------- | ----------- | -----------
url | String | The URL of a given site
name | String | The friendly name of a given URL as defined on the Companies screen
id | String | The Unique identifier for this site
timestamps | Array | Array of timestamps taken at midnight GMT starting from the midnight timestamp immediately after start_timestamp including every midnight timestamp until the midnight timestamp immediately preceeding end_timestamp. These timestamps represent a 24hour day. All counts are cumulative within that 24 hour period.
count | Array | Array of change counts corresponding to the timestamp of the equivalent index. Counts are a cumulative total of all occurances of the given change category (or all categories if none is specified) for the 24 hour period of the corresponding index.
