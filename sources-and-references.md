---
description: >-
  Backed by a wide range of satellite & weather data, as well as powerful open
  source code
---

# Sources & References

### Data Sources

Earth Observation satellite and Weather Model data is used to daily produce the underlying global snow dataset that powers both DeFROST Maps and API services. These sources include:

{% tabs %}
{% tab title="Satellite Data" %}
* [Sentinel-2](https://sentinel.esa.int/web/sentinel/missions/sentinel-2), operated by the European Space Agency.
* [VIIRS](https://earthdata.nasa.gov/earth-observation-data/near-real-time/download-nrt-data/viirs-nrt) onboard Suomi-NPP, operated by NASA.
* [MODIS](https://lance-modis.eosdis.nasa.gov/data/modis.php) onboard Terra & Aqua, operated by NASA.
{% endtab %}

{% tab title="Weather Models" %}
* [ICON-EU](https://www.dwd.de/EN/ourservices/nwp_forecast_data/nwp_forecast_data.html), by Deutscher Wetterdienst.
* [HRDPS](https://weather.gc.ca/grib/grib2_HRDPS_HR_e.html), by Government of Canada.
* [GFS](http://en.wikipedia.org/wiki/Global_Forecast_System), by the National Oceanographic and Atmospheric Administration \(USA\).
{% endtab %}

{% tab title="Snow Models" %}
* [SNODAS](https://nsidc.org/data/g02158), by the National Snow and Ice Data Center \(USA\).
{% endtab %}
{% endtabs %}

### Open Source Works

This section highlights some of the Open Source projects that make DeFROST possible and that we actively support. 

{% hint style="info" %}
**Special mention** goes to the [**Let-It-Snow**](https://gitlab.orfeo-toolbox.org/remote_modules/let-it-snow) module by [CESBIO](https://www.cesbio.cnrs.fr/en/homepage/). DeFROST works with its [custom extension](https://github.com/wegaw/s2-lis-snowcover) of this module for the processing of Sentinel-2 scenes to detect snow on them.

Thanks to Gascoin, S., Grizonnet, M., Bouchet, M., Salgues, G., and Hagolle, O. and all LIS contributors.
{% endhint %}

The list is not exhaustive:

* [Rasterio](https://rasterio.readthedocs.io/en/latest/)
* [Shapely](https://shapely.readthedocs.io/en/latest/manual.html)
* [GeoPandas](https://geopandas.org/)
* [GDAL](https://gdal.org/)
* [QGIS](https://www.qgis.org/en/site/)

