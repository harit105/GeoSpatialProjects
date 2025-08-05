# Crop Land Cover Classification and Legend Creation

A comprehensive tutorial for creating interactive legends for crop and land cover classification using leafmap and various geospatial datasets.

## 📋 Overview

This project demonstrates how to create, customize, and export interactive legends for geospatial land cover data, with a focus on crop classification mapping. The notebook showcases various legend types using NLCD (National Land Cover Database) and ESA WorldCover datasets.

## 🎯 Objectives

- Create interactive, draggable legends for land cover classification
- Demonstrate built-in legend functionality for popular datasets
- Show custom legend creation for specialized classification schemes
- Export legends as standalone HTML files
- Implement styling and positioning options for legends
- Create split-view maps with multiple legends

## 🗂️ Project Structure

```
CropClassificationMapping/
├── CropLandCover.ipynb     # Main tutorial notebook
├── README.md               # This file
└── Generated Files/
    ├── NLCD_legend.html    # Exported NLCD legend
    └── ESA_legend.html     # Exported ESA legend
```

## 📚 What's Included

### 1. Built-in Legend Creation
- **NLCD (National Land Cover Database)** legends
- **ESA WorldCover 2021** legends
- Draggable and non-draggable options
- Position customization

### 2. Custom Legend Development
The notebook includes a custom legend for ESA land cover types:
- 🌳 Trees (10)
- 🌾 Shrubland (20)
- 🌱 Grassland (30)
- 🚜 Cropland (40)
- 🏘️ Built-up (50)
- 🏜️ Barren/sparse vegetation (60)
- ❄️ Snow and ice (70)
- 💧 Open water (80)
- 🌿 Herbaceous wetland (90)
- 🌴 Mangroves (95)
- 🍃 Moss and lichen (100)

### 3. Advanced Features
- **Split-view mapping** with dual legends
- **Custom styling** with CSS parameters
- **HTML export functionality** for standalone use
- **Interactive widgets** for Jupyter environments

## 🛠️ Technologies Used

- **leafmap**: Primary mapping and legend creation library
- **Python**: Core programming language
- **Jupyter Notebook**: Development environment
- **Folium**: Underlying web mapping library
- **HTML/CSS**: Legend styling and export

## 🚀 Getting Started

### Prerequisites
```bash
pip install leafmap
```

### Running the Notebook
1. Clone this repository
2. Open `CropLandCover.ipynb` in Jupyter Notebook/Lab
3. Run cells sequentially to see legend creation examples
4. Exported legends will be saved to your home directory

## 💡 Key Features Demonstrated

### Legend Types
- **Built-in Legends**: Pre-configured for popular datasets
- **Custom Legends**: User-defined classification schemes
- **Styled Legends**: Custom CSS styling options

### Export Options
- **HTML Files**: Standalone legend files for web use
- **Widget Display**: Interactive legends within Jupyter
- **Map Integration**: Legends embedded in interactive maps

### Positioning & Styling
- Multiple position options (topright, bottomleft, etc.)
- Custom CSS styling (borders, backgrounds, fonts)
- Draggable functionality for user interaction

## 🔧 Troubleshooting

### Common Issues

**Read-only File System Error**
```python
# Solution: Save to home directory instead of current directory
output_path = os.path.expanduser("~/legend_file.html")
```

**Widget Display Issues**
```python
# Close widgets properly to avoid conflicts
try:
    widget.close()
except:
    pass
```

## 📈 Use Cases

This project is ideal for:
- **Agricultural Monitoring**: Crop type classification and mapping
- **Land Use Planning**: Urban and rural development analysis
- **Environmental Studies**: Ecosystem and habitat mapping
- **Remote Sensing Applications**: Satellite data visualization
- **Web Development**: Interactive map legend integration

## 🔗 Dataset Information

### NLCD (National Land Cover Database)
- **Source**: USGS
- **Coverage**: Continental United States
- **Resolution**: 30-meter
- **Classes**: 16 land cover types including multiple crop categories

### ESA WorldCover
- **Source**: European Space Agency
- **Coverage**: Global
- **Resolution**: 10-meter
- **Classes**: 11 land cover types including cropland classification

## 📝 Notes

- All exported HTML files are saved to the user's home directory to avoid file system permission issues
- The notebook includes both interactive and static legend examples
- Custom legends can be easily modified by updating the `legend_dict` dictionary
- Split-view functionality requires `draggable=False` for proper display

## 🤝 Contributing

Feel free to contribute by:
- Adding new legend types
- Improving styling options
- Including additional datasets
- Enhancing documentation

## 📄 License

This project is open-source and available under the MIT License.

---

## Credits - Qiusheng Wu

*Created for geospatial analysis and crop classification mapping using Python and leafmap.*
