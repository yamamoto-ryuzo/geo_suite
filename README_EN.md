[日本語版: `README.md`]

## GeoSuite — QGIS Desktop + WebGIS Full-cycle Tool Suite

GeoSuite is a collection of QGIS-centered plugins that automate the full cycle from data ingestion to search, web sharing, and report generation.

## Project Overview

- Scope: ingestion (local/CKAN) → search → web sharing → report generation (PNG/PDF/XLSX)
- Target users: organizations using QGIS for business workflows that want to simplify internal sharing and web publishing

## Workflow

```
Local/CKAN
  ↓
GeoImport (automated GIS ingestion)
  ↓
GeoSearch (map-based search)
  ↓
GeoWebView (style-aware web sharing)
  ↓
GeoReport (layout editing, export, report generation)
```

## Quickstart

1. Install each plugin into QGIS (see each component's repository README)
2. Register data with `GeoImport` (CSV / CKAN)
3. Search and extract areas with `GeoSearch`
4. Generate styled packages / permalinks with `GeoWebView` for sharing
5. Apply layouts and export high-resolution PNG/PDF with `GeoReport`

> Note: XLSX (embedded images) full automation differs between plugin READMEs; `GeoReport` documents current capabilities but check component READMEs for details.

## Components

Each component is maintained in a separate repository. The status below reflects README contents as of 2025-11-30.

---

### GeoImport — Automated GIS ingestion (CKAN / Local)
- Repository: https://github.com/yamamoto-ryuzo/qgis-data-catalog-integration

- Current (2025-11-30):
  - Ingestion from CKAN servers and CKAN-compatible local folders
  - Auto-detection for CSV delimiters and character encodings (UTF-8 / CP932, etc.)
  - Automatic point geometry creation when latitude/longitude columns exist
  - SQLite-based local cache for faster searches

- Future possibilities:
  - STAC / DCAT metadata integration and automatic indexing
  - Large-data ingestion (parallel/streaming, S3-compatible storage)
  - Point-cloud (LAS/LAZ) and 3D feature ingestion (PDAL integration)
  - Improved auto-georeference and CRS detection, automated data quality checks

### GeoSearch — Map-based search (attribute & spatial)
- Repository: https://github.com/yamamoto-ryuzo/GEO-search-plugin

- Current (2025-11-30):
  - Multiple search modes (land parcel number, owner, general attributes)
  - Results shown per-layer in tabs; click to zoom/select on map
  - `selectTheme` support and additive display mode
  - Stabilization for Qt5/Qt6 (QGIS 3.x) compatibility

- Future possibilities:
  - Full-text search enhancements with PostGIS / Elasticsearch / OpenSearch
  - Federated searches across multiple data sources, spatial index optimization
  - Time-series and versioned searches
  - Spatial filters with analytics (buffer, spatial join, attribute scoring)

### GeoWebView — Style-aware web sharing
- Repository: https://github.com/yamamoto-ryuzo/QMapPermalink

- Current (2025-11-30):
  - Export QGIS view state (center, zoom, layer visibility, styles) as permalink or HTML/PNG package
  - Lightweight HTTP server for internal distribution and WFS support for feature delivery
  - Style injection for MapLibre / OpenLayers (with fallback for MapLibre)
  - High-resolution PNG exports and Office export templates (Excel/PowerPoint examples)

- Notes: Vector tile server generation is currently marked as deferred in the component README.

### GeoReport — Layout editing, export, and report generation
- Repository: https://github.com/yamamoto-ryuzo/qgis-layoutitem-selector

- Current (2025-11-30):
  - Save/apply layout templates (JSON-based)
  - Batch edit layout items (maps, legend, labels, images)
  - RubberBand print extent display and mouse-driven adjustments
  - Atlas-like bulk exports; high-resolution PNG/PDF output

---

## Related Tools

- `yr-qgis-launcher` — Portable QGIS / QField environment launcher
- Repository: https://github.com/yamamoto-ryuzo/yr-qgis-launcher

- Current (2025-11-30):
  - `ProjectFile.exe` for direct project launch, permission-based UI and `startup.py` for layer initialization
  - `local-launcher.bat` / `qgislocalsync.config` for local sync (robocopy-based) and auto-launch workflow
  - Version-differential sync for portable QGIS / QField, sample list of bundled plugins
  - Windows batch oriented; README documents deployment path (ASCII-only) and CRLF considerations

- Use case: Useful for offline/portable deployments and unified runtime environments via cloud-sync (e.g., BOX)

## Scenarios

- Internal reporting workflow: `GeoImport` → `GeoSearch` → `GeoWebView` → `GeoReport`
- Web map publishing: package and permalink via `GeoWebView`
- Bulk export: use layout templates for large Atlas outputs

## Contributing

- Components are maintained in their own repositories. Please file issues on the relevant component repo.
- Documentation fixes, translations and Quickstart improvements are welcome via pull requests to this repository.

## Support and License

- Contact: use Issues on the relevant component repositories.
- License: see each component's README / LICENSE.

---

Note: This file was composed on 2025-11-30 referencing individual component READMEs. For latest details, check each component's README and CHANGELOG.md.

-- Japanese version: `README.md` --
