---
description: >-
  Get up and running with our Snow Cover API & Maps and kick-start your DeFROST
  integration.
---

# Development Quickstart

Integrating DeFROST in your apps can begin right after you create a DeFROST account, and in just three simple steps:

1. Obtain your API tokens
2. Make a test API Request
3. Display the snow cover map layer

{% hint style="info" %}
All the source code snippets used in this guide are available in the [DeFROST Code Examples GitHub repository](https://github.com/wegaw/defrost-examples), which allows you to **kick-start a working project with just two commands**.
{% endhint %}

Read below for a step by step guide:

### Step 1: Obtain your API tokens

To use DeFROST, you'll need an access token. We use this token to associate any of your requests to your account. Find your token or refresh it in your [Account Dashboard](https://dashboard.staging.defrost.io/) page or obtain it programmatically using the [Create Token API endpoint](https://staging.defrost.io/api-docs#operation/Create%20token).

You will obtain two tokens:

* An Access Token, allowing you to make any API or Maps request
* A Refresh Token, allowing you to obtain a new Access Token when this expires

{% hint style="info" %}
To increase the security of your account, Access tokens **automatically expire** after 7 days, while Refresh tokens expire after 10 days. 
{% endhint %}

Due to automated expiration of both tokens, you need to implement your integration taking this aspect into account. An expired Access Token will return an HTTP response code `401 Unauthorized`, a signal for you to use the [Refresh Token API endpoint](https://staging.defrost.io/api-docs#operation/Refresh%20token) to obtain a newly valid Access Token. If the Refresh Token is expired, obtain a new pair of tokens via the [Create Token API endpoint](https://staging.defrost.io/api-docs#operation/Create%20token). 

The tokens are standard [JSON Web Tokens](https://jwt.io/). Their payload contain the expiration date, which allows you to easily test whether a token is expired or not:

{% code title="check-refresh-token-expired.js" %}
```javascript
var access_or_refresh_token = '<YOUR_ACCESS_OR_REFRESH_TOKEN>';
return JWTDecode(access_or_refresh_token).exp < Date.now() / 1000;
```
{% endcode %}

### Step 2: Make a test API Request

To test that you are ready to start integrating with DeFROST API, make a test API request using your secret API Access and Refresh tokens to refresh the Access token or retrieve the available snow covers.

{% hint style="warning" %}
Make sure to modify the snippets with your API tokens obtained in the step above
{% endhint %}

{% tabs %}
{% tab title="curl" %}
{% code title="defrost\_test.sh" %}
```bash
# URLs used in this example
export API_URL="https://api.staging.defrost.io/v1/snow-covers/"
export REFRESH_URL="https://api.staging.defrost.io/v1/token/refresh/"
# Your DeFROST API tokens
export JWT_ACCESS_TOKEN="<YOUR_ACCESS_TOKEN>"
export JWT_REFRESH_TOKEN="<YOUR_REFRESH_TOKEN>"

# This is how you would refresh your access token
JWT_ACCESS_TOKEN=`curl -X POST -F "refresh=$JWT_REFRESH_TOKEN" "$REFRESH_URL" | sed -E "s/\{\"access\":\"(.+?)\"\}/\1/gI"`
echo "Your new access token is $JWT_ACCESS_TOKEN"
# Let's make an API call using the new token
DATA=`curl --header "Authorization: Bearer $JWT_ACCESS_TOKEN" "$API_URL"`
echo "DATA RECEIVED: $DATA"
```
{% endcode %}
{% endtab %}

{% tab title="Python" %}
{% code title="defrost\_test.py" %}
```python
import requests

# URLs used in this example
SAMPLE_API_URL = 'https://api.staging.defrost.io/v1/snow-covers/'
TOKEN_REFRESH_URL = 'https://api.staging.defrost.io/v1/token/refresh/'
# Your DeFROST API tokens
JWT_ACCESS_TOKEN = '<YOUR_ACCESS_TOKEN>'
JWT_REFRESH_TOKEN = '<YOUR_REFRESH_TOKEN>'

session = requests.Session()
# This is how you would refresh your access token
r = session.post(TOKEN_REFRESH_URL, data = {'refresh': JWT_REFRESH_TOKEN}, timeout=300)
if r.status_code == 200:
    JWT_ACCESS_TOKEN = r.json()['access']
    print('Your new access token is ', JWT_ACCESS_TOKEN)

# Let's make an API call using the new token
headers = {'Authorization': 'Bearer ' + JWT_ACCESS_TOKEN}
r = session.get(SAMPLE_API_URL, headers=headers, timeout=300)
if r.status_code == 200:
    data = r.json()
    print('Data retrieved', data)
```
{% endcode %}
{% endtab %}

{% tab title="JavaScript" %}
{% code title="defrost\_test.js" %}
```javascript
// In this example we will use the axios package to make API requests
// Make sure you import axios. In this example we do it with bundles.
// You could also get axios by including the following in your HTML head
// <script src="https://unpkg.com/axios/dist/axios.min.js"></script>
// Or in Node: const axios = require('axios');
import axios from 'axios';

// URLs used in this example
let SAMPLE_API_URL = 'https://api.staging.defrost.io/v1/snow-covers/';
let TOKEN_REFRESH_URL = process.env.TOKEN_REFRESH_URL;
// Your DeFROST API tokens
let JWT_ACCESS_TOKEN = '<YOUR_ACCESS_TOKEN>';
let JWT_REFRESH_TOKEN = '<YOUR_REFRESH_TOKEN>';

(async() => {
    // if necessary, this is how you would refresh your access token
    let response = await axios.post(TOKEN_REFRESH_URL, {
        refresh: JWT_REFRESH_TOKEN;
    })

    if(response.status == 200) {
        console.info('Your new access token is ', response.data['access']);
        JWT_ACCESS_TOKEN = response.data['access']; 
    }

    // make sure you always include your access token in every request
    axios.interceptors.request.use( config => {
        config.headers.Authorization = 'Bearer ' + JWT_ACCESS_TOKEN;
        return config;
    }, error => {
        return Promise.reject(error);
    })

    // now you are ready to make an API call
    response = await axios.get(SAMPLE_API_URL);
    if( response.status == 200) {
        console.info(response.statusText,'(',response.status,') ',response.data);
    }
    return response.status;
})();
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Step 3: Display the snow cover map layer

{% hint style="info" %}
The code examples here are using the DeFROST [European Alps Map](../defrost-maps/european-alps-map.md). Check the [Global Map section](../defrost-maps/global-map.md) if you are looking for coverage beyond this region.
{% endhint %}

To test that your integration with DeFROST Maps is working correctly, use the examples below for your web mapping library of choice. We provide examples for the most popular web mapping libraries: [OpenLayers](http://openlayers.org), [Leaflet](https://leafletjs.com/), [Mapbox](https://www.mapbox.com/) and [Google Maps](https://developers.google.com/maps/documentation/javascript/tutorial).

#### Google Maps users: whitelist your HTTP referrers

Using the DeFROST API, you can [**add as many HTTP referrers as you want to your whitelist**](https://defrost.io/api-docs#tag/Domain-whitelist) - exclusively allowing requests from such referrers to use your tokens and DeFROST services. This is an added security layer that, while recommended for all cases, it is only **mandatory for Google Maps users**. Since this library does not support sending your token in each tile request's authorization header, you need to send it via a query parameter - making your token exposed.

{% hint style="warning" %}
Make sure to modify the snippets below with your API access token. The Mapbox snippet requires, in addition, your Mapbox token, and the Google Maps one, your Google Maps API Key.
{% endhint %}

{% tabs %}
{% tab title="OpenLayers" %}
{% code title="defrost-ol-map.html" %}
```markup
<!doctype html>
<html lang="en">
<meta charset="UTF-8">

<head>
    <script src="https://cdn.rawgit.com/openlayers/openlayers.github.io/master/en/v5.3.0/build/ol.js"></script>
    <link rel="stylesheet" href="https://cdn.rawgit.com/openlayers/openlayers.github.io/master/en/v5.3.0/css/ol.css" type="text/css">
    <style>
        html, body {
            margin: 0;
            height: 100%;
        }

        #map {
            height: 100%;
            width: 100%;
        }
    </style>
    <title>DeFROST OpenLayers example</title>
</head>

<body>
    <div id="map"></div>
    <script type="text/javascript">
        var token = '<YOUR_ACCESS_TOKEN>';
        var defrost_maps_url = 'https://maps.staging.defrost.io/{z}/{x}/{y}.png';
        
        var map = new ol.Map({
            target: 'map',
            layers: [
                new ol.layer.Tile({
                    source: new ol.source.OSM()
                }),
                new ol.layer.Tile({
                    source: new ol.source.XYZ({
                        url: defrost_maps_url,
                        tileLoadFunction: (tile, src) => {
                            var client = new XMLHttpRequest();
                            client.open('GET', src);
                            client.responseType = "arraybuffer";
                            client.setRequestHeader("Authorization", "Bearer " + token);
                            client.onload = function () {
                                var arrayBufferView = new Uint8Array(this.response);
                                var blob = new Blob([arrayBufferView], { type: 'image/png' });
                                var urlCreator = window.URL || window.webkitURL;
                                var imageUrl = urlCreator.createObjectURL(blob);
                                tile.getImage().src = imageUrl;
                            };
                            client.send();
                        },
                        crossOrigin: 'anonymous',
                        attributions: 'Snow data &copy; <a href="https://www.defrost.io/">WeGaw Ltd.</a>',
                    }),
                    opacity: 0.3
                })
            ],
            view: new ol.View({
                center: ol.proj.fromLonLat([7.7491, 46.0207]),
                zoom: 12
            })
        });
    </script>
</body>

</html>
```
{% endcode %}
{% endtab %}

{% tab title="Leaflet" %}
{% code title="defrost-leaflet-map.html" %}
```markup
<!doctype html>
<html lang="en">
<meta charset="UTF-8">

<head>
    <script src="https://unpkg.com/leaflet@1.5.1/dist/leaflet.js"></script>
    <link rel="stylesheet" href="https://unpkg.com/leaflet@1.5.1/dist/leaflet.css" type="text/css">
    <style>
        html, body {
            margin: 0;
            height: 100%;
        }

        #map {
            height: 100%;
            width: 100%;
        }
    </style>
    <title>DeFROST Leaflet example</title>
</head>

<body>
    <div id="map"></div>
    <script type="text/javascript">
        var token = '<YOUR_ACCESS_TOKEN>';
        var defrost_maps_url = 'https://maps.staging.defrost.io/{z}/{x}/{y}.png';
        
        L.TileLayer.headers = L.TileLayer.extend({
            createTile(coords, done) {
                var tile = document.createElement('img');

                L.DomEvent.on(tile, 'load', L.Util.bind(this._tileOnLoad, this, done, tile));
                L.DomEvent.on(tile, 'error', L.Util.bind(this._tileOnError, this, done, tile));

                if (this.options.crossOrigin || this.options.crossOrigin === '') {
                    tile.crossOrigin = this.options.crossOrigin === true ? '' : this.options.crossOrigin;
                }

                /*
                Alt tag is set to empty string to keep screen readers from reading URL and for compliance reasons
                http://www.w3.org/TR/WCAG20-TECHS/H67
                */
                tile.alt = '';

                /*
                Set role="presentation" to force screen readers to ignore this
                https://www.w3.org/TR/wai-aria/roles#textalternativecomputation
                */
                tile.setAttribute('role', 'presentation');

                // Custom code to query tiles using Bearer Authentication headers 
                var url = this.getTileUrl(coords);
                var client = new XMLHttpRequest();
                client.open('GET', url);
                client.responseType = "arraybuffer";
                client.setRequestHeader("Authorization", "Bearer " + token);
                client.onload = function () {
                    var arrayBufferView = new Uint8Array(this.response);
                    var blob = new Blob([arrayBufferView], { type: 'image/png' });
                    var urlCreator = window.URL || window.webkitURL;
                    var imageUrl = urlCreator.createObjectURL(blob);
                    tile.src = imageUrl;
                    done(null, tile);
                };
                client.send();

                return tile;
            }
        });
        L.tileLayer.headers = (url, options) => new L.TileLayer.headers(url, options);

        map = L.map('map').setView([46.0207, 7.7491], 12);

        L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
            attribution: 'Map data &copy; <a href="https://www.openstreetmap.org/">OpenStreetMap</a> contributors',
        }).addTo(map);

        // Notice 
        L.tileLayer.headers(defrost_maps_url, {
            attribution: 'Snow data &copy; <a href="https://www.defrost.io/">WeGaw Ltd.</a>',
            crossOrigin: 'anonymous',
            opacity: 0.3
        }).addTo(map);
    </script>
</body>

</html>
```
{% endcode %}
{% endtab %}

{% tab title="Mapbox" %}
{% code title="defrost-mapbox-map.html" %}
```markup
<!doctype html>
<html lang="en">
<meta charset="UTF-8">

<head>
    <script src='https://api.tiles.mapbox.com/mapbox-gl-js/v1.2.0/mapbox-gl.js'></script>
    <link href='https://api.tiles.mapbox.com/mapbox-gl-js/v1.2.0/mapbox-gl.css' rel='stylesheet' />
    <style>
        html, body {
            margin: 0;
            height: 100%;
        }

        #map {
            height: 100%;
            width: 100%;
        }
    </style>
    <title>DeFROST Mapbox example</title>
</head>

<body>
    <div id="map"></div>
    <script type="text/javascript">
        var token = '<YOUR_ACCESS_TOKEN>';
        var defrost_maps_url = 'https://maps.staging.defrost.io/{z}/{x}/{y}.png';
        mapboxgl.accessToken = '<YOUR_MAPBOX_TOKEN>';
        
        var map = new mapboxgl.Map({
            container: 'map',
            style: 'mapbox://styles/mapbox/streets-v11',
            center: [7.7491, 46.0207],
            zoom: 11,
            transformRequest: (url, resourceType) => {
                if (resourceType === 'Tile' && url.startsWith(defrost_maps_url.split('/{z}/{x}/{y}.png')[0])) {
                    return {
                        url: url,
                        headers: { 'Authorization': 'Bearer ' + token },
                    }
                }
            }
        });

        map.on('load', function(){
            var dfTileLayer = {
                "id": 'df',
                "type": "raster",
                "source": {
                    "type": "raster",
                    "tiles": [defrost_maps_url,],
                    "tileSize": 256,
                    "maxzoom": 13
                },
                "paint": {
                    "raster-opacity": 0.3,
                    "raster-resampling": "linear"
                }
            };
            this.addLayer(dfTileLayer);
        });
    </script>
</body>

</html>
```
{% endcode %}
{% endtab %}

{% tab title="Google Maps" %}
{% code title="google-map.html" %}
```markup
<!doctype html>
<html lang="en">
<meta charset="UTF-8">

<head>
    <style>
        html, body {
            margin: 0;
            height: 100%;
        }

        .map {
            height: 100%;
            width: 100%;
        }
    </style>
    <title>DeFROST Google Maps example</title>
</head>

<body>
    <div id="map" class="map"></div>
    <script type="text/javascript">
        var token = '<YOUR_ACCESS_TOKEN>';
        var defrost_maps_url = 'https://maps.defrost.io/{z}/{x}/{y}.png';

        function initMap(){
            map = new google.maps.Map(document.getElementById('map'), {
                center: {lat: 46.0207, lng: 7.7491}, 
                zoom: 12
            });

            // Name the layer anything you like.
            var layerID = 'defrost_alps_snow';

            // Attention: Google Maps JS API does not allow to set an Authorization header
            // in each tile request. We are therefore forced to set the token as a query parameter.
            // BEWARE: this has an increased security risk, as the token is exposed. This is why it is
            // mandatory to whitelist the domains from which you will use it. 
            // Check https://defrost.io/api-docs#tag/Domain-whitelist to learn how.
            // Take into account that this demo will not work by simply opening the HTML file, since no
            // "Referrer" header will be set in the requests in that way.
            defrost_maps_url = defrost_maps_url + '?token=' + token;
            // Create a new ImageMapType layer.
            var layer = new google.maps.ImageMapType({
                name: layerID,
                getTileUrl: function(coord, zoom) {
                    var url = defrost_maps_url
                    .replace('{x}', coord.x)
                    .replace('{y}', coord.y)
                    .replace('{z}', zoom);
                    return url;
                },
                tileSize: new google.maps.Size(256, 256),
                minZoom: 1,
                maxZoom: 20,
                isPng: true,
                opacity: 0.30
            });

            // Register the new layer, then activate it.
            map.overlayMapTypes.push(layer);
        }
        
    </script>
    <script src="https://maps.googleapis.com/maps/api/js?key=<YOUR_GMAPS_API_KEY>&callback=initMap"
    async defer></script>
</body>

</html>
```
{% endcode %}
{% endtab %}
{% endtabs %}

The key point to keep in mind is that DeFROST Maps requires Bearer token Authentication. This forces libraries displaying tile layers to **include the appropriate Authentication header in each tile request**. While Mapbox supports this method out of the box, OpenLayers and Leaflet require a minor workaround: have a look in the examples above. In the special case of Google Maps, you have no option but to send the token as a query parameter, which forces you to [add any HTTP Referrer to your whitelist](https://defrost.io/api-docs#tag/Domain-whitelist).

### Next steps

You are now ready to integrate DeFROST! You can check the following additional resources:

{% hint style="success" %}
[Code Examples GitHub repository](https://github.com/wegaw/defrost-examples):  Full source code and starter project demonstrating integration of DeFROST Maps and API in supported platforms. 
{% endhint %}

