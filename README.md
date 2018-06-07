# Bike round trip planner
A bike round trip planner using the api of openrouteservice

## Info
This is a simple react-geo based round trip planner for biking tours.
While waypoints can be set individually or calculated with help of turf.js, directions are based on the api of openrouteservice.
The basemap is a custom OpenStreetMap style and is being served via geoserver and mapproxy by default. See below for setting up the custom map style.

## Install
Clone repository to your local drive
```javascript static
npm i
```

## Install map style
1. Download an OSM data extract from http://download.geofabrik.de, e.g. for Nordrhein-Westfahlen:
```javascript static
http://download.geofabrik.de/europe/germany/nordrhein-westfalen-latest.osm.pbf
```
2. Download the bounding box for the specific region
https://overpass-turbo.eu/

3. PostgreSQL: Create Database and activate PostGIS extension.
```javascript static
CREATE DATABASE bike_nrw;
CREATE EXTENSION POSTGIS;
```
4. Import the OSM dataset into the database using [Imposm](https://github.com/omniscale/imposm3)
```javascript static
imposm3 import -config config.json -read nordrhein-westfalen-latest.osm.pbf -write -limitto nrw.geojson
```
5. Geoserver: Install the following extensions:
  - Importer
  - Vector tiles
  - [mbstyle](http://ares.opengeo.org/geoserver/master/community-latest/)
  - Import all database tables (see step 4) using Importer. Important: Activate *application/x-protobuf;type=mapbox-vector* (image format) in the Tile-Cache configuration.
  - Create new style (Format: mystyle) and import the *bikestyle.json* file from /assets
  - Create a new group layer (no need for adding the single layers) and apply the bike style
 6. **Mapproxy:** 
 7. src/mapconfig.js: Comment out line 59 and 60. Comment in line 61 to 62. That's it.






## Start
