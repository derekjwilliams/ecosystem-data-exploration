# Code Libraries

## R 

https://github.com/usgs/nabatr/blob/master/R/nabat_gql_queries.R

## JavaScript

GRTS data and D3 snippets for extremely fast visualization 

https://github.com/derekjwilliams/GRTS2GeoJSON

# Resources

NABat home

https://www.nabatmonitoring.org

NABat Director

https://www.usgs.gov/staff-profiles/brian-reichert?qt-staff_profile_science_products=0#

## NABat data exploration 

### Web UI 

https://sciencebase.usgs.gov/nabat/#/data/inventory

Caution, very slow and high memory footprint

Page for account request - login is currently off line


## APIs

Nabat Graphiql (created and originally written by Derek Williams, using PostGraphile for the heavy lifting)

Note, the API has been changed to be very non-cononical (in a data and graphql) since it's original creation.  For example the visualization example query below includes information about visualization, e.g. chart, which should not be in the data API.  As a consequence of other chages the API is also now very slow.

So don't use the API heavily!

It is possible that a separate project may be started by Derek Williams to provide a more useful, efficient, and faster API.  See NaBatSchema.json for the full schema.

https://api.sciencebase.gov/nabat-graphql/graphiql

Nabat Graphql endpoint

https://api.sciencebase.gov/nabat-graphql/graphql

https://sciencebase.usgs.gov/nabat/#/data/inventory

Example queries

```
query {
  allSpecies(first: 100) {
    nodes {
      speciesCode
      
    }
  }
}
```

```
query {
  allVwPublicSelectedForSurveys(first: 100) {
    nodes {
      grtsCellId
      geom4326 {
        geojson
      }
    }
  }
}
```

```
query {
  allCqlKeys(first: 100) {
    nodes {
      cqlGrtsKeysByKey (first: 10) {
        nodes {
          grtsId
        }
      }
    }
  }
}
```

```query {
  allMvwPublicMonthlyRecordCounts (first: 10, filter : {organizationId: {equalTo:3}}) {
    nodes {
      organizationId
      surveyTypeId
      dateMo
      eventCt
      valueCt
    }
  }
}
```

```{
  query {
    fnPublicSearchFeatureText (first: 10) {
      totalCount
      nodes {
        grtsCount
        searchText
        type
        id
        name
        description
      }
    }
  }
}
```

```{
  query {
    fnPublicGetSurveyExtent(first: 1000) {
      totalCount
      nodes {
        stationaryCount
        mobileCount
      }
    }
  }
}```

```{
  query {
    fnPublicGetProjectByGrtsId (_grtsids : 34343) {
      nodes {
        sampleFrameId
        
      }
    }
  }
}
```




Visualization example query:

```
query publicVisualizationSpecies($surveyType: Int!, $grtsOnly: Boolean!, $projectIds: [Int]!, $years: [Int]!, $months: [Int]!, $speciesIds: [Int]!, $genericSpecies: Boolean, $organizationIds: [Int]!, $cqlFilterKey: String) {
    publicVisualizationSpecies(surveyType: $surveyType, grtsOnly: $grtsOnly, projectIds: $projectIds, years: $years, months: $months, speciesIds: $speciesIds, genericSpecies: $genericSpecies, organizationIds: $organizationIds, cqlFilterKey: $cqlFilterKey) {
        location {
            eventGeometryId
            grtsId
            eventCount
            detectionCount
            locationName
            geometry
            __typename}
            chart {
                speciesId
                year
                count
                __typename
            }
            __typename
        }
    }
queryVariables
    {
    "surveyType": 70,
    "chartType": "species",
    "projectIds": [],
    "years": [
        2021,
        2020,
        2019,
        2018,
        2017,
        2016,
        2015,
        2014,
        2013,
        2012,
        2011,
        2010,
        2009,
        2008,
        2007,
        2006,
        2005,
        2004,
        2003,
        2002,
        2001,
        2000,
        1999,
        1998,
        1997,
        1996,
        1995,
        1994,
        1993,
        1992,
        1991,
        1990,
        1989,
        1988,
        1987,
        1986,
        1985,
        1984,
        1983,
        1982,
        1981,
        1980,
        1979,
        1978,
        1977,
        1976,
        1975,
        1974,
        1973,
        1972,
        1971,
        1970,
        1969,
        1968,
        1967,
        1966,
        1965,
        1964,
        1963,
        1962,
        1961,
        1960,
        1959,
        1958,
        1957,
        1956,
        1955,
        1954,
        1953,
        1952,
        1951,
        1950
    ],
    "months": [
        0,
        1,
        2,
        3,
        4,
        5,
        6,
        7,
        8,
        9,
        10,
        11
    ],
    "organizationIds": [],
    "speciesIds": [
        5
    ],
    "grtsOnly": true,
    "covarTypeId": 0,
    "cqlFilterKey": null
    }
```

