
# EgoVision Dataset

The **EgoVision** dataset is a curated collection of 3,064 high-quality (1920×1440) images collected from seven construction-related environments. Designed for egocentric vision tasks in construction safety and automation, this dataset supports various vision-related applications (e.g., image classification, object detection, and semantic segmentation).

## 📁 Folder Structure

```
EgoVision/
├── indoor/
│   ├── env1/
│   ├── env2/
│   └── env3/
├── outdoor/
│   ├── env1/
│   ├── env2/
│   ├── env3/
│   ├── env4/
│   └── env5/
├── processing/
│   ├── chessboard/
│   ├── camera_calibration.py
│   ├── preprocessing.py
│   └── augmentation.py
├── EgoVision Description.docx
└── README.md
```

## 📷 Dataset Overview

- **Total Images**: 3,064  
- **Indoor Scenes**: 1,464 images from 3 environments  
- **Outdoor Scenes**: 1,440 images from 5 environments  
- **Perspective**: Egocentric (first-person) view  
- **Image Size**: 1920×1440 pixels  
- **Supported Tasks**:
  - Hazard classification
  - Object detection
  - Semantic segmentation

## ⚙️ Step-by-Step Processing Instructions

### 1. 📌 Clone and Setup Environment

```bash
git clone https://github.com/your-repo/egovision-dataset.git
cd egovision-dataset
pip install -r requirements.txt
```

Ensure you have installed OpenCV, NumPy, and other dependencies required by the three scripts.

### 2. 🔍 Camera Calibration (Optional)

**Purpose**: Correct lens distortion and align egocentric images into a normalized projection space.

**Script**: `calibration/camera_calibration.py`

**Steps**:
1. Place checkerboard images in `calibration/images/`.
2. Set checkerboard size (e.g., 9x6) in the script.
3. Run the script to generate calibration parameters (`.npz` file).

```bash
python calibration/camera_calibration.py
```

**Output**: `calibration_data.npz` (includes camera matrix and distortion coefficients)

### 3. 🧼 Image Preprocessing

**Purpose**: Resize, crop, normalize, or rectify images for model compatibility.

**Script**: `preprocessing/preprocessing.py`

**Steps**:
1. Specify input and output directories.
2. Choose preprocessing operations (e.g., resize to 512x512, grayscale, rectification).
3. If calibration is needed, load the `.npz` file generated earlier.

```bash
python preprocessing/preprocessing.py --input data/raw --output data/processed --resize 512 512 --rectify calibration/calibration_data.npz
```

**Output**: Preprocessed images saved in `data/processed`

### 4. 🔁 Data Augmentation

**Purpose**: Increase training data diversity for better model generalization.

**Script**: `augmentation/augmentation.py`

**Supported Techniques**:
- Random rotation, flip
- Brightness/contrast adjustment
- Noise injection
- Perspective warp

**Steps**:
```bash
python augmentation/augmentation.py --input data/processed --output data/augmented --augmentations rotate flip brightness
```

**Output**: Augmented dataset in `data/augmented`

### 5. ✅ Dataset Usage Example

Use the processed data in your deep learning pipeline (e.g., PyTorch, TensorFlow). Sample code for loading and visualizing images is provided in the scripts.

## 📚 Reference

If you use this dataset, please cite:

> Liu, Z., Xu, J., Suen, C. W. K., Chen, M., Zou, Z., & Shi, Y. (2025). Egocentric camera-based method for detecting static hazardous objects on construction sites. *Automation in Construction*, 172, 106048.

## 🧠 Applications

The EgoVision dataset is suitable for:
- Risk assessment automation
- PPE detection
- Scene understanding in egocentric construction robotics
