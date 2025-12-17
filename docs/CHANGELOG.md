# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.0] - 2025-12-17

### Added

- Initial release of the Sagaing Fault Seismicity & Building Exposure Map
- **Earthquake Layer**
  - 164 earthquakes from USGS (March 28 - December 10, 2025)
  - Color-coded markers by magnitude (M 2.5 - 7.7)
  - Interactive popups with detailed event information
  - Links to USGS event pages
- **Tectonic Lineaments Layer**
  - Myanmar Tectonic Map 2011 data
  - Interactive popups with feature properties
- **Building Footprints Layer**
  - GlobalBuildingAtlas WFS integration
  - Dynamic loading at zoom level ≥ 12
  - Building height and area information
  - Fallback demo buildings when WFS unavailable
- **User Interface**
  - Dark theme cartographic design
  - Layer toggle controls
  - Magnitude filter slider (2.5 - 7.7)
  - Major events list with click-to-zoom
  - Real-time coordinate display
  - Statistics panel
- **Basemaps**
  - CARTO Dark Matter (default)
  - Esri World Imagery (satellite)
  - OpenStreetMap
- **Documentation**
  - Comprehensive README.md
  - DATA.md with detailed data documentation
  - CITATION.cff for academic citation
  - MIT License with data licensing notes

### Technical Details

- Built with Leaflet 1.9.4
- Self-contained single HTML file
- No server-side dependencies
- Responsive design for desktop and mobile
- CDN-based dependencies (no local installation required)

---

## Future Plans

### [1.1.0] - Planned

- [ ] Time-lapse animation of earthquake sequence
- [ ] Depth visualization (3D or depth filter)
- [ ] Aftershock clustering analysis
- [ ] Export functionality (GeoJSON, CSV)
- [ ] Print/PDF map generation

### [1.2.0] - Planned

- [ ] Multi-language support (Myanmar, Thai)
- [ ] Offline PWA capability
- [ ] Custom earthquake data upload
- [ ] Historical earthquake comparison
- [ ] Population exposure statistics

---

## Version History Summary

| Version | Date | Description |
|---------|------|-------------|
| 1.0.0 | 2025-12-17 | Initial release |

---

*For detailed commit history, see the [GitHub repository](https://github.com/drtinkooo/sagaing-fault-seismicity-buildings/commits/main).*
