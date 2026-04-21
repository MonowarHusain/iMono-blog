---
layout: post
title: "The Efficiency of Global vs. Adaptive Thresholding"
date: 2024-11-12
categories: [Image-Processing, Research]
---

In the early stages of image segmentation, the choice between **Global** and **Adaptive** thresholding is critical. While Global thresholding (Otsu's Method) is computationally cheap, it fails under non-uniform lighting—a common issue in medical imaging datasets.

### The Problem
When an image has varying illumination, a single $T$ value results in significant data loss in shadowed regions. 

### The Individual Logic (C++ Implementation)
To handle this, we calculate the threshold for each pixel based on its local neighborhood. This is a simple implementation of a mean-based adaptive filter:

```cpp
void adaptiveThreshold(const cv::Mat& src, cv::Mat& dst, int blockSize, int C) {
    // blocksize should be odd (e.g., 3, 5, 7)
    cv::adaptiveThreshold(src, dst, 255, 
                          cv::ADAPTIVE_THRESH_MEAN_C, 
                          cv::THRESH_BINARY, 
                          blockSize, C);
}