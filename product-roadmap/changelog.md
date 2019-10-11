---
description: "Be sure to not miss out on new features and improvements! \U0001F680"
---

# Changelog

## Coming soon

* 🌐 **Global coverage at 375 meters resolution** - for both API and Map services on snow cover, scheduled for 30th October 2019!
* ❄ **Alps coverage for snow depth** real-time data
* ☁ **Improved snow detection in extremely cloudy regions** while keeping the best resolution available! 
* 💻 **Snow over an area** new API endpoint
* 🤩 **Self-service signup page** to request access to DeFROST

## v1.1 - 11 Oct 2019

### New Features

* ⚛ **\[API\] New API Endpoint Snow cover over line**: a new endpoint called[ Snow cover over line](https://defrost.ch/api-docs#operation/Snow%20cover%20over%20line) allows you passing a [GeoJSON formatted LineString geometry](https://en.wikipedia.org/wiki/GeoJSON#Geometries) to retrieve the snow cover status for each of the line's point. In addition, this endpoint will return the percentage of the terrain under such line that is covered under snow - by resampling the line to 20 meters. 

### Improvements

* ☁ **\[Data\]** **Snow cover detection during cloudy periods**: the map will now use the best data available either at 20 or 500 meters resolution to map the snow cover during periods of consistent cloudy conditions over any region. This means that for areas under such conditions, resolution might start dropping down up to 500m while still managing to detect snow. Therefore the perceived "pixel size" on the snow cover map may appear to increase. Read the Coming soon section for our roadmap in reaching higher resolution for regions with persistent, long cloudy periods.

## v1.0 - 25 Sept 2019

**DeFROST 1.0 codename ALPINE20 first release!** This is basically including, with coverage for all the European Alpine region \(as per the area defined by the Alpine Convention\):

* ⚛ **DeFROST API Service**: an endpoint for querying snow cover at any point in the alps. Another endpoint for querying the snow depth for any point.
* 🗺 **DeFROST Map Service**: a TMS standard web map tile server secured by JWT tokens providing DeFROST snow cover map compatible with any major web mapping library such as OpenLayers, Leaflet or Mapbox.

