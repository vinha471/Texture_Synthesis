# Texture Synthesis Project

This project implements texture synthesis algorithms, starting with the seminal **Efros-Leung algorithm** and extending to **Image Quilting** for texture synthesis and transfer.

## Table of Contents

-   [Overview](#overview)
-   [File Structure](#file-structure)
-   [Installation](#installation)
-   [Quick Start](#quick-start)
-   [Implementation Details](#implementation-details)
-   [Usage](#usage)
-   [Examples](#examples)
-   [API Reference](#api-reference)
-   [Requirements](#requirements)
-   [Input Textures](#input-textures)
-   [Academic Context](#academic-context)
-   [Contributing](#contributing)
-   [License](#license)
-   [References](#references)
-   [Future Work](#future-work)

## Overview

Texture synthesis is the process of generating larger textures from small input samples while maintaining the visual characteristics and patterns of the original. This project demonstrates two key approaches:

1. **Efros-Leung Algorithm**: Non-parametric sampling that synthesizes textures pixel by pixel
2. **Image Quilting**: Block-based synthesis using overlapping regions and minimum error boundary cuts

## File Structure

```
Texture_Synthesis/
├── README.md                           # This file
├── Texture_Synthesis_Non_Param_Samp.ipynb  # Main implementation notebook
└── requirements.txt                    # Python dependencies
```

## Installation

### Prerequisites

-   Python 3.7 or higher
-   pip package manager

### Setup

1. Clone the repository:

```bash
git clone <repository-url>
cd Texture_Synthesis
```

2. Install dependencies:

```bash
pip install -r requirements.txt
```

3. Launch Jupyter Notebook:

```bash
jupyter notebook Texture_Synthesis_Non_Param_Samp.ipynb
```

## Quick Start

1. **Load a texture image**:

```python
from PIL import Image
import numpy as np

texture = np.array(Image.open('path/to/texture.jpg'))
```

2. **Run basic synthesis**:

```python
# Basic Efros-Leung synthesis
synthesized = synthesize_texture(texture, output_size=(256, 256), window_size=9)
```

3. **View results**:

```python
plt.imshow(synthesized, cmap='gray')
plt.show()
```

## Implementation Details

### Efros-Leung Algorithm

The core implementation follows the paper "Texture Synthesis by Non-parametric Sampling" by Efros and Leung (1999). Key components include:

-   **Neighborhood Matching**: Finds similar neighborhoods in the source texture using Sum of Squared Differences (SSD)
-   **Gaussian Weighting**: Applies Gaussian-weighted windows when comparing neighborhoods for better quality
-   **Pixel-by-Pixel Synthesis**: Grows the texture outward from an initial seed, carefully choosing synthesis order
-   **Threshold-based Selection**: Uses similarity thresholds to ensure high-quality matches

#### Key Functions

-   `create_gaussian_window()`: Creates Gaussian-weighted windows for neighborhood comparison
-   `find_matching_neighborhoods()`: Core algorithm for finding similar neighborhoods
-   `synthesize_texture()`: Main synthesis loop that grows the texture

### Image Quilting Extension

Building on the Efros-Leung foundation, this project extends to implement "Image Quilting for Texture Synthesis and Transfer" (Efros & Freeman, SIGGRAPH 2001). This approach:

-   **Block-based Synthesis**: Takes square blocks from input texture and patches them together
-   **Overlap Handling**: Uses overlap between adjacent blocks to find good matches
-   **Minimum Error Boundary Cuts**: Computes optimal cuts between overlapping blocks using dynamic programming
-   **Reduced Artifacts**: Minimizes visual artifacts through intelligent block placement

## Features

-   **Modular Design**: Clean separation between core algorithms and utility functions
-   **Visualization Tools**: Built-in plotting and testing functions for algorithm validation
-   **Parameter Tuning**: Configurable window sizes, thresholds, and synthesis parameters
-   **Performance Optimization**: Efficient neighborhood search and matching algorithms

## Usage

The notebook is structured in logical sections:

1. **Setup and Utilities**: Helper functions and visualization tools
2. **Gaussian Window Creation**: Weighted neighborhood comparison
3. **Neighborhood Matching**: Core Efros-Leung algorithm implementation
4. **Texture Synthesis**: Complete synthesis pipeline
5. **Image Quilting**: Advanced block-based synthesis

### Parameters

-   `window_size`: Size of neighborhood window (odd numbers recommended)
-   `threshold`: Similarity threshold for neighborhood matching
-   `output_size`: Desired dimensions of synthesized texture
-   `gaussian_sigma`: Standard deviation for Gaussian weighting

## Examples

### Basic Texture Synthesis

```python
# Load texture
texture = load_texture('brick_pattern.jpg')

# Synthesize larger texture
result = synthesize_texture(
    texture,
    output_size=(512, 512),
    window_size=11,
    threshold=0.1
)

# Visualize
plot_comparison(texture, result)
```

### Image Quilting

```python
# Implement block-based synthesis
quilting_result = image_quilting(
    texture,
    block_size=32,
    overlap_size=8,
    output_size=(256, 256)
)
```

## API Reference

### Core Functions

#### `synthesize_texture(source_texture, output_size, window_size, threshold)`

Main synthesis function implementing Efros-Leung algorithm.

**Parameters:**

-   `source_texture`: Input texture as numpy array
-   `output_size`: Tuple of (height, width) for output
-   `window_size`: Neighborhood window size (odd integer)
-   `threshold`: Similarity threshold for matching

**Returns:**

-   Synthesized texture as numpy array

#### `find_matching_neighborhoods(target_neighborhood, source_texture, gaussian_window, valid_mask)`

Finds similar neighborhoods in source texture.

**Parameters:**

-   `target_neighborhood`: Target neighborhood to match
-   `source_texture`: Source texture to search in
-   `gaussian_window`: Gaussian weighting window
-   `valid_mask`: Mask of valid pixels

**Returns:**

-   List of matching neighborhood coordinates

## Requirements

-   Python 3.7+
-   NumPy 1.19+
-   Matplotlib 3.3+
-   PIL/Pillow 8.0+
-   Jupyter Notebook

## Input Textures

The project works with various input textures and includes sample texture files for testing and demonstration. Supported formats:

-   JPEG (.jpg, .jpeg)
-   PNG (.png)
-   TIFF (.tiff)
-   BMP (.bmp)

## Academic Context

This implementation serves as a foundation for understanding texture synthesis principles and can be extended for:

-   Texture transfer applications
-   Style transfer in computer graphics
-   Procedural texture generation
-   Computer vision research

## Contributing

We welcome contributions! Please feel free to submit a Pull Request. For major changes, please open an issue first to discuss what you would like to change.

### Development Setup

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## References

-   Efros, A. A., & Leung, T. K. (1999). Texture synthesis by non-parametric sampling. ICCV.
-   Efros, A. A., & Freeman, W. T. (2001). Image quilting for texture synthesis and transfer. SIGGRAPH.

## Future Work

Potential extensions include:

-   Multi-scale texture synthesis
-   Texture transfer between images
-   Real-time synthesis for interactive applications
-   Integration with deep learning approaches

---

**Note**: This project is part of CS378: Generative Vision and Computing coursework. For questions or issues, please refer to the course materials or contact the course instructor.
