# CivicEngine API Documentation

**API Key:** APIKEY
**API Host:** api.civicengine.com


## Table of contents
1. [Elections API](#elections_api)
2. [Positions API](#positions_api)
3. [Candidates API](#candidates_api)
4. [Normalized Positions API](#norm_positions_api)
5. [Data Dictionary](#data_dictionary)


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

## Normalized Positions API <a name="norm_positions_api"></a>
**Parameters:**

      address - primary search criteria
      lat/lon (optional) - instead of using address, pass lat/lon and bypass geocoding
      include_candidates - choose to include candidates in API response or not
      election_id - if you include candidates, you can filter by a specific election_id (see below)
      level - (federal/state/local/county) - return only positions at a single level
      search_radius - return positions within X miles of address (up to 30)

**Request Syntax:**
curl -H "x-api-key: APIKEY" "https://api.civicengine.com/normalized-positions"

**Return Type:**

JSON dictionary
      
**Returns:**
``` [{"mtfcc": null, "id": 2090, "name": "Township Constable"}, {"mtfcc": null, "id": 2000, "name": "Party Officer - City"}, {"mtfcc": null, "id": 2040, "name": "Township Executive"}, {"mtfcc": null, "id": 1630, "name": "City Taxpayer Advocate"}, {"mtfcc": null, "id": 2380, "name": "Local Higher Education Board"}, {"mtfcc": null, "id": 2060, "name": "Township Legislative"}, {"mtfcc": null, "id": 1780, "name": "City Court Clerk"}, {"mtfcc": null, "id": 4030, "name": "Judicial Circuit Court (1)"}, {"mtfcc": null, "id": 1820, "name": "Fire Committee"}, {"mtfcc": null, "id": 2460, "name": "Regional Planning District"}, {"mtfcc": null, "id": 1600, "name": "City Collector"}, {"mtfcc": null, "id": 2550, "name": "Mosquito Abatement District"}, {"mtfcc": null, "id": 2320, "name": "Combination - Fire And Healthcare District"}, {"mtfcc": null, "id": 925, "name": "County Trustee"}, {"mtfcc": null, "id": 1290, "name": "County Superintendent Of Schools"}, {"mtfcc": null, "id": 1330, "name": "County Road Commissioner"}, {"mtfcc": null, "id": 2030, "name": "Township Collector"}, {"mtfcc": null, "id": 1580, "name": "City Auditor"}, {"mtfcc": null, "id": 2430, "name": "Forest District"}, {"mtfcc": null, "id": 980, "name": "County Sheriff"}, {"mtfcc": null, "id": 1790, "name": "City Highway Supervisor"}, {"mtfcc": null, "id": 710, "name": "District Attorney"}, {"mtfcc": null, "id": 2120, "name": "Township Auditor"}, {"mtfcc": null, "id": 1000, "name": "County Treasurer / Finance Officer"}, {"mtfcc": null, "id": 2110, "name": "Township Director Of Law"}, {"mtfcc": null, "id": 1320, "name": "County Emergency/911/Central Dispatch Board"}, {"mtfcc": null, "id": 2050, "name": "Township Highway Superintendent"}, {"mtfcc": null, "id": 2360, "name": "Water District"}, {"mtfcc": null, "id": 1810, "name": "Town Sergeant"}, {"mtfcc": null, "id": 2630, "name": "Irrigation District"}, {"mtfcc": null, "id": 1080, "name": "County Controller"}, {"mtfcc": null, "id": 1610, "name": "City Police Chief / Marshal"}, {"mtfcc": null, "id": 2500, "name": "Combination - Water And Sewer District"}, {"mtfcc": null, "id": 2070, "name": "Township Treasurer (Fiscal Officer)"}, {"mtfcc": null, "id": 1280, "name": "Racing Commissioner"}, {"mtfcc": null, "id": 2020, "name": "Township Clerk"}, {"mtfcc": null, "id": 1565, "name": "City Clerk/Treasurer"}, {"mtfcc": null, "id": 1670, "name": "City Budget Committee"}, {"mtfcc": null, "id": 2560, "name": "Local Conservation District"}, {"mtfcc": null, "id": 1110, "name": "County Director Of Community Development"}, {"mtfcc": null, "id": 720, "name": "Metro Council President"}, {"mtfcc": null, "id": 2300, "name": "Airport District"}, {"mtfcc": null, "id": 2600, "name": "Nursing Home / Convalescent Center District"}, {"mtfcc": null, "id": 1180, "name": "County Educational Service / Learning Community"}, {"mtfcc": null, "id": 790, "name": "Regional Conservation / Natural Resources Board"}, {"mtfcc": null, "id": 2390, "name": "Local Unified School Board"}, {"mtfcc": null, "id": 2580, "name": "Local Ambulance / Emergency Services District"}, {"mtfcc": null, "id": 4480, "name": "Judicial Local Court (1)"}, {"mtfcc": null, "id": 2310, "name": "Landscaping District"}, {"mtfcc": null, "id": 1720, "name": "Trustee Of The Trust Fund"}, {"mtfcc": null, "id": 1200, "name": "County/Multi-County Water District"}, {"mtfcc": null, "id": 2590, "name": "Local Road District"}, {"mtfcc": null, "id": 4040, "name": "Judicial Circuit Court (2)"}, {"mtfcc": null, "id": 1300, "name": "County Community Council / Advisory"}, {"mtfcc": null, "id": 2130, "name": "Township Parks Commissioner"}, {"mtfcc": null, "id": 2350, "name": "Healthcare / Hospital District"}, {"mtfcc": null, "id": 1635, "name": "City Attorney"}, {"mtfcc": null, "id": 1910, "name": "Board Of Public Affairs"}, {"mtfcc": null, "id": 2650, "name": "Community Development District"}, {"mtfcc": null, "id": 2410, "name": "Local Elementary School Board"}, {"mtfcc": null, "id": 2610, "name": "Flood Control District"}, {"mtfcc": null, "id": 2005, "name": "Township Trustee Leader"}, {"mtfcc": null, "id": 920, "name": "County Assessor"}, {"mtfcc": null, "id": 970, "name": "County Clerk Treasurer"}, {"mtfcc": null, "id": 1510, "name": "City Legislative Chair"}, {"mtfcc": null, "id": 4060, "name": "Judicial Subcircuit Court"}, {"mtfcc": null, "id": 740, "name": "Metro Council Member"}, {"mtfcc": null, "id": 1570, "name": "City Treasurer (Finance Officer)"}, {"mtfcc": null, "id": 990, "name": "County Surveyor"}, {"mtfcc": null, "id": 1890, "name": "City Charter Commissioner"}, {"mtfcc": null, "id": 1860, "name": "Town Grand Juror"}, {"mtfcc": null, "id": 730, "name": "Metro Council Auditor"}, {"mtfcc": null, "id": 1100, "name": "County Director Of Elections"}, {"mtfcc": null, "id": 2640, "name": "Memorial District"}, {"mtfcc": null, "id": 1050, "name": "County Marriage Official"}, {"mtfcc": null, "id": 2510, "name": "Cemetery District"}, {"mtfcc": null, "id": 1010, "name": "County Recorder / Register Of Deeds / Register Of Mesne Conveyance"}, {"mtfcc": null, "id": 2370, "name": "Library District"}, {"mtfcc": null, "id": 4490, "name": "Judicial Local Court (2)"}, {"mtfcc": null, "id": 960, "name": "County Clerk Of Court"}, {"mtfcc": null, "id": 1160, "name": "County Public Defender"}, {"mtfcc": null, "id": 2490, "name": "Tv District"}, {"mtfcc": null, "id": 1800, "name": "City Public Works Commissioner"}, {"mtfcc": null, "id": 4050, "name": "Judical Special Circuit Court"}, {"mtfcc": null, "id": 1120, "name": "County Register Of Wills"}, {"mtfcc": null, "id": 1850, "name": "Town Meeting Member"}, {"mtfcc": null, "id": 2340, "name": "Harbor District"}, {"mtfcc": null, "id": 1250, "name": "Flood Control Board"}, {"mtfcc": null, "id": 1560, "name": "City Clerk/Collector"}, {"mtfcc": null, "id": 1620, "name": "City Constable"}, {"mtfcc": null, "id": 2620, "name": "Museum District"}, {"mtfcc": null, "id": 2010, "name": "Township Trustee"}, {"mtfcc": null, "id": 1020, "name": "County Coroner"}, {"mtfcc": null, "id": 1030, "name": "County Court Constable"}, {"mtfcc": null, "id": 1710, "name": "Supervisor Of The Checklist"}, {"mtfcc": null, "id": 800, "name": "County Attorney"}, {"mtfcc": null, "id": 1350, "name": "County Board Of Education"}, {"mtfcc": null, "id": 1760, "name": "Fence Viewer"}, {"mtfcc": null, "id": 1040, "name": "County Engineer"}, {"mtfcc": null, "id": 1220, "name": "County/Multi-County (Soil) Conservation District"}, {"mtfcc": null, "id": 2330, "name": "Fire District"}, {"mtfcc": null, "id": 1260, "name": "County (Tax) Collector"}, {"mtfcc": null, "id": 1550, "name": "City Clerk (Ward Officer In Some Jurisdictions)"}, {"mtfcc": null, "id": 1240, "name": "County Budget/Finance Committee"}, {"mtfcc": null, "id": 1660, "name": "City Registrar Of Voters"}, {"mtfcc": null, "id": 1770, "name": "City Register Of Wills"}, {"mtfcc": null, "id": 1310, "name": "County Health Department Director"}, {"mtfcc": null, "id": 1830, "name": "Water Commissioner"}, {"mtfcc": null, "id": 1140, "name": "County Jailer"}, {"mtfcc": null, "id": 2480, "name": "Public Transportation District"}, {"mtfcc": null, "id": 2570, "name": "Soil And Water District"}, {"mtfcc": null, "id": 2420, "name": "Local Superintendent Of Schools"}, {"mtfcc": null, "id": 1500, "name": "City Executive (Mayor)"}, {"mtfcc": null, "id": 4470, "name": "Judicial County Court"}, {"mtfcc": null, "id": 2450, "name": "Public Utilities District"}, {"mtfcc": null, "id": 1540, "name": "City Comptroller"}, {"mtfcc": null, "id": 2080, "name": "Township Assessor"}, {"mtfcc": null, "id": 900, "name": "County Executive"}, {"mtfcc": null, "id": 1130, "name": "County Commissioner Of Revenue"}, {"mtfcc": null, "id": 940, "name": "County Clerk"}, {"mtfcc": null, "id": 4610, "name": "Precinct Inspector / Ward Election Inspector"}, {"mtfcc": null, "id": 1190, "name": "County/Multi-County Reclamation District"}, {"mtfcc": null, "id": 1270, "name": "License Commissioner / Director"}, {"mtfcc": null, "id": 1840, "name": "Director Of Public Welfare"}, {"mtfcc": null, "id": 1870, "name": "Town Advisory Board"}, {"mtfcc": null, "id": 910, "name": "County Legislative"}, {"mtfcc": null, "id": 1590, "name": "City Assessor / Lister"}, {"mtfcc": null, "id": 1740, "name": "Ethics Board"}, {"mtfcc": "G4000", "id": 700, "name": "Party Office - State Congressional District"}, {"mtfcc": "G4000", "id": 250, "name": "State Controller"}, {"mtfcc": "G4000", "id": 380, "name": "State Utilities Board"}, {"mtfcc": "G4000", "id": 210, "name": "Agriculture And Industries Commissioner"}, {"mtfcc": "G4000", "id": 4010, "name": "Judicial Appellate Court"}, {"mtfcc": "G4000", "id": 260, "name": "Tax Commissioner"}, {"mtfcc": "G4000", "id": 110, "name": "Lt. Governor"}, {"mtfcc": "G4000", "id": 200, "name": "State Mine Inspector"}, {"mtfcc": "G4000", "id": 430, "name": "State Board Of Governors"}, {"mtfcc": "G4000", "id": 160, "name": "State Comptroller"}, {"mtfcc": "G4000", "id": 400, "name": "State Native Affairs Board"}, {"mtfcc": "G4000", "id": 120, "name": "Lieutenant Governor And Secretary Of State"}, {"mtfcc": "G4000", "id": 230, "name": "Commissioner Of School And Public Lands"}, {"mtfcc": "G4000", "id": 180, "name": "State Treasurer"}, {"mtfcc": "G4000", "id": 190, "name": "State Superintendent Of Schools"}, {"mtfcc": "G4000", "id": 470, "name": "State Public Services Board / Public Regulation / Corporation Commissioner (Ok)"}, {"mtfcc": "G4000", "id": 4020, "name": "Judicial Special Appellate Court"}, {"mtfcc": "G4000", "id": 140, "name": "State Attorney General"}, {"mtfcc": "G4000", "id": 706, "name": "Party Office - State House District"}, {"mtfcc": "G4000", "id": 390, "name": "State K12 Education Board"}, {"mtfcc": "G4000", "id": 410, "name": "State Higher Education Board"}, {"mtfcc": "G4000", "id": 3990, "name": "Judicial Supreme Court - Chief Justice"}, {"mtfcc": "G4000", "id": 130, "name": "Secretary Of State"}, {"mtfcc": "G4000", "id": 280, "name": "State Labor Commissioner"}, {"mtfcc": "G4000", "id": 360, "name": "State Natural Resource Board"}, {"mtfcc": "G4000", "id": 150, "name": "State Agriculture Secretary"}, {"mtfcc": "G4000", "id": 170, "name": "State Auditor"}, {"mtfcc": "G4000", "id": 100, "name": "Governor"}, {"mtfcc": "G4000", "id": 370, "name": "State Labor Board"}, {"mtfcc": "G4000", "id": 240, "name": "Commissioner Of Securities And Insurance"}, {"mtfcc": null, "id": 1, "name": "US President"}, {"mtfcc": "G4000", "id": 2, "name": "US Senate"}, {"mtfcc": "G5200", "id": 3, "name": "US House Of Representatives"}, {"mtfcc": null, "id": 1880, "name": "City Parks And Recreation Commissioner"}, {"mtfcc": null, "id": 2100, "name": "Township Clerk/Treasurer"}, {"mtfcc": null, "id": 2400, "name": "Local High School Board"}, {"mtfcc": null, "id": 1900, "name": "Building Director"}, {"mtfcc": null, "id": 4620, "name": "Party Office - Precinct"}, {"mtfcc": null, "id": 1340, "name": "County Agricultural Extension Council"}, {"mtfcc": null, "id": 1505, "name": "City Manager"}, {"mtfcc": "G4000", "id": 4, "name": "State Legislative Upper House"}, {"mtfcc": "G4000", "id": 5, "name": "State Legislative Lower House"}, {"mtfcc": "G4000", "id": 6, "name": "State Governor"}, {"mtfcc": "G4000", "id": 7, "name": "State Attorney General"}, {"mtfcc": "G4000", "id": 8, "name": "State Lieutanant Governor"}, {"mtfcc": "G4000", "id": 4000, "name": "Judicial Supreme Court"}, {"mtfcc": "G4000", "id": 220, "name": "Commissioner Of Public Lands"}, {"mtfcc": "G4000", "id": 490, "name": "State Board Of Equalization"}, {"mtfcc": null, "id": 1750, "name": "Surveyor Of Wood And Timber"}, {"mtfcc": null, "id": 1690, "name": "Town Moderator"}, {"mtfcc": null, "id": 4600, "name": "Precinct Election Judge"}, {"mtfcc": null, "id": 1530, "name": "City Supervisor"}, {"mtfcc": null, "id": 2520, "name": "General Services District"}, {"mtfcc": null, "id": 1210, "name": "County/Multi-County Parks And Recreation District"}, {"mtfcc": null, "id": 780, "name": "Regional Utility District"}, {"mtfcc": null, "id": 1060, "name": "County Probate Administrator / Register Of Probate / Public Administrator (Nv)"}, {"mtfcc": null, "id": 1170, "name": "County Weed Control"}, {"mtfcc": null, "id": 2440, "name": "Parks And Recreation District"}, {"mtfcc": null, "id": 1230, "name": "County (High) Bailiff"}, {"mtfcc": null, "id": 2530, "name": "Improvement District"}, {"mtfcc": null, "id": 1150, "name": "County Elections Board Member"}, {"mtfcc": null, "id": 1730, "name": "Zoning Board"}, {"mtfcc": null, "id": 760, "name": "Council Of Governments"}, {"mtfcc": null, "id": 1090, "name": "County Hwy Commissioner"}, {"mtfcc": null, "id": 1640, "name": "City Rent Board"}, {"mtfcc": null, "id": 2540, "name": "Sanitary District"}, {"mtfcc": null, "id": 4500, "name": "Judicial Special Local Court"}, {"mtfcc": null, "id": 1700, "name": "City Planning Board"}, {"mtfcc": null, "id": 750, "name": "Regional Education District"}, {"mtfcc": null, "id": 1070, "name": "County Property Assessment Review Board"}, {"mtfcc": null, "id": 1650, "name": "City Neighborhood Board"}, {"mtfcc": null, "id": 930, "name": "County Auditor"}, {"mtfcc": null, "id": 2470, "name": "Swimming Pool District"}, {"mtfcc": null, "id": 4475, "name": "Judicial Special County Court"}, {"mtfcc": null, "id": 950, "name": "County Clerk And Recorder"}, {"mtfcc": null, "id": 1520, "name": "City Legislative"}, {"mtfcc": "G4000", "id": 270, "name": "State Insurance And Fire Safety Commissioner"}, {"mtfcc": "G4000", "id": 440, "name": "State Railroad Commissioner"}, {"mtfcc": "G4000", "id": 420, "name": "State Transportation Board"}, {"mtfcc": "G4000", "id": 705, "name": "Party Office - State Senate District"}, {"mtfcc": "G4000", "id": 770, "name": "Regional Board Of Transportation"}, {"mtfcc": "G4000", "id": 350, "name": "State Insurance Board"}] ```



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

