# Interactive Home Value Index Visualization

This project creates an interactive time-series map visualization of median home values by county in California using the Zillow Home Value Index data.

## Overview

The notebook demonstrates how to:
1. Load geospatial data from a remote source
2. Apply custom color coding based on home value ranges
3. Create an interactive map with a time slider
4. Display the data with a custom legend

## What This Does

The visualization shows the evolution of median home values across California counties over time. Users can:
- Navigate through different time periods using an interactive slider
- View color-coded counties based on home value ranges
- Zoom and pan around the map
- See detailed information for each county

## Technologies Used

### Core Libraries
- **leafmap**: A Python package for interactive mapping and geospatial analysis built on top of ipyleaflet and folium
- **geopandas**: Extends pandas to work with geospatial data, providing geometric operations and spatial indexing
- **pandas**: Data manipulation and analysis library (used internally by geopandas)

### Data Source
- **Zillow Home Value Index**: County-level median home value data for California
- **GeoJSON format**: Geospatial data format that combines geographic features with attribute data

## Features

### Color Coding System
The visualization uses a progressive color scheme to represent different home value ranges:
- **$0 - $200,000**: Very light red (`#ffe6e6`)
- **$200,000 - $400,000**: Light red (`#fbb4b4`)
- **$400,000 - $600,000**: Medium red (`#fc8888`)
- **$600,000 - $800,000**: Medium-dark red (`#fc4e4e`)
- **$800,000 - $1,000,000**: Dark red (`#e31a1c`)
- **$1,000,000 - $2,000,000**: Very dark red (`#99000d`)
- **No Data**: Light gray (`#f0f0f0`)

### Interactive Components
- **Time Slider**: Navigate through different time periods with 0.05-second intervals
- **Zoom to Layer**: Automatically fits the map view to show all data
- **Legend**: Clear visual reference for interpreting the color coding

## Installation

To run this notebook, you'll need to install the required packages:

```bash
pip install leafmap geopandas
```

Or using conda:

```bash
conda install -c conda-forge leafmap geopandas
```

## Usage

1. Open the Jupyter notebook
2. Run all cells in sequence
3. The final cell will display an interactive map
4. Use the time slider to explore how home values changed over time
5. Click and drag to pan, use mouse wheel to zoom

## Data Structure

The dataset includes:
- **Geographic boundaries**: County polygons for California
- **Time-series data**: Median home values across multiple time periods
- **Metadata**: County names, FIPS codes, and other identifying information

## File Structure

```
VectorTimeSlider/
├── README.md                    # This file
└── ZillowTimeSeries.ipynb      # Main Jupyter notebook with visualization code
```

## Code Walkthrough

### Data Loading
```python
# Load geospatial data from remote source
link = "https://github.com/opengeos/datasets/releases/download/us/zillow_home_value_index_by_county_ca.geojson"
data = gpd.read_file(link)
```

### Color Coding
```python
# Apply custom color scheme based on home value ranges
gdf = leafmap.color_code_dataframe(data, legend_dict=legend_dict)
```

### Interactive Visualization
```python
# Create map with time slider and legend
m = leafmap.Map()
m.add_gdf_time_slider(gdf, time_interval=0.05, zoom_to_layer=True)
m.add_legend(title="Median Home Value", legend_dict=legend_dict)
```

## Applications

This visualization technique can be applied to:
- Real estate market analysis
- Urban planning and development
- Economic research and policy analysis
- Educational demonstrations of geographic data visualization
- Investment decision support

## Notes

- The visualization automatically handles missing data by assigning a neutral gray color
- The time slider allows for smooth animation through the temporal dataset
- The map is fully interactive and supports standard web map navigation
- Color coding provides immediate visual understanding of value distributions across geographic areas

## Contributing

Feel free to fork this project and submit pull requests for improvements or additional features.

## License

This project is open source and available under the MIT License.
