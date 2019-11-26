---
description: Daily updated snow cover map at 375 meters resolution
---

# Global Map

DeFROST operates and serves a daily snow cover map with 375 meters resolution for the entire world, excluding extreme latitudes \(i.e. the poles\) above or below the 70th parallels north and south.

![A custom rendering of DeFROST global map taken on 25th November 2019](../.gitbook/assets/globalmap.png)

### Map Characteristics

The table below summarizes this map's key characteristics: 

| **Map Characteristics** |  |
| :--- | :--- |
| **Spatial resolution** | 375 meters |
| **Update time** | Daily at 4PM CET |
| **Tile zoom levels** | 9 zoom levels |
| **Tile size** | 256x256 pixels |
| **Default snow color** | Purple \(\#5350b2\) |
| **Covered area** | 70°N to 70°S |

### Map Endpoint

To display the DeFROST Global snow cover map as a layer over the basemap of your choice, use the URL string below as the Tile Server endpoint:

```http
https://maps.defrost.io/global/v1/{z}/{x}/{y}.png
```

Pay attention to the fact that as any DeFROST endpoint, JWT Authentication is required for the Tile Server. This means **a valid JWT token has to be set in the HTTP Authorization request header**. Read more about Maps Authentication in the [Maps Overview section](maps-overview.md#maps-authentication-json-web-tokens). 

