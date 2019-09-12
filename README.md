---
description: Get a glimpse of how to integrate DeFROST in your website or mobile app.
---

# DeFROST Overview

You can integrate snow cover data from DeFROST in two main ways:

### DeFROST Map Service

The Map Service allows you to **display the snow cover as a map** and integrates quickly with the most popular mobile & web mapping frameworks. This service implements the **Tiled Map Service** standard and allows you to customize the look and feel of the tiles on the fly. 

![DeFROST Snow Cover layer displayed over a Mapbox base map](.gitbook/assets/assets_-lilbxlqv870ib7hjojr_-lmcelxri_gymglf3kfj_-lmch3eqlzcj1yxhvftm_image.png)

You can read through our [quickstart](introduction/development-quickstart.md) to get started with _**Leaflet**, **Mapbox**, **and OpenLayers**._

### DeFROST API

Do you want to power a custom, more advanced use case? [DeFROST API](https://defrost.ch/api-docs) lets you **query snow cover for a point, along a path or over an area programmatically**. Check below for a quick example on a query to find out whether or not there is snow at the top of the Matterhorn:

{% api-method method="get" host="https://api.defrost.ch" path="/v1/snow-point/{lat}/{lng}" %}
{% api-method-summary %}
snow-point
{% endapi-method-summary %}

{% api-method-description %}
Obtain the latest snow status data for a specific coordinate expressed in latitude and longitude degrees.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="lat" type="number" required=true %}
Latitude measured in degrees
{% endapi-method-parameter %}

{% api-method-parameter name="lng" type="number" required=true %}
Longitude measured in degrees
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
In this example, DeFROST returns a snow-positive reply for the Matterhorn summit last sensed by a satellite on 19th August 2019 at 12:15 UTC.
{% endapi-method-response-example-description %}

```javascript
{
    "lat": 45.9766,
    "lng": 7.6585, 
    "snow": true,
    "date": "2019-08-19T12:15:00Z",
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

The DeFROST API is a **RESTful API compliant with the OpenAPI 2.0** standard, so it can be integrated easily in your application.  As such you can use it in any environment connected to the world wide web using a TCP/IP library of your choice.  The **response data format is in the JSON format**, which is widely supported by all major programming languages and frameworks. That means you can integrate the API in most platforms including all major _**web browsers**, **Android**, **iOS**, **Python, C/C++, Node.js**_. You name it. 

{% hint style="info" %}
To get started in minutes with either the Map Service or the API, read the [Development Quickstart](introduction/development-quickstart.md).
{% endhint %}

