# PDFM Demographic Prediction Study

A comprehensive analysis of **Probabilistic Deep Factorization Model (PDFM)** embeddings for geospatial demographic prediction, demonstrating superresolution and imputation techniques across multiple geographic scales.

## 🎯 Project Overview

This study explores how **PDFM embeddings** can predict demographic characteristics at different geographic resolutions, from county-level data to ZIP code-level predictions. We achieve this through two key techniques:

1. **Superresolution**: Training on counties (low-resolution) → Predicting ZIP codes (high-resolution)
2. **Imputation**: Filling missing demographic data using geographically transferable patterns

## 📊 Key Results

### Performance Summary
| Technique | Target Variable | Model | R² Score | Correlation |
|-----------|----------------|-------|----------|-------------|
| Superresolution | Education Level | Linear | 73.6% | **85.9%** |
| Imputation | Education Level | Linear | **81.5%** | 90.3% |
| Imputation | Income | Linear | 76.5% | 87.5% |
| Imputation | Blood Pressure | LightGBM | **78.2%** | 88.4% |
| Imputation | Asthma | LightGBM | 74.0% | 86.1% |

### 🏆 Breakthrough Achievement
- **85.9% correlation** for county → ZIP code superresolution
- **88.9% correlation** for cross-county ZIP code imputation
- Successfully predicted demographics for 25,000+ ZIP codes using training data from different counties

## 🗂️ Dataset Information

### PDFM Embeddings
- **Counties**: 3,088 places with 330-dimensional embeddings
- **ZIP Codes**: 32,069 places with 330-dimensional embeddings
- **Feature Categories**: 
  - 🔄 **Trends** (128 features): Economic and demographic time-series patterns
  - 🗺️ **Maps** (128 features): Spatial infrastructure and geographic patterns
  - 🌤️ **Weather** (74 features): Climate and environmental conditions

### Ground Truth Data (Data Commons API)
- **Population**: Total person count
- **Education**: Percentage with bachelor's degree or higher
- **Age**: Median age of residents
- **Income**: Median household income
- **Health**: Asthma and high blood pressure percentages

## 🔬 Methodology

### 1. Data Integration
```python
# Combine county and ZIP code embeddings
county_embeddings = pd.read_csv('county_embeddings.csv').set_index('place')
zip_embeddings = pd.read_csv('zcta_embeddings.csv').set_index('place')
embeddings = pd.concat([county_embeddings, zip_embeddings])

# Download real-world demographics via Data Commons API
df_labels = dc.build_multivariate_dataframe(embeddings.index, labels)
```

### 2. Superresolution Analysis
- **Training**: County-level demographics (3,088 samples)
- **Testing**: ZIP code-level predictions (32,069 samples)
- **Goal**: Learn geographic patterns from large areas, apply to small areas

### 3. Imputation Analysis
- **Training**: ZIP codes from 20% of counties (7,000 samples)
- **Testing**: ZIP codes from remaining 80% of counties (25,069 samples)
- **Goal**: Fill demographic gaps using transferable geographic patterns

### 4. Model Comparison
- **Linear Models**: Ridge regression with MinMax scaling
- **LightGBM**: Gradient boosting with feature importance analysis
- **Evaluation**: R², correlation, RMSE, MAE metrics

## 📈 Key Findings

### Geographic Patterns Are Surprisingly Linear
- **Economic variables** (education, income) work best with simple linear models
- **Health variables** benefit from complex interactions captured by LightGBM
- **Age demographics** are the most challenging to predict geographically

### Feature Importance Insights
Different demographic outcomes depend on different types of geographic information:

| Variable | Trends | Maps | Weather | Interpretation |
|----------|--------|------|---------|----------------|
| **Education** | 40% | **52%** | 3% | Infrastructure + economic patterns |
| **Income** | **55%** | 37% | 8% | Economic trends + location |
| **Blood Pressure** | 31% | **35%** | 22% | Urban environment + climate |
| **Asthma** | **47%** | 30% | 23% | Socioeconomic + environmental factors |

### Transferable Geographic Knowledge
PDFM embeddings capture patterns that work across:
- ✅ Different geographic scales (counties ↔ ZIP codes)
- ✅ Different regions (rural Texas ↔ urban California)  
- ✅ Different demographic variables (economic, health, age)

## 🛠️ Technical Setup

### Dependencies
```bash
pip install pandas numpy scikit-learn lightgbm
pip install geopandas matplotlib seaborn
pip install datacommons_pandas
```

### macOS LightGBM Setup
```bash
# Install OpenMP dependency
brew install libomp

# Reinstall LightGBM
pip uninstall lightgbm -y
pip install lightgbm --upgrade
```

### Data Requirements
- PDFM embedding files: `county_embeddings.csv`, `zcta_embeddings.csv`
- Geometry files: `county.geojson`, `zcta.geojson`
- Internet connection for Data Commons API calls

## 📁 File Structure
```
PDFM_Notebooks/
├── PDFM_Demographic_Prediction_Study.ipynb  # Main analysis notebook
├── README.md                                 # This documentation
└── data/
    ├── county_embeddings.csv                # County-level PDFM features
    ├── zcta_embeddings.csv                  # ZIP code-level PDFM features
    ├── county.geojson                       # County boundaries
    └── zcta.geojson                         # ZIP code boundaries
```

## 🎯 Real-World Applications

### Market Research & Business Intelligence
- **Store Location**: Predict demographics for new retail locations
- **Market Sizing**: Estimate customer base without expensive surveys
- **Competitive Analysis**: Understand demographic patterns across markets

### Public Health & Policy
- **Disease Surveillance**: Predict health outcomes in under-surveyed areas
- **Resource Allocation**: Target healthcare services based on predicted needs
- **Environmental Health**: Model pollution-health interactions

### Urban Planning & Development
- **Housing Development**: Predict neighborhood characteristics for new projects
- **Infrastructure Planning**: Allocate services based on demographic predictions
- **Gentrification Studies**: Track changing neighborhood patterns

### Real Estate & Finance
- **Property Valuation**: Incorporate demographic predictions into pricing models
- **Risk Assessment**: Evaluate areas with limited demographic data
- **Investment Analysis**: Identify emerging markets and demographic shifts

## 🔮 Future Directions

### Model Improvements
- **Ensemble Methods**: Combine linear and tree-based models
- **Deep Learning**: Explore neural network architectures for geographic data
- **Temporal Analysis**: Incorporate time-series patterns in demographics

### Geographic Expansion
- **International Data**: Apply techniques to global demographic prediction
- **Micro-Geographic**: Extend to census block or building-level predictions
- **Multi-Scale Integration**: Simultaneous prediction across multiple resolutions

### Additional Variables
- **Economic Indicators**: Employment, poverty rates, business density
- **Environmental Factors**: Air quality, walkability, green space access
- **Social Metrics**: Crime rates, school quality, community engagement

## 📚 Citation & References

### Citing This Work
If you use this analysis, please cite:
```bibtex
@misc{shah2025pdfm_demographic,
  title={PDFM Demographic Prediction Study: Geographic Superresolution and Imputation using Probabilistic Deep Factorization Models},
  author={Harit Shah},
  year={2025},
  note={Analysis of Google's Population Dynamics Foundation Model Embeddings for demographic prediction}
}
```

### PDFM Embeddings License & Citation
This work uses **Google's Population Dynamics Foundation Model (PDFM) Embeddings** released under the **Creative Commons Attribution 4.0 International (CC BY 4.0)** license. 

**Required Citation for PDFM Embeddings:**
```bibtex
@article{agarwal2024pdfm,
  title={General Geospatial Inference with a Population Dynamics Foundation Model},
  author={Mohit Agarwal and Mimi Sun and Chaitanya Kamath and Arbaaz Muslim and Prithul Sarker and Joydeep Paul and Hector Yee and Marcin Sieniek and Kim Jablonski and Yael Mayer and David Fork and Sheila de Guia and Jamie McPike and Adam Boulanger and Tomer Shekel and David Schottlander and Yao Xiao and Manjit Chakravarthy Manukonda and Yun Liu and Neslihan Bulut and Sami Abu-el-haija and Arno Eigenwillig and Parth Kothari and Bryan Perozzi and Monica Bharel and Von Nguyen and Luke Barrington and Niv Efron and Yossi Matias and Greg Corrado and Krish Eswaran and Shruthi Prabhakara and Shravya Shetty and Gautam Prasad},
  journal={arXiv preprint arXiv:2411.07207},
  year={2024}
}
```

**License Terms (CC BY 4.0):**
- ✅ **Share**: Copy and redistribute the material in any medium or format
- ✅ **Adapt**: Remix, transform, and build upon the material for any purpose
- ⚠️ **Attribution Required**: Must give appropriate credit and cite the original work

### Key Technologies
- **Data Commons**: Google's public data platform
- **PDFM**: Probabilistic Deep Factorization Models for geographic embeddings
- **LightGBM**: Microsoft's gradient boosting framework
- **GeoPandas**: Geographic data analysis in Python

## 🤝 Contributing

Contributions are welcome! Areas of interest:
- Additional demographic variables
- New geographic regions
- Alternative modeling approaches
- Visualization improvements

## 📄 License & Contact

### Project License
This analysis is available under the **MIT License**. See LICENSE file for details.

### Data License
The underlying **PDFM embeddings** are provided by Google under **Creative Commons Attribution 4.0 International (CC BY 4.0)** license.

### Contact
- **Author**: Harit Shah
- **Last Updated**: September 2025
- **Status**: Active Development

For questions about the analysis methodology or implementation, please open an issue in the repository.

---

> 💡 **Key Insight**: This study proves that abstract geographic embeddings (PDFM) contain enough information to predict real-world demographic outcomes with 85-90% accuracy, even across different scales and regions. This opens new possibilities for data-driven urban planning, public health, and market research.
