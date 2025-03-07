# README: Sentinel-1 & Sentinel-2 Classification Project

## Project Overview
This project focuses on processing, analyzing, and classifying satellite imagery from Sentinel-1 (SAR) and Sentinel-2 (optical) to study land cover types in the Velondriake region. The classification utilizes Random Forest models trained on combined Sentinel-1 and Sentinel-2 data to distinguish various land cover classes, such as mangrove forests, terrestrial vegetation, barren land, and water bodies.

## Data Sources
- **Sentinel-1**: SAR data (VV & VH polarizations)
- **Sentinel-2**: Multispectral bands (B2, B3, B4, B5, B6, B7, B8, B11, B12, B8A)
- **Ancillary Data**: Training and validation polygons

## Preprocessing Steps
1. **Resampling Sentinel-1 Data**: Sentinel-1 imagery was resampled to match the spatial resolution of Sentinel-2.
2. **Cloud Masking**: Cloud-affected pixels were identified using Sentinel-2 cloud probability layers and masked from the dataset.
3. **Angle Correction**: Sentinel-1 data was corrected for incidence angle effects to improve classification accuracy.
4. **Feature Calculation**: Vegetation and water indices such as NDVI, MNDWI, SAVI, and custom indices were computed.
5. **Data Extraction**: Training and validation samples were extracted using reference polygons, ensuring that NaN (cloud-masked) pixels were excluded.

## Model Training & Feature Importance
- A **Random Forest classifier** was trained separately on Sentinel-2 and Sentinel-1+Sentinel-2 datasets.
- Feature importance analysis revealed key spectral bands and indices contributing to classification accuracy.

## Classification & Output
- The trained model was applied to the full study area to generate a classified raster.
- The output raster was saved as a GeoTIFF file with class values:
  1. Closed-Canopy Mangrove
  2. Open-Canopy Mangrove I
  3. Open-Canopy Mangrove II
  5. Terrestrial Forest
  6. Other Terrestrial Vegetation
  8. Barren Exposed
  9. Residual Water

## Usage Instructions
### Prerequisites
Ensure the following Python libraries are installed:
- `rasterio`
- `geopandas`
- `shapely`
- `numpy`
- `matplotlib`
- `scikit-learn`

### Running the Pipeline
1. Place Sentinel-1 and Sentinel-2 raster files in the project directory.
2. Ensure training and validation shapefiles are available.
3. Run the preprocessing script to align and mask the data.
4. Train the classifier using the training dataset.
5. Apply the trained model to classify the study area.
6. Export the classified raster for visualization in GIS software (e.g., ArcGIS, QGIS).

## Potential Issues & Solutions
- **Cloud Contamination in Training Data**: Mask NaN values before model training.
- **Mismatched Spatial Resolutions**: Ensure all datasets are resampled to a common resolution.
- **Angle Effects in Sentinel-1**: Apply incidence angle normalization for better classification results.

## Future Improvements
- Integration of additional SAR-derived features (e.g., texture analysis).
- Experimentation with deep learning models for improved classification.
- Multi-temporal analysis to monitor changes over time.

## Contact
For questions or contributions, please contact: [Your Name / Email]
