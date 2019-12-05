# CivicEngine API Documentation

**API Key:** APIKEY
**API Host:** api.civicengine.com


## Table of contents
1. [Elections API](#elections_api)
2. [Positions API](#positions_api)
2a. [Election Results](#election_results)
3. [Candidates API](#candidates_api)
4. [Measures API](#measures_api)
5. [Normalized Positions API](#norm_positions_api)
6. [Elected Officials API](#elected_officials)
7. [Districts API](#districts)


## Elections API  <a name="elections_api"></a>
**Parameters:**

      state - state the election takes place in (optional)
      start-at - starting timestamp of queried elections (optional)
      end_at -  end timestamp of queried elections in the search request (optional)
      updated_since - beginning timestamp of record updates in the search request (optional)

**Request Syntax:**

      To query the election IDs, you can hit the /elections endpoint:

      curl -H "x-api-key: APIKEY" "https://api.civicengine.com/elections"

**Return Type:**

JSON dictionary

**Returns:**

```
{
  "timestamp": datetime,
  "elections": [
    {
      "ocd_id": string,
      "name": string,
      "election_day": date_string,
      "updated_at": datetime,
      "state": string,
      "id": int,
      "type": string,
    }]
}
```


## Positions API <a name="positions_api"></a>
**Parameters:**
      Note: Users can search with EITHER address or lat/lon

      address - primary search criteria
      county - the county the position is held in
      election_date - set an election_date to return only candidates who are up for election on that date
      election_id - if you include candidates, you can filter by a specific election_id (see below)
      exclude_statewide - option to exclude statewide positions
      include_candidates - choose to include candidates in API response or not
      include_endorsements - choose to include endorsements in API response or not
      include_office_holders - choose to include office holders in API response or not
      include_volunteer_urls  - choose to include volunteer urls in API response or not
      level - (federal/state/local/county) - return only positions at a single level
      lat/lon (optional) - instead of using address, pass lat/lon and bypass geocoding
      search_radius - return positions within X miles of address (up to 30)
      state - the state the position is held in
      year



**Request Syntax:**

      To query candidate positions based on address:
      ```
      curl "https://api.civicengine.com/positions?include_candidates=1&address=350%2B5th%2BNew%2BYork%2BNY%2B10118" \
     -H 'x-api-key: APIKEY'
      ```

**Return Type:**

JSON dictionary

**Returns:**
```
{
  "timestamp": "2019-08-05T21:38:48.608189",
  "positions": [
    {
      "position_id": 268420,
      "paperwork_instructions": null,
      "general_date": "2019-02-26",
      "sub_area_value": null,
      "normalized_position": {},
      "sub_area_name": null,
      "retention": false,
      "unexpired_term": true,
      "employment_type": null,
      "primary_date": "",
      "state": "NY",
      "candidates": [
        {
          "urls": [
            {
              "url": "https://melissamarkviverito.com/",
              "entry_type": "website",
              "url_id": 154958,
              "type": "website"
            },
            {
              "url": "https://www.facebook.com/mmviverito/",
              "entry_type": "facebook",
              "url_id": 154960,
              "type": "facebook"
            },
            {
              "url": "https://twitter.com/MMViverito",
              "entry_type": "twitter",
              "url_id": 154963,
              "type": "twitter"
            }
          ],
          "first_name": "Melissa",
          "last_name": "Mark-Viverito",
          "election_result": null,
          "suffix": null,
          "incumbent": false,
          "position_id": 268420,
          "election_id": 370,
          "election_day": "2019-02-26",
          "endorsements": [
            10,
            2163
          ],
          "id": 305505,
          "party_name": "Democratic",
          "middle_name": null,
          "thumb_url": null,
          "nickname": null,
          "slug": "melissa-mark-viverito",
          "photo_url": null
        }
      ],
      "general_filing_end": "",
      "description": "The office of Public Advocate for the City of New York is a citywide elected position in New York City, which is first in line to succeed the Mayor. The office serves as a direct link between the electorate and city government, effectively acting as an ombudsman, or \"watchdog,\" for New Yorkers.",
      "eligibility_requirements": null,
      "has_unknown_boundaries": false,
      "slug": null,
      "la_style": false,
      "salary": null,
      "number_of_seats": 1,
      "name": "New York City Public Advocate (unexpired term)",
      "level": "LOCAL",
      "position_type": null,
      "runoff_date": null,
      "judicial": false,
      "primary_filing_end": ""
    }
  ],
  "address": "350+5th+New+York+NY+10118",
  "coords": {
    "latitude": 40.7482436,
    "longitude": -73.9851073
  },
  "result_count": 1
}
```

### Notes on Election Results <a name="election_results"></a>

In the case of a PAST election, the election result will be in the candidate object returned above as the `election_result` object. It can take one of three values (LOSE, WIN, RUNOFF, PRIMARY WIN).  Below is an example of a snippet of the candidate response with an election result in it.

```
          "first_name": "Clare",
          "last_name": "Quish",
          "election_result": "WON",
          "suffix": "",
          "incumbent": false,
          "position_id": 78977,
          "election_id": 5,
          "election_day": "2018-03-20",
```

The best way to make sure you get only the values for the election you want is to query on the `election_date` parameter. Once the election passes, we'll being updating the `election_result` flags.


## Candidates API <a name="candidates_api"></a>
**Parameters:**

      tenant_id - the customer id
      election_id - without an election ID, then certain fields (should as stances) will be empty. A candidates stances are specifically linked to an election cycle, which is linked to an election_id

**Request Syntax:**
      To query candidates:

      ```
      curl -H "x-api-key: API_KEY" "https://api.civicengine.com/candidate/1"
      ```

**Return Type:**

JSON dictionary

**Returns:**

Below is sample return dictionary for a candidate request. Note that "stances" are embedded within `issues.stances`. For instance, a candidate may have stances about the issue of National Security.

```
{
  "thumb_url": string,
  "urls": [
    {
      "url": string
      "type": enum(twitter, facebook, website)
    }
  ],
  "first_name": string,
  "last_name": string,
  "middle_name": string,
  "suffix": string,
  "issues": [
    {
      "is_question": boolean,
      "issue_id": int,
      "name": string,
      "question_text": string,
      "stances": [
        {
          "reference_url": string,
          "stance_id": int,
          "candidate_id": int,
          "description": string
         }
       ]
  }],
  "endorsements": [
    {
      "logo_url": string,
      "id": int,
      "website_url": string,
      "name": string
    }],
  "experience":[
    {
      "start_year": int,
      "entry_type": string,
      "company": string,
      "end_year" int,
      "duration": string,
      "position": "string"
    }
  ],
  "candidacies": [
    {
      "is_running_mate": bool,
      "position_id": int,
      "election_day": string,
      "state": string,
      "sub_area_name_secondary": string,
      "sub_area_value": string,
      "party_short_name": string,
      "party_name": string,
      "position_name": string,
      "incumbent": bool,
      "row_order": int,
      "sub_area_name": string,
      "running mate": int,
      "election_id": int,
      "sub_area_value_secondary": string
    },
    ...
  ],
  "bar_association_evaluations": [],
  "education":[]
}
```

## Measures API  <a name="measures_api"></a>

This API, when give an address or Lat/Longitude pair, will return all measures up for election on a given election date.

**Request Syntax:**
```
curl -H "x-api-key: APIKEY" "https://api.civicengine.com/measures?address=60202&election_date=2018-11-07"
```
The measures API accepts the following parameters:
* lng - longitude
* lat - latitude to search for
* address - address to search for
* election_id
* election_date

Note that either (lng, lat) OR an address is required AND an election_id OR an election_date is required.

**Return Type:**
JSON dictionary

** Returns**
```
{
  "timestamp": datetime,
  "positions": [
    {
      "pro_snippet": string,
      "con_snippet": string,
      "title": string,
      "text": string,
      "summary": string,
      "state": string,
      "row_order": int,
      "name":  string
    }
  ],
  "coords": {
    "latitude": float,
    "longitude": float,
  },
  "result_count": int
}
```

## Normalized Positions API <a name="norm_positions_api"></a>

This API will return the full list of normalized positions. Normalized positions are a standardized way of handling position types - for instance, US Senators will all have the same normalized position. So will "City Dogcatcher" or any other elected position. This allows us to represent office holders and election candidates across multiple locations with an id identifying the role.

**Parameters:**

None

**Request Syntax:**
curl -H "x-api-key: APIKEY" "https://api.civicengine.com/normalized-positions"

**Return Type:**

JSON dictionary

**Returns:**
```
[
  {
    "mtfcc": string,
    "id": integer,
    "name": string
  },
]
```

## Elected Officials API  <a name="elected_officials"></a>

This API, when given an address OR a (latitude, longitude) pair will return the office holders (also known as elected officials) for the given location. Note: the endpoint has a dash in it `office-holders` and not an underscore.

**Parameters:**
* address - Address (Required, OR lat/lng is required)
* lat - Latitude
* lng - Longitude

**Request Syntax:**
curl -H "x-api-key: APIKEY" "https://api.civicengine.com/office-holders?address=60202"

**Return Type:**

JSON dictionary

**Returns:**

```
{
  "timestamp": datetime,
  "office_holders": list,
  "coords": {
    "latitude": float,
    "longitude": float
  },
  "result_count": integer
}
```

The `office_holders` list will consist of office holder records in the form:

```
    {
      "urls": [
        {
          "url":  string,
          "type": enum(website, facebook, twitter)
        }
      ],
      "first_name": string,
      "last_name": string,
      "start_at": string,
      "suffix": string,
      "level": enum(FEDERAL, STATE, LOCAL, PARTY),
       "normalized_position": {
        "id": int,
        "mtfcc": string,
        "description": string,
        "name": string,
        "level": string,
      },
      "position_id": int,
      "position_type": string,
      "end_at": string,
      "party_name": string,
      "candidate_id": int,
      "position_name": string,
      "middle_name": string,
      "thumb_url": string,
      "nickname": string,
      "photo_url": string,
      }
```



## Districts API  <a name="districts"></a>

The districts API takes a latitude and longitude and returns the matching districts for that location. Note that this API does not return matching positions but rather returns matching districts only without any election-specific information. This is useful if you want to return which congressional district or state legislative district an address is in. If you are looking for election specific information, please use the `/positions` API above.

**Parameters:**

    * address - Address (Required, OR lat/lng is required)
    * lat - Latitude
    * lng - Longitude

**Request Syntax:**

      To query the election IDs, you can hit the /elections endpoint:

      curl -H "x-api-key: APIKEY" "https://api.civicengine.com/districts?address=1060+W+Addison+St+Chicago+IL+60613"

**Return Type:**

JSON dictionary

**Returns:**

```
{
  "timestamp": datetime,
  "coords": {
    "latitude": float,
    "longitude": float
  },
  "results": [
    {
      "district_type": string,
      "name": string
      "district_no": string,
      "id": string
    },
```
