# Predicting Home Values in 3D with PDFM Features

A comprehensive geospatial analysis project that visualizes and predicts residential home values using 3D mapping techniques and PDFM (Population Dynamics Foundation Model) embeddings.

## 📋 Overview

This project combines Zillow's Home Value Index (ZHVI) data with county-level geospatial boundaries to create interactive 3D visualizations of median home values across the United States. The notebook demonstrates advanced spatial data integration and 3D choropleth mapping techniques.

<img width="800" height="800" alt="newplot" src="https://github.com/user-attachments/assets/27892fdf-1c8c-468c-827b-b655db222d41" />

<img width="528" height="575" alt="Screenshot 2025-08-05 at 1 36 28 PM" src="https://github.com/user-attachments/assets/9e7b50a2-baab-4edb-ba4d-10bd9af8caf2" />

## 🎯 Objectives

- **3D Visualization**: Create extruded 3D maps showing home values by county
- **Data Integration**: Merge Zillow home value data with US county geometries
- **Interactive Mapping**: Develop rotatable, zoomable 3D visualizations
- **PDFM Integration**: Prepare framework for machine learning predictions using place embeddings
- **Spatial Analysis**: Analyze geographic patterns in residential real estate values

## 🗂️ Project Structure

```
PredictingHomeValuesIn3D/
├── PDFMFEATURES.ipynb         # Main analysis notebook
├── README.md                  # This file
└── Generated Data/
    ├── zillow_home_value_index_by_county.csv  # Downloaded ZHVI data
    └── county.geojson                         # US county boundaries
```

## 📚 What's Included

### 1. Data Acquisition & Processing
- **Zillow Home Value Index**: County-level median home values (October 2024)
- **US County Boundaries**: High-resolution GeoJSON polygons for all US counties
- **Automated Downloads**: Self-contained data retrieval system

### 2. Geospatial Data Integration
- **Index Standardization**: FIPS code mapping between datasets
- **Coordinate System Alignment**: Proper geometric projections
- **Data Quality Validation**: Geometry and attribute verification

### 3. Interactive Visualizations

#### Standard 2D Choropleth Map
- Color-coded counties by median home value
- Interactive zoom and pan capabilities
- Legend with value ranges

#### Advanced 3D Extruded Map
- **Height Dimension**: County extrusion based on home values
- **60-degree Pitch**: Optimal viewing angle for 3D effects
- **Scale Factor**: 3x extrusion for enhanced visibility
- **Rotation Support**: Full 360-degree navigation

### 4. PDFM Integration Framework
- Placeholder structure for Place Description Foundation Model embeddings
- Machine learning pipeline preparation
- Feature engineering capabilities

## 🛠️ Technologies Used

- **leafmap**: Primary 3D mapping and visualization library
- **GeoPandas**: Geospatial data manipulation and analysis
- **Pandas**: Data processing and transformation
- **MapLibre GL JS**: Underlying web-based mapping engine
- **scikit-learn**: Machine learning framework (prepared for PDFM)
- **Python**: Core programming language

## 🚀 Getting Started

### Prerequisites
```bash
pip install leafmap[maplibre] geopandas pandas scikit-learn
```

### Running the Analysis
1. Open `PDFMFEATURES.ipynb` in Jupyter Notebook/Lab
2. Run cells sequentially to:
   - Download required datasets
   - Process and merge spatial data
   - Generate 2D and 3D visualizations
3. Interact with the generated maps

### Key Features Demonstrated

**Data Pipeline**:
```python
# Automated data download and processing
zhvi_df = pd.read_csv(zhvi_file)
county_gdf = gpd.read_file(county_geojson)

# Index mapping for proper joins
county_gdf_reset['geoId'] = 'geoId/' + county_gdf_reset['FIPS']
```

**3D Visualization**:
```python
# Create extruded 3D map
m = leafmap.Map(style="liberty", pitch=60)
m.add_data(gdf, extrude=True, scale_factor=3)
```

## 🔧 Key Technical Solutions

### Index Mapping Resolution
**Challenge**: Mismatched identifiers between Zillow and county data
**Solution**: FIPS code extraction and geoId format standardization
```python
county_gdf_reset['FIPS'] = county_gdf_reset['GEO_ID'].str[-5:]
county_gdf_reset['geoId'] = 'geoId/' + county_gdf_reset['FIPS']
```

### Geometry Integration
**Challenge**: Joining tabular data with spatial geometries
**Solution**: Proper index alignment and GeoDataFrame creation
- ✅ 3,073 successful county matches
- ✅ 100% geometry validation
- ✅ Complete spatial coverage

### File System Compatibility
**Challenge**: Read-only environments and permission issues
**Solution**: Home directory file management
```python
zhvi_file = os.path.expanduser("~/zillow_home_value_index_by_county.csv")
county_geojson = os.path.expanduser("~/county.geojson")
```

## 📊 Data Specifications

### Zillow Home Value Index
- **Source**: Zillow Research
- **Temporal Coverage**: Monthly data through October 2024
- **Spatial Resolution**: US counties (3,073 records)
- **Value Type**: Median home values in USD

### US County Boundaries
- **Source**: US Census Bureau via OpenGeo
- **Format**: GeoJSON with polygon geometries
- **Attributes**: County names, FIPS codes, area measurements
- **Coordinate System**: WGS84 (EPSG:4326)

## 🎯 Visualization Features

### 2D Choropleth Map
- **Color Scheme**: Sequential Blues palette
- **Interactive Features**: Zoom, pan, hover tooltips
- **Legend**: Automatic value classification
- **Performance**: Optimized for 3,000+ polygons

### 3D Extruded Map
- **Height Encoding**: Home values mapped to polygon extrusion
- **Viewing Angle**: 60-degree pitch for optimal perspective
- **Navigation**: 3D rotation, zoom, and pan
- **Performance**: Hardware-accelerated rendering via WebGL

## 🔮 Future Enhancements

### PDFM Integration
- **Place Embeddings**: High-dimensional feature vectors for each county
- **Machine Learning**: Regression models for value prediction
- **Feature Engineering**: Combining spatial and embedding features

### Advanced Analytics
- **Temporal Analysis**: Time series prediction of home values
- **Spatial Autocorrelation**: Neighborhood effects modeling
- **Market Segmentation**: Clustering analysis of similar counties

### Enhanced Visualizations
- **Multi-temporal Maps**: Animation of value changes over time
- **Comparative Views**: Side-by-side regional analysis
- **Custom Styling**: User-defined color schemes and extrusion factors

## 💡 Use Cases

This project framework supports various applications:

- **Real Estate Analysis**: Market trend identification and valuation
- **Urban Planning**: Development impact assessment
- **Investment Research**: Geographic portfolio optimization
- **Academic Research**: Spatial economics and housing studies
- **Data Journalism**: Interactive storytelling with housing data

## 🤝 Contributing

Contributions are welcome! Areas for improvement:
- Additional data sources integration
- Advanced 3D visualization techniques
- Machine learning model development
- Performance optimization
- Documentation enhancement

## 📄 License

This project is open-source and available under the MIT License.

## 🏠 About

Created for geospatial analysis and real estate visualization using cutting-edge 3D mapping technologies. This project demonstrates the power of combining traditional GIS data with modern web-based visualization tools to create compelling and informative spatial narratives.

---

*Transforming housing data into interactive 3D experiences for better spatial understanding and decision-making.*
