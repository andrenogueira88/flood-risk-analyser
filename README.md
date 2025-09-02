# Flood Risk Analyzer

A QGIS plugin for flood risk classification and analysis using machine learning-based feature selection techniques.

![QGIS Plugin](https://img.shields.io/badge/QGIS-Plugin-green)
![Python](https://img.shields.io/badge/Python-3.x-blue)
![License](https://img.shields.io/badge/License-GPL%20v2-blue)

## Overview

The Flood Risk Analyzer is a comprehensive QGIS plugin designed to help researchers, urban planners, and environmental scientists analyze flood risk patterns using multiple geospatial datasets. The plugin processes various raster layers (elevation, precipitation, land cover, etc.) and applies advanced machine learning techniques to identify the most important features for flood risk prediction.

## Features

### 🗂️ Multi-Format Data Support
- **Raster Files**: TIF, IMG formats
- **Vector Files**: SHP format
- **Data Types**: Continuous, Categorical, Binary, and Target variables

### 🔍 Advanced Feature Selection Methods
- **ANOVA F Test**: Statistical significance testing for continuous features
- **Mutual Information**: Captures non-linear relationships between features
- **Random Forest Importance**: Ensemble-based feature ranking
- **Recursive Feature Elimination (RFE)**: Iterative backward feature selection
- **L1 Regularization (LASSO)**: Automatic sparse feature selection

### 📊 Comprehensive Analytics
- Descriptive statistics for continuous variables
- Categorical feature distribution analysis
- Target class balance visualization
- Feature importance ranking and selection

### 💾 Data Processing & Export
- Automated raster-to-DataFrame conversion
- Spatial coordinate preservation
- Missing data handling
- Parquet format export for processed data

## Installation

### Prerequisites
- QGIS 3.x
- Python 3.x with the following packages:
  ```
  pandas
  numpy
  scikit-learn
  osgeo (GDAL)
  ```

### Plugin Installation
1. Download the plugin files
2. Copy the plugin folder to your QGIS plugins directory:
   - **Windows**: `C:\Users\[username]\AppData\Roaming\QGIS\QGIS3\profiles\default\python\plugins\`
   - **macOS**: `~/Library/Application Support/QGIS/QGIS3/profiles/default/python/plugins/`
   - **Linux**: `~/.local/share/QGIS/QGIS3/profiles/default/python/plugins/`
3. Restart QGIS
4. Enable the plugin in `Plugins > Manage and Install Plugins > Installed`

## Usage

### Step 1: Data Loading and Configuration

1. **Launch the Plugin**
   - Navigate to `Plugins > Flood Risk Identifier > FloodRisk Analyzer`

2. **Add Input Files**
   - Click `Add File` to select raster or vector files
   - Assign appropriate data types to each file:
     - **Continuous**: Elevation, precipitation, temperature data
     - **Categorical**: Land use classes, soil types
     - **Binary**: Urban/rural, water/no-water
     - **Target**: Flood occurrence (exactly one required)

3. **Remove Unwanted Files**
   - Select files in the list and click `Remove File` if needed

### Step 2: Data Processing

1. **Process DataFrame**
   - Click `Process DataFrame` to merge all raster layers
   - The plugin automatically:
     - Validates CRS and resolution consistency
     - Converts rasters to aligned DataFrames
     - Applies one-hot encoding for categorical data
     - Handles missing values appropriately

2. **Review Statistics**
   - Check the statistics tables for data quality
   - Verify continuous feature distributions
   - Examine categorical feature counts
   - Assess target class balance

### Step 3: Feature Selection

1. **Select Method**
   - Choose from 5 available feature selection methods
   - Each method has specific strengths for different data types

2. **Apply Feature Selection**
   - Click the method button to execute feature selection
   - Results display ranked features with importance scores
   - Selected features are marked for easy identification

3. **Interpret Results**
   - Review feature importance rankings
   - Identify key predictors of flood risk
   - Use selected features for subsequent modeling

## Method Descriptions

| Method | Best For | Characteristics |
|--------|----------|----------------|
| **ANOVA F Test** | Continuous features | Fast, assumes linear relationships |
| **Mutual Information** | Mixed data types | Captures non-linear patterns |
| **Random Forest** | Complex interactions | Handles feature interactions well |
| **RFE** | Optimal subset | Iterative, computationally intensive |
| **L1 Regularization** | Sparse solutions | Automatic feature elimination |

## Output Files

The plugin generates several outputs:

- **`processed_data.parquet`**: Merged and processed DataFrame
- **Feature importance rankings**: Displayed in the plugin interface
- **Statistical summaries**: Available in the statistics tabs

## Technical Details

### Data Processing Pipeline

1. **Raster Loading**: Uses QGIS API to load and validate raster layers
2. **Coordinate Alignment**: Ensures all layers share the same CRS and resolution
3. **Data Extraction**: Converts raster pixels to tabular format with coordinates
4. **Feature Engineering**: Applies appropriate encoding based on data types
5. **Quality Control**: Handles NoData values and validates data integrity

### Feature Selection Implementation

The plugin implements scikit-learn's feature selection methods with optimizations for geospatial data:

- **Preprocessing**: Automatic handling of missing values
- **Scaling**: Applied when necessary for specific methods
- **Cross-validation**: Built-in validation for robust results
- **Class Balancing**: Addresses imbalanced target distributions

## Troubleshooting

### Common Issues

**Error: "Exactly one target file must be specified"**
- Ensure you have designated exactly one file as "Target" type

**Error: "CRS mismatch between layers"**
- Reproject all input layers to the same coordinate reference system

**Error: "Resolution mismatch between layers"**
- Resample layers to the same pixel resolution using QGIS tools

**Error: "No valid data after removing NaN values"**
- Check for excessive missing data in input layers
- Consider using interpolation to fill gaps

### Performance Tips

- Use smaller study areas for initial testing
- Consider resampling high-resolution data if processing is slow
- Ensure adequate system memory for large datasets

## Contributing

Contributions are welcome! Please feel free to submit issues, feature requests, or pull requests.

### Development Setup

1. Clone the repository
2. Set up a QGIS development environment
3. Install required Python dependencies
4. Follow QGIS plugin development guidelines

## License

This program is free software; you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation; either version 2 of the License, or (at your option) any later version.

## Author

**Andre Nogueira Sousa**  
Email: andrenogsousa@gmail.com

## Citation

If you use this plugin in your research, please cite:

```
Sousa, A.N. (2025). Flood Risk Analyzer: QGIS Plugin for Flood Risk Classification. 
QGIS Plugin Repository. https://github.com/[your-repo]/flood-risk-analyzer
```

## Acknowledgments

- Built using the QGIS Plugin Builder
- Utilizes scikit-learn for machine learning functionality
- Thanks to the QGIS development community for excellent documentation
