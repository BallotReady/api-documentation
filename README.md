# CivicEngine API Documentation

**API Key:** APIKEY
**API Host:** api.civicengine.com


## Table of contents
1. [Elections API](#elections_api)
2. [Positions API](#positions_api)
3. [Candidates API](#candidates_api)
3. [Data Dictionary](#data_dictionary)


## Elections API  <a name="elections_api"></a>
**Parameters:**

      address - primary search criteria
      lat/lon (optional) - instead of using address, pass lat/lon and bypass geocoding
      include_candidates - choose to include candidates in API response or not
      election_id - if you include candidates, you can filter by a specific election_id (see below)
      level - (federal/state/local/county) - return only positions at a single level
      search_radius - return positions within X miles of address (up to 30)

**Request Syntax:**

      To query the election IDs, you can hit the /elections endpoint:
      
      curl -H "x-api-key: APIKEY" "https://api.civicengine.com/elections"
      
**Return Type:**

JSON dictionary

**Returns:**

```
{
  "timestamp": "2018-08-06T23:08:42.107793",
  "elections": [
    {
      "ocd_id": "ocd-division/country:us/state:WA",
      "name": "Washington 2018 Primary Election",
      "election_day": "2018-08-07",
      "updated_at": "2017-10-14T15:22:20.102000",
      "state": "WA",
      "id": 339
    },
    {
      "ocd_id": null,
      "name": "Ohio 08.07.18 Special Election",
      "election_day": "2018-08-07",
      "updated_at": "2018-07-28T20:34:00.938562",
      "state": "OH",
      "id": 360
    },
    {
      "ocd_id": "ocd-division/country:us/state:MO",
      "name": "Missouri 2018 Primary Election",
      "election_day": "2018-08-07",
      "updated_at": "2018-08-05T01:52:52.084826",
      "state": "MO",
      "id": 338
    },
    {
      "ocd_id": "ocd-division/country:us/state:MI",
      "name": "Michigan 2018 Primary Election",
      "election_day": "2018-08-07",
      "updated_at": "2018-07-28T16:47:59.855969",
      "state": "MI",
      "id": 337
    },
    {
      "ocd_id": "ocd-division/country:us/state:KS",
      "name": "Kansas 2018 Primary Election",
      "election_day": "2018-08-07",
      "updated_at": "2018-08-05T01:47:44.698766",
```


## Positions API <a name="positions_api"></a>
**Parameters:**

      address - primary search criteria
      lat/lon (optional) - instead of using address, pass lat/lon and bypass geocoding
      include_candidates - choose to include candidates in API response or not
      election_id - if you include candidates, you can filter by a specific election_id (see below)
      level - (federal/state/local/county) - return only positions at a single level
      search_radius - return positions within X miles of address (up to 30)

**Request Syntax:**
      
      To query candidate positions based on address: 
      
      curl -H "x-api-key: APIKEY" "https://api.civicengine.com/positions?include_candidates=1&address=350+5th+New+York+NY+10118"

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



## Candidates API <a name="candidates_api"></a>
**Parameters:**

      address - primary search criteria
      lat/lon (optional) - instead of using address, pass lat/lon and bypass geocoding
      include_candidates - choose to include candidates in API response or not
      election_id - if you include candidates, you can filter by a specific election_id (see below)
      level - (federal/state/local/county) - return only positions at a single level
      search_radius - return positions within X miles of address (up to 30)

**Request Syntax:**
      To query candidates:
      
      curl -H "x-api-key: API_KEY" "https://api.civicengine.com/candidate/1"
      
**Return Type:**

JSON dictionary
      
**Returns:**
```
{
  "thumb_url": "https://br-production-assets.s3.amazonaws.com/uploads/candidate/headshot/1/thumb_1.jpg",
  "urls": [
    {
      "url": "https://twitter.com/HillaryClinton",
      "type": "twitter"
    },
    {
      "url": "https://www.hillaryclinton.com/",
      "type": "website"
    }
  ],
  "first_name": "Hillary",
  "last_name": "Clinton",
  "middle_name": null,
  "suffix": null,
  "endorsements": [
    {
      "logo_url": "https://br-production-assets.s3.amazonaws.com/uploads/organization/logo/2/TurnoutProject.png",
      "id": 2,
      "website_url": null,
      "name": "Turnout Project"
    },
    {
      "logo_url": "https://br-production-assets.s3.amazonaws.com/uploads/organization/logo/3/sierraclub_copy.png",
      "id": 3,
      "website_url": "https://www.sierraclub.org/",
      "name": "Sierra Club"
    },
    {
      "logo_url": "https://br-production-assets.s3.amazonaws.com/uploads/organization/logo/5/USChamberOfCommerce.png",
      "id": 5,
      "website_url": null,
      "name": "US Chamber Of Commerce"
    },
    {
      "logo_url": "https://br-production-assets.s3.amazonaws.com/uploads/organization/logo/8/pp_logo.png",
      "id": 8,
      "website_url": "https://www.plannedparenthoodaction.org/",
      "name": "Planned Parenthood Action Fund"
```



## Data Dictionary <a name="data_dictionary"></a>

## Elections API:

Data Field | Description
------------ | -------------
election_id | unique id representing a specific election
name | the name describing the specific election (i.e. Tennessee 2018 Primary Election)
election_date | the date of the election
state | the state the election takes place in
dates | an indicator for whether the election took place in the past or will take place in the future
candidates | the number of candidates running in the election
positions | the number of positions open candidates can compete in


## Positions API:

Data Field | Description
------------ | -------------
position_id | unique id reprsenting the position for a candidate
name | name of the position
state | state where the position is held
position_level | an indicator for whether the position is at the local, county, state, or federal level
city/county | the city or county the position is held in
next_election_year | the calendar year the next election for this position takes place 
election_id | 
current_office_holder | indicator for whether the related office holder is currently in office
judicial | an indicator representing whether the position is a judicial branch position


## Candidates API:

Data Field | Description
------------ | -------------
candidate_id | unique id representing each candidate
name | the name of the candidate
state | the state the candidate represents
party | the party the candidate belongs to
election_id | unique id representing the election the candidate won
election_day | the day the candidate was elected
position_level | an indicator for whether the candidate is elected at the local, state, or federal level
position | the position the candidate was elected to
current_office_holder | an indicator for whether the candidate is currently in office
website | the website of the candidate
org_endorsement | the organizations that have endorsed the candidate
endorsement_count | the count of endorsements received by the candidate
photo | an indicator for whether the candidate has a photo on file




--------------------------------------------------------------------------------------------------------

