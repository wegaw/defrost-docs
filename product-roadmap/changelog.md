---
description: "Be sure to not miss out on new features and improvements! \U0001F680"
---

# Changelog

## Coming soon

* 🗺 **Smooth snow-covered area edges** in the maps ****for a neat look & feel 
* ❄ **Global coverage for snow depth** real-time data
* 💻 **Snow over an area** new API endpoint

## v1.2.3 - 22 Nov 2019

### Improvements

* 🗺**\[Map\] Tiles load 41% faster:** we have deployed a few fixes in orur servers to be able to manage more map tile requests in parallel, so that we can serve maps 41% faster, in average, than before.
* ⚛ **\[API\] Snow depth resolution improved**: for the Swiss Alps, you now get snow depth estimations that are closer to the real world's depth thanks to improved resolution in our models.

## v1.2.2 - 15 Nov 2019

### New Features

* 🗺**\[Map\] Google Maps support:** you can now integrate the DeFROST Maps directly with Google Maps JavaScript API V3! Check [the documentation](../introduction/development-quickstart.md#google-maps-users-whitelist-your-http-referrers) and [code examples](https://github.com/wegaw/defrost-examples/blob/master/tests/map_tests/google-map.html) to get started.

## v1.2.1 - 11 Nov 2019

### New Features

* 🌐 **\[General\] Public demo page available:** you can now navigate the latest global snow cover map on our [new demo page](https://defrost.io/demo) and leave your feedback! 

### Improvements

* 🗺 **\[Map\] Improved snow detection in extremely cloudy regions** while keeping the best resolution available for the [European Alps Map](../defrost-maps/european-alps-map.md). This improvement will soon be deployed for the global map.

### Bugfix

* ⚛ **\[API\] Snow depth endpoint fixed**: After the global map inclusion in version 1.2, the snow depth endpoint started malfunctioning and reporting 0cm anywhere. This bug has been fixed in version 1.2.1. Thanks to our pilot users for reporting.

## v1.2 - 1 Nov 2019

### New Features

* 🗺 **\[Map\]** [**DeFROST Global Snow Cover Map**](../defrost-maps/global-map.md) **at 375 meters resolution:** [new Map endpoint](../defrost-maps/global-map.md#map-endpoint) offering a fresh daily map on snow coverage between the 70°N and 70°S parallels. 
* ⚛ **\[API\] DeFROST Global Snow Cover at 375 meters resolution:** now allows for Snow cover at point and over-line queries anywhere between the 70°N and 70°S parallels. 

### Changes

* ‼ 🌐 **\[General\] DeFROST domain migrates from .ch to .io** _****_: DeFROST is now served, in addition to the previous .ch domain, [under a new .io domain](https://defrost.io). This includes both the website, documentation, API and Maps. The next major version, 2.0 scheduled for first half 2020, will deprecate and discontinue the .ch domain. 

### Improvements

* 📘 **\[Documentation\]** **New DeFROST Maps section**: this section presents and describes the characteristics of both maps operated by DeFROST, this is, the European Alps Map and the Global Map. In addition, it will help you out in setting up your snow cover map! Read more at [Maps Overview](../defrost-maps/maps-overview.md).

## v1.1.1 - 16 Oct 2019

### New Features

* ⚛ **\[API\] The "Snow cover over a line" endpoint returns 2 new metrics**: the minimum and maximum snow depth observed across the points that compose the line you are querying snow for are now returned by the [Snow cover over line](https://defrost.io/api-docs#operation/Snow%20cover%20over%20line) API endpoint.

## v1.1 - 11 Oct 2019

### New Features

* ⚛ **\[API\] New API Endpoint Snow cover over line**: a new endpoint called[ Snow cover over line](https://defrost.io/api-docs#operation/Snow%20cover%20over%20line) allows you passing a [GeoJSON formatted LineString geometry](https://en.wikipedia.org/wiki/GeoJSON#Geometries) to retrieve the snow cover status for each of the line's point. In addition, this endpoint will return the percentage of the terrain under such line that is covered under snow - by resampling the line to 20 meters. 

### Changes

* ⚛ **\[API\] Snow depth is now returned as part of Snow cover at point and over-line endpoints**. A single, interpolated value is returned for each point. For now, we are able to provide snow depth values for locations in the Swiss Alps. 
* ‼ ⚛ **\[API\] Snow depth endpoint deprecated**: The _Snow depth at point_ endpoint is deprecated and will be removed in the next minor version 1.2. The snow depth metric is now returned at the _Snow cover at point_ and _Snow cover over line_ endpoints, please switch to using those instead. 

### Improvements

* ☁ **\[Data\]** **Snow cover detection during cloudy periods**: the map will now use the best data available either at 20 or 500 meters resolution to map the snow cover during periods of consistent cloudy conditions over any region. This means that for areas under such conditions, resolution might start dropping down up to 500m while still managing to detect snow. Therefore the perceived "pixel size" on the snow cover map may appear to increase. [Improved in version 1.2.1](changelog.md#v-1-2-1-11-nov-2019).

## v1.0 - 25 Sept 2019

**DeFROST 1.0 codename ALPINE20 first release!** This is basically including, with coverage for all the European Alpine region \(as per the area defined by the Alpine Convention\):

* ⚛ **DeFROST API**: an endpoint for querying snow cover at any point in the alps. Another endpoint for querying the snow depth for any point.
* 🗺 **DeFROST Maps**: a TMS standard web map tile server secured by JWT tokens providing DeFROST snow cover map compatible with any major web mapping library such as OpenLayers, Leaflet or Mapbox.

