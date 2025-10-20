# Hands-on Notebook - Edge Detection and Kernels

This hands-on notebook explores edge detection and spatial kernels in digital images. It combines theory, worked examples, and executable Python code to demonstrate how convolutional kernels (filters) detect intensity changes and how classical edge detectors (Sobel, Prewitt, Roberts, Laplacian, Canny) are implemented and tuned.

## Learning objectives

- Understand convolution and discrete derivatives in 2D images.
- Construct and apply common kernels (Sobel, Prewitt, Roberts, Laplacian).
- Compare gradient magnitude, direction, and thresholding strategies.
- Implement and analyze the Canny edge detector steps (smoothing, gradient, non-maximum suppression, hysteresis).
- Explore border handling, smoothing trade-offs, and parameter sensitivity.
- Practice reproducible experiments with Jupyter notebooks.

## Prerequisites

- Basic Python (functions, NumPy arrays).
- Familiarity with linear algebra and discrete derivatives is helpful but not required.

Software requirements

- Python 3.8+ (tested)
- Packages: numpy, scipy, matplotlib, opencv-python (cv2) or scikit-image, jupyter

Quick install

```bash
python -m venv .venv
source .venv/bin/activate    # macOS / Linux
.\.venv\Scripts\Activate     # Windows
pip install --upgrade pip
pip install numpy scipy matplotlib scikit-image opencv-python jupyterlab
```

## Files in this folder

- README.md — this file
- edge-detection-and-kernels.ipynb — interactive notebook with explanations and runnable cells
- requirements.txt — (optional) pinned dependencies
- data/ — sample images used by the notebook (or the notebook will load images from scikit-image)

## Notebook structure

1. Introduction
    - Motivation and practical use cases (feature detection, segmentation preprocessing)
2. Theory refresher
    - Discrete convolution, kernels, separability
    - Relationship between smoothing and derivative estimation
3. Building kernels
    - Identity, box blur, Gaussian
    - First-order derivative kernels (forward, backward, central)
    - Sobel, Prewitt, Roberts, Laplacian kernels and interpretations
4. Filtering examples
    - Applying kernels with explicit convolution and via OpenCV / scikit-image
    - Handling borders (reflect, constant, nearest)
    - Visualizing gradient magnitude and orientation
5. Canny edge detector
    - Step-by-step implementation with visual intermediate results
    - Parameter tuning (sigma, low/high thresholds)
6. Experiments and exercises
    - Compare detectors on natural, synthetic, noisy images
    - Measure robustness to blur and noise
    - Implement custom kernels and test separability
7. Notes and best practices
    - Performance considerations (use separable filters, FFT for large kernels)
    - Numeric stability and dtype handling (convert to float, normalize kernels)
8. References and further reading
    - Links to algorithm descriptions and library docs

## How to run

- Start Jupyter Lab / Notebook in this directory:

```bash
jupyter lab
# or
jupyter notebook
```

- Open `edge-detection-and-kernels.ipynb` and run cells interactively.

Optional: Open the notebook directly in Google Colab — upload the notebook or use a repository link. If using Colab, install required packages in a cell:

```python
!pip install scikit-image opencv-python
```

## Tips for reproducible experiments

- Fix numpy and random seeds when generating synthetic data.
- Use consistent image normalization (e.g., float in [0, 1]).
- Keep a small config cell at the top of the notebook for parameters you want to vary.
- Save result figures to an `output/` directory with descriptive filenames.

## Expected outputs

- Side-by-side visual comparisons of filtered images and edge maps.
- Plots of gradient magnitude and orientation histograms.
- Interactive examples (via parameter cells) showing how kernel size, smoothing, and thresholds affect detection.

## Exercises (suggested)

- Implement a simple separable Gaussian + Sobel pipeline and compare to OpenCV's output.
- Implement non-maximum suppression from scratch and validate against scikit-image / OpenCV.
- Evaluate edge detectors on a noisy image and report which is most robust under different SNRs.

## Contact / Contribution

Submit issues or pull requests to the repository where this notebook is hosted. Include reproducible steps and sample images for any bug reports.
