# Multi-View Image Analysis - Scene-Adaptive Feature Correspondence Pipeline

A feature correspondence system for multi-view image analysis that employs scene-adaptive processing and integrated quality assessment. Built for the ETH3D dataset, this pipeline significantly improves matching quality and spatial coverage through pose-guided matching strategies and multi-layer occlusion detection.

# Author; Code IPYNB, Setup, Analysis files.
[![Author](https://img.shields.io/badge/Author-Joel%20Markapudi-blue)](https://www.linkedin.com/in/joemjs/)



## Key Features

- **Scene-Adaptive Processing**: Automatically adjusts matching parameters based on scene characteristics
  - Geometric complexity analysis and scene classification (confined/structured/open)
  - Dynamic parameter adjustment for different scene types
  - Quaternion-based view overlap computation

- **GPU-Accelerated Preprocessing**:
  - Optimized color space transformations (RGB→LAB→XYZ)
  - Enhanced CLAHE implementation with bilateral filtering
  - Batch processing with automated reference size detection

- **Advanced Feature Correspondence**:
  - FLANN-based matching with geometric verification
  - Multi-layer occlusion handling using masks and 3D constraints
  - Track formation with quality-based filtering
  - Comprehensive quality metrics and validation

## Performance Highlights

- 28.47% spatial coverage (vs. 25.7% baseline)
- Average track length increased from 3.49 to 3.56 frames
- Consistent quality scores (0.93/1.00)
- Processing over 1 million features with geometric consistency
- 38.52% successful 2D-3D correspondence rate
- Mean triangulation angle: 10.85°

## System Requirements

- The Setup Guide is present in the Setup Document (Environment) folder.
- Note that these commands are not ready-to-use Envrionment Setup Commands but rather are meant to be used for an idea.
- The latest copy of the YML file is present in the respective folder.
- This environment almost took 11+ GB and its requires significant study, and careful installation.
  
## Project Structure

```

ETH3D 3D Reconstruction Pipeline
├── Configuration & Initialization
│   ├── Environment Setup
│   │   ├── GPU Configuration (CUDA, PyTorch AMP, Memory Management)
│   │   └── Dataset Organization (mv_undistorted, calibration, image paths)
│   └── Component Configuration
│       ├── ProcessingConfig (Scene selection, batch sizes, thresholds)
│       └── Dataclass Hierarchy (GPUConfig, PreprocessingSettings, MatchingConfig)

├── Scene Processing Chain
│   ├── Scene Analysis & Preparation
│   │   ├── Scene Type Detection (CONFINED, STRUCTURED, OPEN)
│   │   ├── Camera Calibration Loading (intrinsics, poses, quaternions)
│   │   └── Image Organization (sequential pairs, path management)
│   │

│   ├── GPU-Accelerated Preprocessing
│   │   ├── Color Space Operations (RGB→LAB, gamma correction, XYZ conversion)
│   │   ├── Enhancement Chain (CLAHE, bilateral filtering, noise reduction)
│   │   └── Batch Processing (PyTorch tensors, memory-efficient operations)
│   │
│   ├── Feature Processing
│   │   ├── SIFT Detection (CPU-optimized, response strength, octave analysis)
│   │   ├── Quality Metrics (coverage ratio, spatial distribution, scale analysis)
│   │   └── Feature Management (ImageFeatures class, descriptor organization)
│   │   
│   ├── Match Processing
│   │   ├── Pair Selection
│   │   │   ├── View Overlap Analysis (frustum intersection, angle computation)
│   │   │   ├── Camera Position Analysis (baseline ratio, distance metrics)
│   │   │   └── Occlusion Mask/Mesh reading, Occlusion Filtering.

│   │   ├── Geometric Verification
│   │   │   ├── FLANN Matching (kNN, ratio test)
│   │   │   ├── RANSAC (fundamental matrix estimation, outlier rejection)
│   │   │   └── Pose-based Validation (triangulation angles, view metrics)
│   │   │

│   │   └── Quality Assessment
│   │       ├── Match Statistics (inlier ratios, distribution analysis)
│   │       └── Geometric Consistency (epipolar constraints, reprojection)
│   │
│   └── Correspondence Management
│       ├── Track Formation (feature ID management, sequential tracking)
│       ├── Track Analysis (length distribution, persistence metrics)
│       └── Consistency Validation (geometric verification, track merging)

├── Results Management
│   ├── Data Organization
│   │   ├── SceneData Structure (features, matches, metadata organization)
│   │   ├── Storage Hierarchy (HDF5 compression, JSON metadata)
│   │   └── Version Control (timestamps, processing records)
│   │
│   ├── Quality Control
│   │   ├── Validation Chain (feature quality, match consistency, track validity)
│   │   ├── Statistical Analysis (coverage metrics, match distribution)
│   │   └── Error Handling (graceful degradation, recovery mechanisms)
│   │
│   └── Visualization
│       ├── Match Visualization (OpenCV drawMatches, color coding)
│       ├── Track Analysis (length distribution, persistence plots)
│       └── Quality Metrics (heatmaps, distribution plots)

└── Registry & Testing
    ├── ResultsRegistry (singleton pattern, result access)
    ├── Performance Metrics (processing time, feature counts, match quality)
    └── Validation Tests (quick tests, sanity checks, quality verification)
```

## Core Components

### Feature Detection & Analysis
- Custom `FeatureExtractor` class with optimized SIFT implementation
- Grid-based spatial distribution analysis
- Real-time quality metrics computation

### Correspondence Management
- Scene-adaptive matching parameter selection
- Pose-guided matching strategies
- Multi-layer visibility checking
- Track formation and validation

### Quality Assessment
- Comprehensive validation framework
- Real-time feature distribution analysis
- Track length and distribution evaluation
- Match quality validation using geometric consistency

## Results & Visualization

The pipeline generates detailed visualizations and metrics:
- Feature distribution plots
- Track persistence analysis
- Match quality visualizations
- Camera path analysis
- Comprehensive quality metrics

## Dataset

The implementation is tested on the ETH3D High-Resolution Multi-View Dataset, specifically:
- High-resolution DSLR images (6048×4032)
- Camera calibration data
- Ground truth 3D point clouds
- Occlusion information (binary masks and surface meshes)


## Citation

If you use this code/work in your research, please cite:
```bibtex
@misc{markapudi2024multiview,
    title={Multi-View Image Analysis Pipeline - Enhancing Feature Correspondence through Scene-Adaptive Processing},
    author={Markapudi, Joel},
    year={2024},
    institution={Northeastern University}
}
```

## Acknowledgments
- ETH3D dataset team for providing the comprehensive multi-view dataset
- COLMAP project for inspiration in reconstruction workflows

## Contact
- Joel Markapudi - markapudi.j@northeastern.edu
