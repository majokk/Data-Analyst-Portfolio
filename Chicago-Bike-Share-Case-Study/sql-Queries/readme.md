# Chicago Bikeshare: How to Attract More Regular Members

Divvy is a fictional company running a Bikeshare scheme in the Greater Chicago Area. 
My task is to analyze the data and give suggestions for the Business Development on how to increase the number regular members.

## Data

The dataset I am working with consists Divvy Bikeshare data. For relevance and simplicity, the analysis is limited to data from July 2022 to Aug 2023. 
The dataset containts Trip attributes includes, start-end coordinates, timestamps, rideable type (electric, docked and normal bike), user type (member or casual rider) and station information where applicable. 

To provide more depth and breath to the analysis, I have added the geogrpahic boundaries of Chicago Community Areas to the dataset. Community Areas are neighbourhoods of Chicago for which census data is available. This makes it possible to add spatial, demographic and socio-economic dimensions to the analysis. 

## Data Preparation 

Divvy Trip Data is available in csv format. I downloaded the data, created Google Cloud storage bucket and created a corresponding Dataset in a designated Google BigQuery (BQ) Project. The Community Area data is available on Chicacgo Data Portal. The data is available in many common formats. I dowloaded the data in geojson format. However, BigQuery requires geojson data to be in the newline-delimited format. (This allows each line of the file to read, parsed and processed without readng the whole file into memory). To convert the json file to ndjson I used the jq command-line tool:

`type cm.geojson | jq -c ".features[]" > cm.geojsonl`

Uploading newline delimited geojson via console is not supported in BigQueyr. Google Cloud shell upload script:

```
bq load  --source_format=NEWLINE_DELIMITED_JSON --json_extension=GEOJSON --autodetect \
 divvy_trip_data.comm_areas_geo \
gs://com_area_geo/cm_nl.geojsonl \
```




## List of sql-queries with description
### Setup, Data Exploration,
### Data Cleaning
### Analysis
