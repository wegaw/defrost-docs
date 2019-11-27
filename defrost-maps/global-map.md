---
description: Daily updated snow cover map at 375 meters resolution
---

# Global Map

DeFROST operates and serves a daily snow cover map with 375 meters resolution for the entire world, excluding extreme latitudes \(i.e. the arctic and antarctic circles\).

![Global snow map from 27th November 2019 - red lines indicate latitude coverage boundaries](../.gitbook/assets/global.png)

Polar latitudes are mapped, but are subject to very low resolution and update frequency to seasonal perpetual darkness conditions in winter. Therefore, we currently do not recommend using the global map for latitudes above or below the 66.5° parallels south or north. 

### Map Characteristics

The table below summarizes this map's key characteristics: 

| **Map Characteristics** |  |
| :--- | :--- |
| **Spatial resolution** | 375 meters |
| **Update time** | Daily at 4PM CET |
| **Tile zoom levels** | 9 zoom levels |
| **Tile size** | 256x256 pixels |
| **Default snow color** | Purple \(\#5350b2\) |
| **Covered area** | 66.5°N to 66.5°S |

### Map Endpoint

To display the DeFROST Global snow cover map as a layer over the basemap of your choice, use the URL string below as the Tile Server endpoint:

```http
https://maps.defrost.io/global/v1/{z}/{x}/{y}.png
```

Pay attention to the fact that as any DeFROST endpoint, JWT Authentication is required for the Tile Server. This means **a valid JWT token has to be set in the HTTP Authorization request header**. Read more about Maps Authentication in the [Maps Overview section](maps-overview.md#maps-authentication-json-web-tokens). 

