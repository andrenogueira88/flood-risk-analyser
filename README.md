# Flood Risk Analyzer

A QGIS plugin for flood risk classification and analysis using machine learning-based feature importance analysis techniques.

![QGIS Plugin](https://img.shields.io/badge/QGIS-Plugin-green)
![Python](https://img.shields.io/badge/Python-3.x-blue)
![License](https://img.shields.io/badge/License-GPL%20v2-blue)

## Overview

The Flood Risk Analyzer is a comprehensive QGIS plugin designed to help researchers, urban planners, and environmental scientists analyze flood risk patterns using multiple geospatial datasets. The plugin processes various raster layers (elevation, precipitation, land cover, etc.) and applies advanced machine learning techniques to identify and rank the importance of all features for flood risk prediction.

## Features

### 🗂️ Multi-Format Data Support
- **Raster Files**: TIF, IMG formats
- **Vector Files**: SHP format
- **Data Types**: Continuous, Categorical, Binary, and Target variables

### 🔍 Advanced Feature Importance Methods
- **ANOVA F Test**: Statistical significance testing for continuous features
- **Mutual Information**: Captures non-linear relationships between features
- **Random Forest Importance**: Ensemble-based feature ranking with impurity measures
- **Permutation Importance**: Model-agnostic importance based on performance impact
- **L1 Regularization (LASSO)**: Coefficient-based linear feature importance

### 📊 Comprehensive Analytics
- Descriptive statistics for continuous variables
- Categorical feature distribution analysis
- Target class balance visualization
- Complete feature importance ranking for all input features

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

### Step 3: Feature Importance Analysis

1. **Select Method**
   - Choose from 5 available feature importance methods
   - Each method has specific strengths for different data types and relationships

2. **Apply Feature Importance Analysis**
   - Click the method button to execute the analysis
   - Results display all features ranked by importance scores
   - Complete ranking provided for all input features

3. **Interpret Results**
   - Review feature importance rankings (1 = most important)
   - Identify key predictors of flood risk across all features
   - Compare results across different methods for robust insights

## Method Descriptions

| Method | Best For | Characteristics | Output Interpretation |
|--------|----------|----------------|---------------------|
| **ANOVA F Test** | Continuous features | Fast, statistical significance | Higher F-scores = more important |
| **Mutual Information** | Non-linear relationships | Captures complex dependencies | Higher MI scores = stronger relationships |
| **Random Forest** | Feature interactions | Handles mixed data types | Normalized importance (0-1) |
| **Permutation Importance** | Model-agnostic analysis | Performance-based importance | Mean decrease in accuracy |
| **L1 Regularization** | Linear relationships | Coefficient magnitude | Absolute coefficient values |

## Key Features (Version 1.1+)

### Complete Feature Ranking
- **No Selection Limits**: All input features receive importance scores and rankings
- **Comprehensive Analysis**: Every feature is evaluated regardless of dataset size
- **Method-Specific Scoring**: Each algorithm provides interpretable importance measures
- **Robust Comparisons**: Compare feature rankings across multiple methods

### Enhanced Methods
- **Added Permutation Importance**: New model-agnostic method for robust importance assessment
- **Improved Interpretability**: Method-specific importance scores with clear interpretation guidelines
- **Better Performance**: Optimized algorithms for comprehensive feature analysis

## Output Files

The plugin generates several outputs:

- **`processed_data.parquet`**: Merged and processed DataFrame with all features
- **Feature importance rankings**: Complete ranking of all features displayed in interface
- **Statistical summaries**: Comprehensive statistics available in the statistics tabs

## Technical Details

### Data Processing Pipeline

1. **Raster Loading**: Uses QGIS API to load and validate raster layers
2. **Coordinate Alignment**: Ensures all layers share the same CRS and resolution
3. **Data Extraction**: Converts raster pixels to tabular format with coordinates
4. **Feature Engineering**: Applies appropriate encoding based on data types
5. **Quality Control**: Handles NoData values and validates data integrity

### Feature Importance Implementation

The plugin implements scikit-learn's feature importance methods optimized for geospatial data:

- **Comprehensive Analysis**: All features analyzed using `k='all'` parameter
- **Preprocessing**: Automatic handling of missing values and data scaling
- **Robust Scoring**: Multiple algorithms provide different perspectives on feature importance
- **Class Balancing**: Addresses imbalanced target distributions across all methods

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

**Unexpected importance rankings**
- Try multiple methods to identify consistently important features
- Consider data quality and preprocessing effects
- Validate results against domain knowledge

### Performance Tips

- Use smaller study areas for initial testing
- Consider resampling high-resolution data if processing is slow
- Ensure adequate system memory for large datasets
- Permutation Importance is computationally intensive - use for final analysis

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
Sousa, A.N. (2025). Flood Risk Analyzer: QGIS Plugin for Flood Risk Classification 
Using Machine Learning Feature Importance Analysis. Version 1.1. 
https://github.com/[your-repo]/flood-risk-analyzer
```

## Acknowledgments

- Built using the QGIS Plugin Builder
- Utilizes scikit-learn for machine learning functionality
- Thanks to the QGIS development community for excellent documentation
- Prof. Rogerio Negri - INPE-BR
- Prof. Leonardo Bacelar - INPE-BR
