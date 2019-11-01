---
description: Daily updated snow cover map at 375 meters resolution
---

# Global Map

### Map Characteristics

The table below summarizes this map's key characteristics: 

| **Map Characteristics** |  |
| :--- | :--- |
| **Spatial resolution** | 375 meters |
| **Update time** | Daily at 4PM CET |
| **Tile zoom levels** | 9 zoom levels |
| **Tile size** | 256x256 pixels |
| **Default snow color** | Purple \(\#5350b2\) |

### Map Endpoint

To display the DeFROST Global snow cover map as a layer over the basemap of your choice, use the URL string below as the Tile Server endpoint:

```http
https://maps.defrost.io/global/v1/{z}/{x}/{y}.png
```

Pay attention to the fact that as any DeFROST endpoint, JWT Authentication is required for the Tile Server. This means **a valid JWT token has to be set in the HTTP Authorization request header**. Read more about Maps Authentication in the [Maps Overview section](overview.md#maps-authentication-json-web-tokens). 

