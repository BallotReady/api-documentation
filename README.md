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
7. [Data Dictionary](#data_dictionary)


## Elections API  <a name="elections_api"></a>
**Parameters:**

      state - state the election takes place in
      end_at -  end timestamp of queried elections in the search request
      updated_since - beginning timestamp of record updates in the search request
  
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
      "id": int
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
      tenant - the customer id
      year 
      


**Request Syntax:**
      
      To query candidate positions based on address: 
      ```
      curl -H "x-api-key: APIKEY" "https://api.civicengine.com/positions?include_candidates=1&address=350+5th+New+York+NY+10118"
      ```

**Return Type:**

JSON dictionary

**Returns:**
```
{
  "timestamp": "2018-08-06T22:45:19.142297",
  "positions": [
    {
      "general_filing_end": "2018-07-31",
      "salary": "174000.00",
      "description": "The US Senate is one of two chambers of the federal legislature.  Senators are responsible for writing and passing legislation, approving presidential appointments, and ratifying treaties with foreign countries.",
      "number_of_seats": 1,
      "position_id": 46210,
      "position_type": null,
      "employment_type": "Full Time",
      "level": "FEDERAL",
      "paperwork_instructions": "File with State Board of Elections and FEC",
      "eligibility_requirements": "Senator must be at least thirty years, have been a citizen of the United States for nine years, and must be an inhabitant of the State in which they are running.",
      "general_date": "NOV",
      "primary_date": "SEP",
      "has_unknown_boundaries": false,
      "state": "NY",
      "runoff_date": null,
      "sub_area_value": null,
      "normalized_position": {
        "id": 2,
        "mtfcc": "G4000",
        "description": null,
        "name": "US Senate",
        "level": "federal"
      },
      "sub_area_name": null,
      "primary_filing_end": "2018-04-12",
      "candidates": [
        {
          "urls": [
            {
              "url": "https://www.chelefarleyforsenate.com/",
              "entry_type": "website",
              "url_id": 95186,
              "type": "website"
            },
            {
              "url": "https://www.facebook.com/CheleFarley/",
```

### Notes on Election Results <a name="election_results"></a>

In the case of a PAST election, the election result will be in the candidate object returned above as the `election_result` object. It can take one of three values (WON, LOST, RUNOFF, JUNGLE_WIN).  Below is an example of a snippet of the candidate response with an election result in it.

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

**Request Syntax:**
      To query candidates:
      
      ```
      curl -H "x-api-key: API_KEY" "https://api.civicengine.com/candidate/1"
      ```
      
**Return Type:**

JSON dictionary
      
**Returns:**

Below is sample return dictionary for a candidate request. Note that "stances" are embedded within "issues". For instance, a candidate may have stances about the issue of National Security.

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
    }]
}
```

## Measures API  <a name="measures_api"></a>
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
    "mtfcc": null,
    "id": 2090,
    "name": "Township Constable"
  },
  {
    "mtfcc": null,
    "id": 2000,
    "name": "Party Officer - City"
  },
  {
    "mtfcc": null,
    "id": 2040,
    "name": "Township Executive"
  },
  {
    "mtfcc": null,
    "id": 1630,
    "name": "City Taxpayer Advocate"
  },
  {
    "mtfcc": null,
    "id": 2380,
    "name": "Local Higher Education Board"
  },
  {
    "mtfcc": null,
    "id": 2060,
    "name": "Township Legislative"
  },
  {
    "mtfcc": null,
    "id": 1780,
    "name": "City Court Clerk"
  },
  {
    "mtfcc": null,
    "id": 4030,
    "name": "Judicial Circuit Court (1)"
  },
  {
    "mtfcc": null,
    "id": 1820,
    "name": "Fire Committee"
  },
  {
    "mtfcc": null,
    "id": 2460,
    "name": "Regional Planning District"
  },
  {
    "mtfcc": null,
    "id": 1600,
    "name": "City Collector"
  },
  {
    "mtfcc": null,
    "id": 2550,
    "name": "Mosquito Abatement District"
  },
  {
    "mtfcc": null,
    "id": 2320,
    "name": "Combination - Fire And Healthcare District"
  },
  {
    "mtfcc": null,
    "id": 925,
    "name": "County Trustee"
  },
  {
    "mtfcc": null,
    "id": 1290,
    "name": "County Superintendent Of Schools"
  },
  {
    "mtfcc": null,
    "id": 1330,
    "name": "County Road Commissioner"
  },
  {
    "mtfcc": null,
    "id": 2030,
    "name": "Township Collector"
  },
  {
    "mtfcc": null,
    "id": 1580,
    "name": "City Auditor"
  },
  {
    "mtfcc": null,
    "id": 2430,
    "name": "Forest District"
  },
  {
    "mtfcc": null,
    "id": 980,
    "name": "County Sheriff"
```

## Elected Officials API  <a name="elected_officials"></a>

This API, when given an address OR a (latitude, longitude) pair will return the office holders (also known as elected officials) for the given location.

**Parameters:**
* address - Address (Required, OR lat/lng is required)
* lat - Latitude 
* lng - Longitude 

**Request Syntax:**
curl -H "x-api-key: APIKEY" "https://api.civicengine.com/office_holders?address=60202"

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

