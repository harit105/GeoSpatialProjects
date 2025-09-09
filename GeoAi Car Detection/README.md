# Car Detection Using GeoAI

This project demonstrates how to train a deep learning model for detecting cars in satellite/aerial imagery using the `geoai-py` library. The project implements a complete machine learning pipeline from data preparation to model inference and visualization.

## Overview

The project uses a Mask R-CNN model to detect cars in high-resolution geospatial imagery. The workflow includes:

1. **Data Loading**: Download training and test datasets from HuggingFace
2. **Data Visualization**: Interactive visualization of training data and imagery
3. **Data Preprocessing**: Create training tiles from raster and vector data
4. **Model Training**: Train a Mask R-CNN model for object detection
5. **Inference**: Run predictions on test imagery
6. **Post-processing**: Vectorize detection masks and create final outputs
7. **Visualization**: Interactive maps and split-view comparisons

## Dataset

The project uses publicly available datasets hosted on HuggingFace:

- **Training Raster**: High-resolution 7cm aerial imagery (`cars_7cm.tif`)
- **Training Labels**: Car detection annotations in GeoJSON format (`car_detection.geojson`)
- **Test Raster**: Test imagery for model evaluation (`cars_test_7cm.tif`)

## Project Structure

```
├── train_car_detection.ipynb    # Main notebook with complete workflow
├── output/                      # Generated during training
│   ├── images/                  # Training image tiles
│   ├── labels/                  # Training label tiles
│   └── models/                  # Trained model files
├── cars_prediction.tif          # Model prediction masks
├── cars_prediction.geojson      # Vectorized car detections
└── README.md                    # This file
```

## Requirements

- Python 3.7+
- geoai-py library
- CUDA-compatible GPU (recommended for training)

## Installation

```bash
pip install geoai-py
```

## Usage

### 1. Data Download and Visualization

The notebook starts by downloading the required datasets and visualizing the training data:

```python
import geoai

# Download datasets
train_raster_path = geoai.download_file(train_raster_url)
train_vector_path = geoai.download_file(train_vector_url)
test_raster_path = geoai.download_file(test_raster_url)

# Visualize training data
geoai.view_vector_interactive(train_vector_path, tiles=train_raster_url)
```

### 2. Training Data Preparation

Creates training tiles from the raster imagery and vector labels:

```python
out_folder = "output"
tiles = geoai.export_geotiff_tiles(
    in_raster=train_raster_path,
    out_folder=out_folder,
    in_class_data=train_vector_path,
    tile_size=512,
    stride=256,
    buffer_radius=0,
)
```

### 3. Model Training

Trains a Mask R-CNN model with the following configuration:

```python
geoai.train_MaskRCNN_model(
    images_dir=f"{out_folder}/images",
    labels_dir=f"{out_folder}/labels",
    output_dir=f"{out_folder}/models",
    num_channels=3,
    pretrained=True,
    batch_size=4,
    num_epochs=100,
    learning_rate=0.005,
    val_split=0.2,
)
```

### 4. Model Inference

Runs the trained model on test imagery:

```python
geoai.object_detection(
    test_raster_path,
    masks_path,
    model_path,
    window_size=512,
    overlap=256,
    confidence_threshold=0.5,
    batch_size=4,
    num_channels=3,
)
```

### 5. Post-processing and Visualization

Converts detection masks to vector format and creates interactive visualizations:

```python
# Vectorize detections
gdf = geoai.orthogonalize(masks_path, output_path, epsilon=2)

# Create interactive visualizations
geoai.view_vector_interactive(output_path, tiles=test_raster_url)
geoai.create_split_map(
    left_layer=output_path,
    right_layer=test_raster_url,
    left_args={"style": {"color": "red", "fillOpacity": 0.2}},
    basemap=test_raster_url,
)
```

## Key Features

- **Automated Data Pipeline**: Complete workflow from raw data to final predictions
- **High-Resolution Processing**: Works with 7cm resolution aerial imagery
- **Interactive Visualizations**: Web-based maps for data exploration and results
- **Configurable Training**: Adjustable hyperparameters for model optimization
- **Vector Output**: Generates GeoJSON files compatible with GIS software
- **Split-view Comparisons**: Side-by-side visualization of predictions and imagery

## Model Configuration

- **Architecture**: Mask R-CNN with pretrained backbone
- **Input Channels**: 3 (RGB imagery)
- **Tile Size**: 512x512 pixels
- **Overlap**: 256 pixels
- **Batch Size**: 4
- **Epochs**: 100
- **Learning Rate**: 0.005
- **Validation Split**: 20%

## Output Files

- `cars_prediction.tif`: Raster masks of detected cars
- `cars_prediction.geojson`: Vector polygons of car detections
- `output/models/best_model.pth`: Trained model weights

## Applications

This workflow can be adapted for various geospatial object detection tasks:

- Vehicle counting and traffic analysis
- Infrastructure monitoring
- Urban planning and development
- Environmental monitoring
- Disaster response and damage assessment
## Results

The trained model successfully detects cars in aerial imagery with configurable confidence thresholds. The final output includes both raster masks and vector polygons suitable for further GIS analysis.

## License

This project uses publicly available datasets and the open-source geoai-py library. 

## Acknowledgments

- Dataset provided by [giswqs/geospatial](https://huggingface.co/datasets/giswqs/geospatial) on HuggingFace
- Built using the [geoai-py](https://github.com/opengeos/geoai) library
