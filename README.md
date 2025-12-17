# Sagaing Fault Seismicity & Building Exposure Map

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Data: USGS](https://img.shields.io/badge/Data-USGS-blue.svg)](https://earthquake.usgs.gov/)
[![Buildings: GlobalBuildingAtlas](https://img.shields.io/badge/Buildings-GlobalBuildingAtlas-orange.svg)](https://github.com/zhu-xlab/GlobalBuildingAtlas)

An interactive web map visualizing earthquake activity along Myanmar's Sagaing Fault system (March 28 - December 10, 2025), integrated with tectonic lineaments and building footprint data for seismic risk assessment.

![Map Preview](preview.png)

## 🌍 Live Demo

[View Live Map](https://drtinkooo.github.io/sagaing-fault-seismicity-buildings/)

## 📋 Overview

This project provides a comprehensive visualization of seismic activity following the devastating **M 7.7 Mandalay earthquake** on March 28, 2025 - one of the most significant seismic events in Myanmar's recent history. The map integrates multiple geospatial datasets to support:

- **Seismic hazard awareness** for communities along the Sagaing Fault
- **Building exposure analysis** using GlobalBuildingAtlas data
- **Tectonic context** through Myanmar's official lineament mapping
- **Public education** about earthquake risks in the region

## 🗺️ Features

### Data Layers

| Layer | Source | Description |
|-------|--------|-------------|
| **Earthquakes** | [USGS Earthquake Catalog](https://earthquake.usgs.gov/) | 164 events (M 2.5-7.7), March 28 - December 10, 2025 |
| **Tectonic Lineaments** | [Myanmar Tectonic Map 2011](https://github.com/drtinkooo/myanmar-earthquake-archive) | Official geological fault mapping |
| **Buildings** | [GlobalBuildingAtlas](https://github.com/zhu-xlab/GlobalBuildingAtlas) | 2.75 billion global building polygons with heights |

### Interactive Controls

- **Layer Toggle**: Enable/disable individual data layers
- **Magnitude Filter**: Slider to filter earthquakes by minimum magnitude (2.5-7.7)
- **Major Events List**: Quick navigation to significant earthquakes (M ≥ 5.0)
- **Multiple Basemaps**: Dark mode, satellite imagery, and OpenStreetMap
- **Coordinate Display**: Real-time cursor position tracking
- **Click Popups**: Detailed information for each feature

### Visual Design

- Modern dark theme optimized for cartographic display
- Color-coded earthquake markers by magnitude
- Responsive design for desktop and mobile devices
- Glass-morphism UI panels with backdrop blur effects

## 🚀 Quick Start

### Option 1: Direct Use

1. Download `index.html`
2. Open in any modern web browser
3. No server required - runs entirely client-side

### Option 2: Local Development

```bash
# Clone the repository
git clone https://github.com/drtinkooo/sagaing-fault-seismicity-buildings.git

# Navigate to directory
cd sagaing-fault-seismicity-buildings

# Open in browser (or use a local server)
open index.html

# Optional: Use Python's built-in server
python -m http.server 8000
# Then visit http://localhost:8000
```

### Option 3: GitHub Pages Deployment

1. Fork this repository
2. Go to Settings → Pages
3. Select "Deploy from a branch" → `main` → `/ (root)`
4. Your map will be available at `https://[username].github.io/sagaing-fault-seismicity-buildings/`

## 📊 Data Sources

### Earthquake Data

- **Source**: USGS Earthquake Hazards Program
- **API**: [USGS FDSNWS Event Query](https://earthquake.usgs.gov/fdsnws/event/1/)
- **Parameters**:
  - Time range: March 28, 2025 - December 10, 2025
  - Bounding box: 9.5°N - 28.5°N, 92°E - 101.2°E
  - Minimum magnitude: 2.5
- **Total Events**: 164 earthquakes
- **Major Event**: M 7.7 on March 28, 2025 (Mandalay earthquake)

### Tectonic Lineaments

- **Source**: Myanmar Tectonic Map 2011
- **Format**: GeoJSON
- **Repository**: [myanmar-earthquake-archive](https://github.com/drtinkooo/myanmar-earthquake-archive)
- **Features**: Major fault lines including the Sagaing Fault system

### Building Footprints

- **Source**: GlobalBuildingAtlas (Zhu et al., 2025)
- **Access**: Web Feature Service (WFS)
- **Endpoint**: `https://tubvsig-so2sat-vm1.srv.mwn.de/geoserver/ows`
- **Coverage**: Global (2.75 billion buildings)
- **Attributes**: Building height, footprint area, LoD1 3D models
- **License**: CC BY-NC 4.0

## 🔧 Technical Details

### Dependencies

All dependencies are loaded via CDN - no local installation required:

| Library | Version | Purpose |
|---------|---------|---------|
| [Leaflet](https://leafletjs.com/) | 1.9.4 | Interactive mapping |
| [Google Fonts](https://fonts.google.com/) | - | Typography (Outfit, IBM Plex Mono) |

### Browser Compatibility

| Browser | Supported |
|---------|-----------|
| Chrome | ✅ 90+ |
| Firefox | ✅ 88+ |
| Safari | ✅ 14+ |
| Edge | ✅ 90+ |
| Mobile browsers | ✅ |

### Performance Notes

- **Building layer**: Loads dynamically at zoom level ≥ 12 to optimize performance
- **Maximum features**: Limited to 1,500 buildings per view to prevent browser slowdown
- **Fallback**: Demo buildings displayed if WFS service is unavailable

## 📁 Project Structure

```
sagaing-fault-seismicity-buildings/
│
├── index.html          # Main application (self-contained)
├── README.md           # This documentation
├── LICENSE             # MIT License
├── CITATION.cff        # Citation metadata
├── preview.png         # Map preview image
│
└── docs/               # Additional documentation
    ├── DATA.md         # Detailed data documentation
    ├── METHODOLOGY.md  # Analysis methodology
    └── CHANGELOG.md    # Version history
```

## 🎨 Customization

### Modifying Earthquake Data

To update with new earthquake data, replace the `earthquakeData` object in `index.html`:

```javascript
const earthquakeData = {
    "type": "FeatureCollection",
    "features": [
        {
            "type": "Feature",
            "properties": {
                "mag": 5.2,
                "place": "Location description",
                "time": 1743144652709,  // Unix timestamp in milliseconds
                "url": "https://earthquake.usgs.gov/...",
                "felt": 45
            },
            "geometry": {
                "type": "Point",
                "coordinates": [longitude, latitude, depth]
            }
        }
        // ... more features
    ]
};
```

### Fetching Fresh USGS Data

```bash
# Example USGS API query
curl "https://earthquake.usgs.gov/fdsnws/event/1/query?format=geojson&starttime=2025-03-28&endtime=2025-12-10&minlatitude=9.5&maxlatitude=28.5&minlongitude=92&maxlongitude=101.2&minmagnitude=2.5&orderby=time"
```

### Styling Earthquakes

Modify the `getStyle()` function to change marker appearance:

```javascript
function getStyle(mag) {
    let r, c;
    if (mag >= 7.0) { r = 12; c = '#8B0000'; }      // Dark red
    else if (mag >= 6.0) { r = 10; c = '#DC143C'; } // Crimson
    else if (mag >= 5.0) { r = 7; c = '#FF4500'; }  // Orange red
    else if (mag >= 4.0) { r = 5; c = '#FF6347'; }  // Tomato
    else { r = 3.5; c = '#FFA07A'; }                // Light salmon
    return { radius: r, fillColor: c, color: '#fff', weight: 2, opacity: 1, fillOpacity: 0.85 };
}
```

### Adding Custom Basemaps

```javascript
const customLayer = L.tileLayer('https://your-tile-server/{z}/{x}/{y}.png', {
    attribution: 'Your attribution',
    maxZoom: 19
});
```

## 📈 The 2025 Myanmar Earthquake Sequence

### Main Event: M 7.7 Mandalay Earthquake

| Parameter | Value |
|-----------|-------|
| **Date & Time** | March 28, 2025, 06:20:52 UTC |
| **Epicenter** | 22.001°N, 95.925°E |
| **Depth** | 10 km |
| **Magnitude** | 7.7 Mw |
| **Rupture Length** | ~500-510 km |
| **Surface Offset** | 3-5 m average, up to 5 m peak |
| **Propagation** | Supershear (>5.3 km/s) |

### Sagaing Fault System

- **Length**: 1,200-1,500 km
- **Type**: Right-lateral strike-slip
- **Slip Rate**: 18-24 mm/year
- **Historical Gap**: Ruptured section not broken since 1839

### Affected Areas

- Mandalay Region
- Sagaing Region
- Nay Pyi Taw Union Territory
- Magway Region

## 📚 References

### Data Citations

**GlobalBuildingAtlas:**
```bibtex
@Article{essd-17-6647-2025,
    AUTHOR = {Zhu, X. X. and Chen, S. and Zhang, F. and Shi, Y. and Wang, Y.},
    TITLE = {GlobalBuildingAtlas: an open global and complete dataset of building polygons, heights and LoD1 3D models},
    JOURNAL = {Earth System Science Data},
    VOLUME = {17},
    YEAR = {2025},
    NUMBER = {12},
    PAGES = {6647--6668},
    DOI = {10.5194/essd-17-6647-2025}
}
```

**USGS Earthquake Catalog:**
```bibtex
@misc{usgs2025,
    author = {{U.S. Geological Survey}},
    title = {Earthquake Hazards Program},
    year = {2025},
    url = {https://earthquake.usgs.gov/}
}
```

**Myanmar Tectonic Map:**
```bibtex
@misc{myanmar_tectonic_2011,
    author = {{Myanmar Geosciences Society}},
    title = {Myanmar Tectonic Map},
    year = {2011}
}
```

### Related Resources

- [USGS Event Page - M 7.7 Myanmar](https://earthquake.usgs.gov/earthquakes/eventpage/us6000nth5)
- [GlobalBuildingAtlas Web Viewer](https://tubvsig-so2sat-vm1.srv.mwn.de)
- [GlobalBuildingAtlas Data Download](https://mediatum.ub.tum.de/1782307)

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request. For major changes, please open an issue first to discuss what you would like to change.

### Development Guidelines

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

### Reporting Issues

Please use the [GitHub Issues](https://github.com/drtinkooo/sagaing-fault-seismicity-buildings/issues) page to report bugs or request features.

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

### Data Licenses

| Dataset | License |
|---------|---------|
| Earthquake data | Public domain (USGS) |
| Tectonic lineaments | Open data |
| GlobalBuildingAtlas | CC BY-NC 4.0 |

**Note**: Building data from GlobalBuildingAtlas is licensed for non-commercial use only.

## 👤 Author

**Tin Ko Oo**
- GitHub: [@drtinkooo](https://github.com/drtinkooo)
- Affiliation: Mahidol University, Thailand

## 🙏 Acknowledgments

- [USGS Earthquake Hazards Program](https://earthquake.usgs.gov/) for real-time earthquake data
- [Zhu Lab, Technical University of Munich](https://github.com/zhu-xlab) for GlobalBuildingAtlas
- [Leaflet](https://leafletjs.com/) for the excellent mapping library
- [CARTO](https://carto.com/) for dark basemap tiles
- Myanmar Geosciences Society for tectonic data

---

<p align="center">
  <i>Created for seismic hazard awareness and public education</i>
  <br>
  <i>In memory of those affected by the 2025 Myanmar earthquake</i>
</p>
