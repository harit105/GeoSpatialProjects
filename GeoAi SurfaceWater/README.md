# Surface Water Detection using GeoAI

This project demonstrates how to train and deploy a deep learning model for detecting surface water bodies from satellite imagery using the `geoai-py` library. The workflow includes data preparation, model training, inference, and visualization of results.

## Project Overview

The project uses NAIP (National Agriculture Imagery Program) imagery to train a Mask R-CNN model for surface water detection. The trained model can then be used to identify and map water bodies in new satellite images.

## Dataset

The project uses the following datasets from Hugging Face:
- **Training Raster**: NAIP imagery for training (`naip_water_train.tif`)
- **Training Masks**: Ground truth water masks (`naip_water_masks.tif`)
- **Test Raster**: NAIP imagery for testing/inference (`naip_water_test.tif`)

## Workflow

### 1. Data Download and Exploration
- Downloads training and test datasets from Hugging Face
- Explores raster properties and visualizes the data
- Displays training masks overlaid on satellite imagery

### 2. Training Data Preparation
- Exports GeoTIFF tiles from the training raster and masks
- Creates 512x512 pixel tiles with 128-pixel stride
- Organizes data into appropriate folder structure for model training

### 3. Model Training
- Trains a Mask R-CNN model for object detection
- Uses 4-channel imagery (RGB + NIR)
- Configuration:
  - Batch size: 4
  - Epochs: 10
  - Learning rate: 0.005
  - Validation split: 20%
  - Uses pretrained weights for transfer learning

### 4. Inference
- Applies the trained model to test imagery
- Uses sliding window approach with:
  - Window size: 512x512 pixels
  - Overlap: 128 pixels
  - Confidence threshold: 0.3
- Generates water detection masks

### 5. Post-processing and Vectorization
- Converts raster masks to vector polygons (GeoJSON format)
- Applies filtering based on:
  - Minimum area: 1000 square units
  - Simplification tolerance: 1 unit
- Adds geometric properties (including elongation ratio)
- Filters out elongated features (elongation < 10) to focus on water bodies

### 6. Visualization and Results
- Creates interactive maps showing detected water bodies
- Generates split-screen comparisons between original imagery and detections
- Provides statistical analysis of detected features

## Key Features

- **Multi-spectral Analysis**: Utilizes 4-channel imagery (RGB + Near-Infrared)
- **Deep Learning**: Implements Mask R-CNN for precise water body detection
- **Geospatial Processing**: Handles large-scale satellite imagery with tiling
- **Interactive Visualization**: Creates web-based maps for result exploration
- **Quality Filtering**: Applies geometric constraints to improve detection accuracy

## Requirements

```bash
pip install geoai-py
```

## File Structure

```
GeoAi SurfaceWater/
├── train_water_detection.ipynb    # Main notebook
├── README.md                      # This file
├── output/                        # Generated training data and models
│   ├── images/                    # Training image tiles
│   ├── labels/                    # Training mask tiles  
│   └── models/                    # Trained model files
├── naip_water_prediction.tif      # Inference results (raster)
└── naip_water_prediction.geojson  # Vectorized water bodies
```

## Usage

1. Open the Jupyter notebook `train_water_detection.ipynb`
2. Run all cells sequentially to:
   - Download and explore the dataset
   - Prepare training data
   - Train the Mask R-CNN model
   - Run inference on test data
   - Visualize results

## Results

The model successfully identifies surface water bodies in satellite imagery with the following characteristics:
- Accurate detection of lakes, ponds, and rivers
- Filtering of false positives using geometric properties
- Interactive visualization for result validation
- Export to standard geospatial formats (GeoJSON)

## Applications

This workflow can be applied to:
- Environmental monitoring
- Water resource management
- Flood mapping and assessment
- Land use classification
- Climate change studies

## Technical Details

- **Model Architecture**: Mask R-CNN with ResNet backbone
- **Input Resolution**: 512x512 pixels per tile
- **Spectral Bands**: Red, Green, Blue, Near-Infrared
- **Output Format**: Binary masks and vector polygons
- **Coordinate System**: Preserves original raster CRS

## Future Improvements

- Experiment with different model architectures (U-Net, DeepLab)
- Incorporate temporal analysis for change detection
- Add water quality assessment capabilities
- Optimize model for real-time processing
- Include additional spectral indices (NDWI, MNDWI)
