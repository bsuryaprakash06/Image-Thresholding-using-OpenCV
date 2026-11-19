# Image Thresholding using OpenCV

## Objective

The objective of this project is to implement and compare fundamental image thresholding techniques—global binary thresholding, adaptive Gaussian thresholding, and Otsu's binarization—using OpenCV in Python. The experiment evaluates the performance of each approach in segmenting foreground content (musical notation and text) from an image (`PianoNotes.png`) subjected to non-uniform illumination and background shadow gradients.

## Algorithm / Approach

The implementation loads the target image in grayscale mode and applies three distinct binarization strategies:

1. **Global Binary Thresholding (`cv2.threshold`)**:
   Applies fixed threshold values ($T = 50$ and $T = 127$) across all pixels. Pixels with intensity values greater than the threshold are set to the maximum value (255), while those below are mapped to 0.

2. **Adaptive Gaussian Thresholding (`cv2.adaptiveThreshold`)**:
   Computes localized threshold values for each pixel dynamically using a Gaussian-weighted sum over a local neighborhood window (block size of $11 \times 11$) minus a constant ($C = 2$). This accounts for spatial variations in illumination across the document.

3. **Otsu's Binarization (`cv2.THRESH_OTSU`)**:
   Calculates an optimal global threshold automatically by analyzing the bimodal intensity histogram and maximizing inter-class variance between foreground and background pixel distributions.

## Results

Each method is evaluated on `PianoNotes.png`, with outputs displayed side-by-side using Matplotlib:

- **Global Thresholding**: Fixed thresholds fail to handle the lighting gradient. At $T = 127$, shaded regions are entirely masked out and information is lost. At $T = 50$, foreground notes are captured in shaded areas but significant noise and artifacts appear across brighter areas.
- **Adaptive Gaussian Thresholding**: Produces the superior segmentation result. By adapting the threshold locally, it effectively suppresses uneven shadows and isolates musical notes, clefs, and staff lines with high clarity across the entire page.
- **Otsu's Thresholding**: Computes an optimal global threshold ($T \approx 133$) without manual parameter tuning. However, as a global approach, it cannot compensate for localized illumination gradients and produces similar loss of detail in shaded regions as manual global thresholding.

## References

- OpenCV Documentation: Image Thresholding (https://docs.opencv.org/4.x/d7/d4d/tutorial_py_thresholding.html)
- Otsu, N. (1979). "A Threshold Selection Method from Gray-Level Histograms." *IEEE Transactions on Systems, Man, and Cybernetics*, 9(1), 62–66.
