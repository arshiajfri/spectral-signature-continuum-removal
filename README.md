# Spectral Signature Continuum Removal

## Overview

This project implements an object-oriented approach for **continuum removal** of spectral signatures using the **convex hull method**. The goal is to remove the continuum (baseline) from spectral data to enhance the detection and analysis of absorption features.

## What is Continuum Removal?

Continuum removal is a preprocessing technique used in spectroscopy and remote sensing to normalize spectral signatures. It helps to:
- Remove the spectral continuum (baseline) effects
- Enhance absorption features
- Facilitate mineral identification and classification
- Improve spectral matching and comparison

The convex hull method computes the upper envelope of the spectral signature and removes it from the original spectrum.

## Project Structure

```
Spectral Signature Continuum Removal/
├── README.md                           # This file
├── continuum_removal/                  # ContinuumRemoval module directory
│   ├── continuum_removal.py           # Main ContinuumRemoval class module
│   └── Main.ipynb                     # Module notebook sample usage
├── Data/                               # Data directory
│   ├── groundTruth_Cuprite_end12/      # Ground truth data directory
│   │   ├── groundTruth_Cuprite_nEnd12.mat  # Spectral data file
│   │   ├── #1 Alunite_m.jpg           # Reference images
│   │   ├── #2 Andradite_m.jpg
│   │   └── ... (other mineral samples)
```

## Requirements

### Python Packages

```bash
numpy>=1.20.0
scipy>=1.7.0
matplotlib>=3.3.0
jupyter>=1.0.0
```

### Installation

```bash
pip install numpy scipy matplotlib jupyter
```

## Features

### ContinuumRemoval Class

A reusable Python class that performs continuum removal using the convex hull method.

**Key Methods:**
- `compute_convex_hull()`: Computes the convex hull continuum for the spectral signature
- `compute_continuum_removed()`: Computes the continuum-removed spectrum
- `plot_analysis(title)`: Visualizes the analysis in three subplots

**Attributes:**
- `wavelength`: Array of wavelength values
- `spectral_signature`: Original spectral reflectance values
- `convex_hull`: Computed convex hull continuum
- `convex_points`: Points defining the convex hull
- `continuum_removed`: Final continuum-removed spectrum

## Usage

### Basic Usage

```python
from continuum_removal import ContinuumRemoval
import numpy as np

# Example spectral data
wavelength = np.array([400, 500, 600, 700, 800, 900, 1000])  # nm
spectral_signature = np.array([0.5, 0.6, 0.45, 0.7, 0.55, 0.8, 0.6])

# Create ContinuumRemoval instance
continuum_removal = ContinuumRemoval(wavelength, spectral_signature)

# Compute and plot results
continuum_removal.plot_analysis(title="Sample Spectrum")
```

### Working with Real Data

```python
from scipy.io import loadmat
from continuum_removal import ContinuumRemoval

# Load ground truth data
GT = loadmat("Data/groundTruth_Cuprite_end12/groundTruth_Cuprite_nEnd12.mat")
wavelength = np.squeeze(GT["waveLength"])
M = GT["M"]  # Spectral signatures matrix

# Process each spectral sample
for i in range(M.shape[1]):
    spectral_signature = M[:, i]
    
    # Create ContinuumRemoval instance
    continuum_removal = ContinuumRemoval(wavelength, spectral_signature)
    
    # Get coordinate name for the title
    title = f"Spectrum of {GT['cood'][i][0][0]}"
    
    # Compute and plot continuum removal results
    continuum_removal.plot_analysis(title=title)
```

### Accessing Results Programmatically

```python
# Create instance
continuum_removal = ContinuumRemoval(wavelength, spectral_signature)

# Compute continuum removal
continuum_removal.compute_continuum_removed()

# Access results
original_spectrum = continuum_removal.spectral_signature
convex_hull = continuum_removal.convex_hull
continuum_removed = continuum_removal.continuum_removed

print(f"Original spectrum shape: {original_spectrum.shape}")
print(f"Continuum removed shape: {continuum_removed.shape}")
```

## Methodology

### Convex Hull Computation

1. **Point Construction**: Create 2D points from wavelength and reflectance pairs
2. **Hull Computation**: Calculate convex hull using scipy's ConvexHull algorithm
3. **Point Extraction**: Extract vertices of the convex hull
4. **Deduplication**: Remove duplicate points
5. **Interpolation**: Interpolate hull points to original wavelength grid

### Continuum Removal

The continuum-removed spectrum is computed as:
```
continuum_removed = spectral_signature - convex_hull
```

## Visualization

The `plot_analysis()` method generates three subplots:

1. **Original Spectrum**: The input spectral signature
2. **Spectrum with Convex Hull**: Original spectrum overlaid with the computed convex hull
3. **Continuum-Removed Spectrum**: The final result after continuum removal

## Dataset

The project uses the **Cuprite** hyperspectral dataset, which includes:
- Ground truth spectral signatures for 12 mineral samples
- Wavelength range: Visible to near-infrared spectra
- Reference images for mineral identification

Minerals included:
- Alunite
- Andradite
- Buddingtonite
- Dumortierite
- Kaolinite variants
- Muscovite
- Montmorillonite
- Nontronite
- Pyrope
- Sphene
- Chalcedony

## Applications

This continuum removal implementation can be used for:
- Mineral identification from hyperspectral data
- Remote sensing applications
- Agricultural monitoring
- Environmental analysis
- Geological surveys
- Quality control in food and pharmaceutical industries

## References

- Continuum removal is widely used in hyperspectral imaging and spectroscopy
- The convex hull method is a standard approach for continuum normalization
- Cuprite dataset is a commonly used benchmark in hyperspectral analysis

## Author

UTMS Semester 3, Pattern Recognition Course - Project 1

## License

Educational use

## Contributing

This is an academic project for learning purposes.

## Future Enhancements

Potential improvements:
- [ ] Add support for other continuum removal methods (polynomial fitting, etc.)
- [ ] Batch processing capabilities for large datasets
- [ ] Custom plotting options and styling
- [ ] Statistical analysis of absorption features
- [ ] Export functionality for processed spectra
- [ ] GUI interface for interactive analysis

