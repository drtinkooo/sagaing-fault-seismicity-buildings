# Data Documentation

This document provides detailed information about the data sources, formats, and processing methods used in this project.

## Table of Contents

1. [Earthquake Data](#earthquake-data)
2. [Tectonic Lineaments](#tectonic-lineaments)
3. [Building Footprints](#building-footprints)
4. [Data Processing](#data-processing)
5. [Data Updates](#data-updates)

---

## Earthquake Data

### Source

**USGS Earthquake Hazards Program**
- Website: https://earthquake.usgs.gov/
- API: FDSNWS Event Web Service
- Endpoint: `https://earthquake.usgs.gov/fdsnws/event/1/query`

### Query Parameters

| Parameter | Value | Description |
|-----------|-------|-------------|
| `starttime` | 2025-03-28 | Start of monitoring period |
| `endtime` | 2025-12-10 | End of monitoring period |
| `minlatitude` | 18.375256 | Southern boundary |
| `maxlatitude` | 23.871374 | Northern boundary |
| `minlongitude` | 95.270039 | Western boundary |
| `maxlongitude` | 96.797532 | Eastern boundary |
| `minmagnitude` | 2.5 | Minimum magnitude threshold |
| `orderby` | time-asc | Sort by time (oldest → newest) |
| `format` | geojson | Output format |

### API Query URL

```
https://earthquake.usgs.gov/fdsnws/event/1/query?format=geojson&starttime=2025-03-28&endtime=2025-12-10&minlatitude=18.375256&maxlatitude=23.871374&minlongitude=95.270039&maxlongitude=96.797532&minmagnitude=2.5&orderby=time-asc-asc
```

### Data Schema

```json
{
  "type": "FeatureCollection",
  "metadata": {
    "generated": 1765368828000,
    "url": "...",
    "title": "USGS Earthquakes",
    "status": 200,
    "api": "1.14.1",
    "count": 83
  },
  "features": [
    {
      "type": "Feature",
      "id": "us6000nth5",
      "properties": {
        "mag": 7.7,
        "place": "28 km NNE of Sagaing, Burma (Myanmar)",
        "time": 1743144652709,
        "updated": 1743150000000,
        "tz": null,
        "url": "https://earthquake.usgs.gov/earthquakes/eventpage/us6000nth5",
        "detail": "...",
        "felt": 1128,
        "cdi": 8.1,
        "mmi": 8.5,
        "alert": "red",
        "status": "reviewed",
        "tsunami": 0,
        "sig": 1180,
        "net": "us",
        "code": "6000nth5",
        "magType": "mww",
        "type": "earthquake",
        "title": "M 7.7 - 28 km NNE of Sagaing, Burma (Myanmar)"
      },
      "geometry": {
        "type": "Point",
        "coordinates": [95.9252, 22.001, 10.0]
      }
    }
  ]
}
```

### Key Properties

| Property | Type | Description |
|----------|------|-------------|
| `mag` | Number | Magnitude value |
| `place` | String | Location description |
| `time` | Number | Unix timestamp (milliseconds) |
| `url` | String | USGS event page URL |
| `felt` | Number | Number of felt reports |
| `cdi` | Number | Community Decimal Intensity |
| `mmi` | Number | Modified Mercalli Intensity |
| `depth` | Number | Depth in km (in geometry.coordinates[2]) |

### Statistics Summary

| Metric | Value |
|--------|-------|
| Total Events | 83 |
| Magnitude Range | 3.4 - 7.7 |
| Events M ≥ 5.0 | 6 |
| Events M ≥ 6.0 | 2 |
| Events M ≥ 7.0 | 1 |
| Depth Range | 4.5 - 141.5 km |
| Median Depth | 10.0 km |


---

## Tectonic Lineaments

### Source

**Myanmar Tectonic Map 2011**
- Publisher: Myanmar Geosciences Society
- Repository: https://github.com/drtinkooo/myanmar-earthquake-archive
- File: `Myanmar_Tectonic_Map_2011.geojson`

### Data Description

The tectonic lineament data represents major geological fault structures in Myanmar, including:

- **Sagaing Fault**: The main right-lateral strike-slip fault (~1,200-1,500 km)
- **Kabaw Fault**: Western boundary fault system
- **Shan Scarp**: Eastern boundary structures
- **Subsidiary faults**: Secondary fault splays and branches

### Data Schema

```json
{
  "type": "FeatureCollection",
  "features": [
    {
      "type": "Feature",
      "properties": {
        "NAME": "Sagaing Fault",
        "TYPE": "Strike-slip",
        "ACTIVITY": "Active"
      },
      "geometry": {
        "type": "LineString",
        "coordinates": [
          [lon1, lat1],
          [lon2, lat2],
          ...
        ]
      }
    }
  ]
}
```

### Sagaing Fault Characteristics

| Parameter | Value |
|-----------|-------|
| Length | 1,200-1,500 km |
| Type | Right-lateral strike-slip |
| Slip Rate | 18-24 mm/year |
| Strike | N-S to NNE-SSW |
| Major Segments | Northern, Central, Southern |

---

## Building Footprints

### Source

**GlobalBuildingAtlas**
- Authors: Zhu et al. (2025)
- Repository: https://github.com/zhu-xlab/GlobalBuildingAtlas
- Paper: Earth System Science Data, 17, 6647-6668
- DOI: 10.5194/essd-17-6647-2025

### Access Methods

#### 1. Web Feature Service (WFS)

```
Base URL: https://tubvsig-so2sat-vm1.srv.mwn.de/geoserver/ows
```

**Example Request:**
```
https://tubvsig-so2sat-vm1.srv.mwn.de/geoserver/ows?
  service=WFS&
  version=1.1.0&
  request=GetFeature&
  typeName=GBAData:LoD1_buildings&
  outputFormat=application/json&
  srsName=EPSG:4326&
  bbox=95.5,21.0,96.5,22.5,EPSG:4326&
  maxFeatures=1000
```

#### 2. Web Viewer

Interactive viewer: https://tubvsig-so2sat-vm1.srv.mwn.de

#### 3. Full Download

MediaTUM: https://mediatum.ub.tum.de/1782307

### Data Schema

```json
{
  "type": "FeatureCollection",
  "features": [
    {
      "type": "Feature",
      "properties": {
        "height": 12.5,
        "area": 156.8,
        "confidence": 0.92
      },
      "geometry": {
        "type": "Polygon",
        "coordinates": [
          [
            [lon1, lat1],
            [lon2, lat2],
            [lon3, lat3],
            [lon4, lat4],
            [lon1, lat1]
          ]
        ]
      }
    }
  ]
}
```

### Data Specifications

| Attribute | Description | Unit |
|-----------|-------------|------|
| `height` | Building height | meters |
| `area` | Footprint area | square meters |
| `confidence` | Prediction confidence | 0-1 |

### Coverage Statistics

| Metric | Value |
|--------|-------|
| Global Building Count | 2.75 billion |
| Spatial Resolution | 3 × 3 meters |
| Tile Size | 5° × 5° |
| Data Formats | GeoJSON, GeoTIFF |
| Height Model | LoD1 (Level of Detail 1) |

### Myanmar Coverage

The GlobalBuildingAtlas provides complete coverage for Myanmar, including:
- Urban areas: Mandalay, Sagaing, Nay Pyi Taw, Yangon
- Rural settlements along the Sagaing Fault corridor
- Estimated millions of building footprints in the affected region

---

## Data Processing

### Earthquake Data Processing

1. **Acquisition**: USGS API query with specified parameters
2. **Filtering**: Events within Myanmar bounding box, M ≥ 2.5
3. **Embedding**: GeoJSON directly embedded in HTML for offline capability
4. **Validation**: Cross-checked with USGS event pages

### Tectonic Data Processing

1. **Source**: Direct fetch from GitHub repository
2. **Format**: Native GeoJSON, no transformation required
3. **Loading**: Dynamic fetch at map initialization

### Building Data Processing

1. **WFS Query**: Bounding box request for current map view
2. **Feature Limit**: Maximum 1,500 features per request
3. **Zoom Threshold**: Buildings loaded only at zoom ≥ 12
4. **Fallback**: Demo buildings generated if WFS unavailable

---

## Data Updates

### Updating Earthquake Data

To refresh earthquake data with the latest events:

```bash
# Download latest data
curl -o earthquakes.geojson "https://earthquake.usgs.gov/fdsnws/event/1/query?format=geojson&starttime=2025-03-28&endtime=$(date +%Y-%m-%d)&minlatitude=18.375256&maxlatitude=23.871374&minlongitude=95.270039&maxlongitude=96.797532&minmagnitude=2.5&orderby=time-asc"

# Or use Python
python3 -c "
import urllib.request
import json
from datetime import datetime

url = f'https://earthquake.usgs.gov/fdsnws/event/1/query?format=geojson&starttime=2025-03-28&endtime={datetime.now().strftime(\"%Y-%m-%d\")}&minlatitude=18.375256&maxlatitude=23.871374&minlongitude=95.270039&maxlongitude=96.797532&minmagnitude=2.5&orderby=time-asc'

with urllib.request.urlopen(url) as response:
    data = json.loads(response.read())
    print(f'Total events: {len(data[\"features\"])}')
    with open('earthquakes.geojson', 'w') as f:
        json.dump(data, f)
"
```

### Update Frequency Recommendations

| Data Type | Recommended Update | Reason |
|-----------|-------------------|--------|
| Earthquakes | Weekly/Monthly | Ongoing seismicity |
| Tectonic Lines | Rarely | Static geological data |
| Buildings | Annually | Slow urban change |

---

## Data Quality Notes

### Earthquake Data

- **Completeness**: Good for M ≥ 4.0, variable for smaller events
- **Location Accuracy**: ±5-10 km for most events
- **Depth Uncertainty**: Higher for shallow events (<20 km)
- **Review Status**: Mix of automatic and reviewed solutions

### Building Data

- **Source Imagery**: Planet satellite imagery (3m resolution)
- **Extraction Method**: Deep learning (UNet + regularization)
- **Height Estimation**: Monocular height estimation (HTC-DC Net)
- **Known Limitations**: 
  - Rural areas may have lower completeness
  - Height accuracy varies by building type
  - Some vegetation misclassification possible

---

## License Summary

| Dataset | License | Commercial Use |
|---------|---------|----------------|
| USGS Earthquakes | Public Domain | ✅ Allowed |
| Myanmar Tectonic Map | Open Data | ✅ Allowed |
| GlobalBuildingAtlas | CC BY-NC 4.0 | ❌ Non-commercial only |

---

*Last updated: December 2025*
