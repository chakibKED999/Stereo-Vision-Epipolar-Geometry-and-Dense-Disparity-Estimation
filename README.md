# 📸 Stereo Vision: Epipolar Geometry & Dense Disparity Estimation

> A complete Computer Vision project implementing stereo image matching, epipolar geometry, fundamental matrix estimation, stereo rectification, and dense disparity map reconstruction using OpenCV and SIFT.

![Python](https://img.shields.io/badge/Python-3.10-blue)
![OpenCV](https://img.shields.io/badge/OpenCV-Computer_Vision-green)
![SIFT](https://img.shields.io/badge/SIFT-Feature_Detection-orange)
![Stereo](https://img.shields.io/badge/Stereo_Vision-Depth_Estimation-red)
![Master](https://img.shields.io/badge/Master-MIV-lightgrey)

---

# 📖 Overview

This project presents a complete **Stereo Vision pipeline** for estimating scene depth from two images captured by different viewpoints.

The project explores the fundamental concepts of **epipolar geometry**, **feature matching**, and **dense stereo correspondence**, ultimately reconstructing a **dense disparity map** representing the relative depth of objects in the scene.

Three complementary implementations are included:

- **Epipolar Geometry using SIFT**
- **Improved Fundamental Matrix Estimation using Homography Filtering**
- **Dense Disparity Map Reconstruction using StereoSGBM**

The project was developed as part of the **Master's Program in Image Processing & Artificial Intelligence (MIV)** at **USTHB** for the Computer Vision laboratory. It follows the practical work objectives of implementing SIFT-based matching, estimating the fundamental matrix, drawing epipolar lines, performing stereo rectification, and generating dense disparity maps. :contentReference[oaicite:0]{index=0} :contentReference[oaicite:1]{index=1}

---

# ✨ Features

- 📷 Stereo image processing
- 🔍 SIFT keypoint detection
- 🎯 Descriptor extraction
- 🔗 Feature matching
- ✅ Lowe Ratio Test
- 🧮 Fundamental Matrix estimation
- 📐 Epipolar line visualization
- 🏗️ Homography estimation with RANSAC
- 📌 Inlier filtering
- 🔄 Stereo rectification
- 🌄 Dense disparity map computation
- 📊 StereoSGBM algorithm
- 🎨 Disparity visualization
- 💾 Automatic result generation

---

# 📑 Project Report

## Project Objective

Recovering three-dimensional information from two-dimensional images is one of the most important problems in Computer Vision.

Stereo vision estimates the depth of objects by analyzing two images captured from slightly different viewpoints, similar to human binocular vision.

The objectives of this project are:

- Detect robust image features
- Match corresponding points
- Estimate the epipolar geometry
- Visualize epipolar constraints
- Rectify stereo images
- Compute dense disparity maps
- Estimate relative scene depth

This workflow forms the basis of many modern applications including:

- 🚗 Autonomous driving
- 🤖 Robotics
- 🚁 Drone navigation
- 🛰 Remote sensing
- 🏭 Industrial inspection
- 📦 Augmented Reality
- 🏥 Medical imaging

---

# 🧠 Understanding Stereo Vision

Stereo vision relies on two cameras observing the same scene.

Because the cameras are separated by a small baseline, every visible object appears at slightly different horizontal positions in both images.

This positional difference is called **disparity**.

The relationship between disparity and depth is inversely proportional:

- Large disparity → Object is close
- Small disparity → Object is far

Estimating accurate disparities therefore enables reconstruction of the scene's 3D structure.

---

# 🔍 Why SIFT?

The first step of stereo reconstruction is identifying reliable corresponding points.

This project uses the **Scale-Invariant Feature Transform (SIFT)** algorithm because it provides highly distinctive local image descriptors.

SIFT offers several advantages:

- Scale invariant
- Rotation invariant
- Robust to illumination changes
- Robust to viewpoint variation
- Excellent matching accuracy
- Stable keypoint localization

Each detected feature is represented by a high-dimensional descriptor that allows reliable matching between stereo images.

---

# 🔗 Feature Matching

After feature extraction, descriptors from the two images are matched.

The project applies:

- Brute Force Matching (BFMatcher)
- FLANN-based Matcher
- Lowe Ratio Test

The Lowe Ratio Test removes ambiguous matches by comparing the nearest and second-nearest descriptor distances, keeping only distinctive correspondences. The provided implementations detect SIFT features, compute descriptors, perform descriptor matching, and retain good correspondences using the ratio test before estimating the epipolar geometry. :contentReference[oaicite:2]{index=2} :contentReference[oaicite:3]{index=3}

---

# 📐 Epipolar Geometry

Epipolar geometry describes the geometric relationship between two camera views.

Instead of searching the entire second image for a corresponding point, the search is constrained to an **epipolar line**, greatly reducing computational complexity.

The project computes:

- Fundamental Matrix
- Epipolar Lines
- Inlier Correspondences

The resulting visualization demonstrates the geometric consistency between stereo image pairs.

---

# 🧮 Fundamental Matrix Estimation

The Fundamental Matrix establishes the mathematical relationship between corresponding image points.

This project estimates it using robust techniques:

- Least Median (LMedS)
- RANSAC

Robust estimation removes incorrect matches (outliers), preserving only geometrically consistent correspondences.

---

# 🏗️ Why Homography Filtering?

One implementation improves correspondence quality by estimating a **Homography Matrix** before computing the Fundamental Matrix.

Only matches that contribute to the best homography are retained.

Benefits include:

- Better correspondence quality
- Reduced outliers
- More stable Fundamental Matrix
- Cleaner epipolar lines
- Improved stereo reconstruction

This preprocessing significantly increases the reliability of the geometric estimation. The second implementation explicitly estimates a homography with RANSAC, filters matches to inliers, and only then computes the fundamental matrix from those correspondences. :contentReference[oaicite:4]{index=4}

---

# 🔄 Stereo Rectification

Before computing disparities, both images must be rectified.

Stereo rectification transforms both images so that:

- Corresponding pixels lie on the same horizontal scanline
- Stereo matching becomes significantly easier
- Horizontal disparity can be computed directly

This project performs **uncalibrated stereo rectification** using the estimated Fundamental Matrix.

---

# 🌄 Dense Disparity Estimation

After rectification, dense correspondence is computed using the **Stereo Semi-Global Block Matching (StereoSGBM)** algorithm.

Unlike sparse feature matching, dense stereo estimates disparity for nearly every image pixel.

Advantages include:

- Dense depth estimation
- Better object reconstruction
- Smooth disparity transitions
- Improved robustness

StereoSGBM combines local block matching with semi-global optimization to produce high-quality disparity maps.

---

# ⚙️ Pipeline

## 1️⃣ Image Acquisition

- Read stereo images
- Resize images
- Convert to grayscale

---

## 2️⃣ Feature Extraction

- Detect SIFT keypoints
- Compute descriptors

---

## 3️⃣ Feature Matching

- BFMatcher / FLANN
- Lowe Ratio Test
- Keep reliable matches

---

## 4️⃣ Geometric Estimation

- Estimate Homography (optional)
- Estimate Fundamental Matrix
- Remove outliers

---

## 5️⃣ Epipolar Geometry

- Compute epipolar lines
- Draw corresponding epipolar constraints
- Validate stereo consistency

---

## 6️⃣ Stereo Rectification

- Compute rectification homographies
- Warp stereo images
- Align epipolar lines horizontally

---

## 7️⃣ Dense Stereo Matching

- Configure StereoSGBM parameters
- Compute disparity
- Normalize disparity image

---

## 8️⃣ Visualization

Generate:

- SIFT Keypoints
- Feature Matches
- Epipolar Lines
- Rectified Images
- Dense Disparity Map

---

# 📂 Project Structure

```text
Stereo-Vision-Epipolar-Geometry-and-Dense-Disparity-Estimation/

│
├── epipolar1.py
├── epipolar2.py
├── disparity_map.py
│
├── images/
│   ├── left_images/
│   └── right_images/
│
├── results/
│   ├── sift_keypoints.png
│   ├── keypoint_matches.png
│   ├── epilines.png
│   ├── rectified_images.png
│   ├── disparity_SGBM_norm.png
│   └── original_images.png
│
├── report/
│   └── TP4_Computer_Vision.pdf
│
└── README.md
```

---

# ▶️ Running the Project

Install dependencies:

```bash
pip install opencv-python numpy matplotlib
```

Run the epipolar geometry experiment:

```bash
python epipolar1.py
```

Improved version with homography filtering:

```bash
python epipolar2.py
```

Generate the dense disparity map:

```bash
python disparity_map.py
```

---

# 📊 Results

The project produces several visual outputs:

- SIFT keypoints
- Feature correspondences
- Epipolar line visualization
- Rectified stereo pair
- Dense disparity map

These outputs demonstrate the complete stereo vision workflow from feature extraction to dense depth estimation.

---

# ✅ Strengths

- Complete stereo vision pipeline
- Robust SIFT feature extraction
- Accurate descriptor matching
- Homography-based outlier filtering
- Fundamental matrix estimation
- Epipolar geometry visualization
- Stereo rectification
- Dense disparity reconstruction
- Modular implementation
- Easy to extend

---

# ⚠️ Limitations

- Requires textured scenes
- Sensitive to repetitive patterns
- Performance depends on image quality
- Computationally expensive for high-resolution images
- Does not generate absolute metric depth without camera calibration

---

# 🚀 Future Improvements

- Camera calibration
- Depth map reconstruction in metric units
- 3D point cloud generation
- Open3D visualization
- GPU acceleration
- Deep-learning stereo matching
- Real-time stereo vision
- SLAM integration
- Visual odometry
- Autonomous robot navigation

---

# 🛠️ Technologies Used

- Python
- OpenCV
- NumPy
- Matplotlib
- SIFT
- BFMatcher
- FLANN Matcher
- RANSAC
- Homography
- Fundamental Matrix
- Stereo Rectification
- StereoSGBM

---

# 📚 References

- David G. Lowe — Distinctive Image Features from Scale-Invariant Keypoints (SIFT)
- Richard Hartley & Andrew Zisserman — Multiple View Geometry in Computer Vision
- OpenCV Documentation
- StereoSGBM Documentation
- Epipolar Geometry in Computer Vision
- USTHB — Computer Vision Laboratory (Master MIV)
