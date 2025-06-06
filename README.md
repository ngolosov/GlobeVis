# Globe Visualization Templates

[![GitHub Repository](https://img.shields.io/badge/GitHub-Repository-blue.svg)](https://github.com/ngolosov/GlobeVis/)

This repository contains templates for creating interactive 3D globe visualizations of various global datasets. The templates are designed for the GeoGraphics lab and come in two versions: CSV-based and JSON-based.

## Overview

These templates allow you to create interactive globe visualizations where countries are colored based on various metrics, with optional features like markers and tooltips. The globe is interactive, allowing users to:
- Rotate and zoom the view
- Hover over countries to see detailed information
- View color-coded data representation
- (Optional) Interact with markers for specific locations

## Template Versions

### 1. CSV Version
Located in the `csv_version/` directory, this version accepts data in CSV format.

#### Input Requirements:
- Main data file must be a CSV with at least these columns:
  - `alpha_3_code`: Three-letter country code (e.g., "USA", "GBR")
  - `value`: Numerical value for the metric being visualized

Example CSV format:
```csv
alpha_3_code,value
USA,75.2
GBR,82.1
```

### 2. JSON Version
Located in the `js_version/` directory, this version accepts data in JSON format.

#### Input Requirements:
Either:

A) Use a separate JSON data file with the following structure:
```json
{
  "countryData": [
    {
      "Alpha-3 code": "USA",
      "data": [
        {
          "year": 2020,
          "value": 75.2
        }
      ]
    }
  ]
}
```

B) Use attributes directly from the GeoJSON file:
You can add your data directly to the GeoJSON file's properties and use them in the visualization. This is often simpler if you have a single value per country. To do this:

1. Add your data as properties in the GeoJSON file:
```json
{
  "type": "Feature",
  "properties": {
    "ADMIN": "United States",
    "ISO_A2": "US",
    "your_metric": 75.2  // Add your custom attribute here
  },
  "geometry": { ... }
}
```

2. Modify the `coloringConfig` in the template:
```javascript
const coloringConfig = {
  title: 'Your Metric Name',
  getValueFunction: feat => feat.properties.your_metric || 0,  // Reference your custom attribute
  classes: [
    // ... color classes ...
  ]
};
```

This approach is demonstrated in the `_Single variable.html` template, which uses properties directly from the GeoJSON file.

## Available Templates

Both versions include templates for visualizing various metrics:
- Poverty Headcount Ratio
- Government Effectiveness Index
- Gender Inequality Index
- Refugee Population by Country
- Access to Electricity
- City Markers (with custom markers on the globe)

## How to Use

1. Choose the appropriate version (CSV or JSON) based on your data format
2. Copy the relevant template file from either `csv_version/` or `js_version/`
3. Prepare your data file according to the format requirements
4. Place your data file in the `datasets/` directory
5. Update the template file to:
   - Point to your data file
   - Modify the title and legend as needed
   - Adjust the color scale and ranges if necessary

## Required Files

- `datasets/ne_110m_admin_0_countries.geojson`: Base map data (included)
- Your data file (CSV or JSON)
- For marker-based visualizations: `datasets/markers.json` (if using markers)

## Customization

Each template includes configurable options for:
- Color scales and ranges
- Legend formatting
- Tooltip content
- Auto-rotation speed
- Marker size and appearance (if using markers)

## Dependencies

The templates use:
- Three.js for 3D rendering
- D3.js for data processing and color scales
- Custom Globe visualization library

## Getting Started

1. Choose a template that matches your data type (CSV or JSON)
2. Prepare your data file in the correct format
3. Update the `coloringConfig` object in the template to match your data ranges
4. Update the tooltip format to display relevant information
5. Test the visualization in a web browser

## Notes

- The templates automatically filter out Antarctica from the visualization
- All visualizations include auto-rotation (can be disabled)
- Responsive design is included for proper sizing on different screens
- Tooltips show country name, ISO code, and relevant data values 

## Live Examples

### CSV Version Templates

| Template Name | Description | Live Demo |
|--------------|-------------|-----------|
| Access to Electricity | Visualizes percentage of population with access to electricity | [View Demo](https://golosov.pro/GlobeVis/csv_version/Access%20to%20Electricity.html) |
| Gender Inequality Index | Shows gender inequality index by country | [View Demo](https://golosov.pro/GlobeVis/csv_version/Gender%20Inequality%20Index.html) |
| Government Effectiveness Index | Displays government effectiveness metrics | [View Demo](https://golosov.pro/GlobeVis/csv_version/Government%20Effectiveness%20Index.html) |
| Poverty Headcount Ratio | Shows poverty rates across countries | [View Demo](https://golosov.pro/GlobeVis/csv_version/Poverty%20Headcount%20Ratio.html) |
| Poverty Headcount Ratio with markers | Same as above with additional location markers | [View Demo](https://golosov.pro/GlobeVis/csv_version/Poverty%20Headcount%20Ratio%20with%20markers.html) |
| Refugee Population by Country | Visualizes refugee population distribution | [View Demo](https://golosov.pro/GlobeVis/csv_version/Refugee%20Population%20by%20Country.html) |
| City Markers | Displays major cities as markers on the globe | [View Demo](https://golosov.pro/GlobeVis/csv_version/City%20Markers.html) |

### JavaScript Version Templates

| Template Name | Description | Live Demo |
|--------------|-------------|-----------|
| Single Variable | Basic template using GeoJSON properties directly | [View Demo](https://golosov.pro/GlobeVis/js_version/_Single%20variable.html) |
| Government Effectiveness Index | Displays government effectiveness metrics | [View Demo](https://golosov.pro/GlobeVis/js_version/Government%20Effectiveness%20Index.html) |
| Poverty Headcount Ratio | Shows poverty rates across countries | [View Demo](https://golosov.pro/GlobeVis/js_version/Poverty%20Headcount%20Ratio.html) |
| Poverty Headcount Ratio with markers | Same as above with additional location markers | [View Demo](https://golosov.pro/GlobeVis/js_version/Poverty%20Headcount%20Ratio%20with%20markers.html) |
| Refugee Population by Country | Visualizes refugee population distribution | [View Demo](https://golosov.pro/GlobeVis/js_version/Refugee%20Population%20by%20Country.html) | 

## How to embed this in the WordPress page
Navigate to the Pages in the admin console. Edit/create a page. Switch to the "text" mode in the editor. Copy-paste this code to the editor. Replace the `src` tag with the visualization file URL.
```html
<iframe 
  src="https://golosov.pro/GlobeVis/csv_version/Access%20to%20Electricity.html" 
  width="100%" 
  height="600px" 
  frameborder="0"
  style="border: none; border-radius: 8px;">
</iframe>
}
```
