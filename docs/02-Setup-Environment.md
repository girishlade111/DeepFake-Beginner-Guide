# Setting Up Your DeepFake Development Environment

## Overview

This guide will walk you through setting up a complete environment for working with DeepFake technology, including software, hardware considerations, and essential tools.

## Hardware Requirements

### Minimum Requirements
- **CPU**: Intel i5 or AMD Ryzen 5 (4+ cores)
- **RAM**: 8GB (16GB recommended)
- **Storage**: 50GB free space (SSD preferred)
- **GPU**: NVIDIA GPU with 4GB+ VRAM (optional but highly recommended)
- **OS**: Windows 10/11, Ubuntu 20.04+, or macOS 10.15+

### Recommended Setup
- **CPU**: Intel i7/i9 or AMD Ryzen 7/9 (8+ cores)
- **RAM**: 32GB or more
- **Storage**: 500GB+ SSD
- **GPU**: NVIDIA RTX 3060+ with 8GB+ VRAM
- **OS**: Ubuntu 22.04 LTS (best compatibility)

### GPU Considerations
- **CUDA Support**: Essential for training and processing
- **VRAM**: More VRAM = higher resolution processing
- **Brands**: NVIDIA preferred (better CUDA/cuDNN support)
- **Cloud Options**: Google Colab, AWS, Azure for GPU access

## Software Installation

### Step 1: Install Python

#### Windows
```bash
# Download Python 3.9 or 3.10 from python.org
# During installation, check "Add Python to PATH"
# Verify installation:
python --version
pip --version
```

#### Linux (Ubuntu/Debian)
```bash
sudo apt update
sudo apt install python3.10 python3-pip python3-venv
python3 --version
```

#### macOS
```bash
# Install Homebrew first (brew.sh)
brew install python@3.10
python3 --version
```

### Step 2: Install CUDA and cuDNN (For NVIDIA GPUs)

#### Check CUDA Compatibility
```bash
nvidia-smi
```

#### Install CUDA Toolkit
1. Visit: https://developer.nvidia.com/cuda-downloads
2. Download CUDA 11.8 or compatible version
3. Follow installation wizard
4. Verify installation:
```bash
nvcc --version
```

#### Install cuDNN
1. Visit: https://developer.nvidia.com/cudnn
2. Download cuDNN for your CUDA version
3. Extract and copy files to CUDA directory
4. Set environment variables

### Step 3: Create Virtual Environment

```bash
# Create project directory
mkdir deepfake-projects
cd deepfake-projects

# Create virtual environment
python -m venv deepfake-env

# Activate environment
# Windows:
deepfake-env\Scripts\activate
# Linux/macOS:
source deepfake-env/bin/activate
```

### Step 4: Install Deep Learning Frameworks

#### PyTorch (Recommended)
```bash
# For CUDA 11.8
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118

# For CPU only
pip install torch torchvision torchaudio

# Verify installation
python -c "import torch; print(torch.cuda.is_available())"
```

#### TensorFlow (Alternative)
```bash
pip install tensorflow>=2.10.0

# Verify GPU support
python -c "import tensorflow as tf; print(tf.config.list_physical_devices('GPU'))"
```

### Step 5: Install Essential Libraries

```bash
# Computer vision
pip install opencv-python opencv-contrib-python
pip install dlib
pip install face-recognition
pip install mediapipe

# Image processing
pip install Pillow
pip install scikit-image
pip install imageio

# Data handling
pip install numpy pandas
pip install scipy

# Visualization
pip install matplotlib
pip install seaborn

# Deep learning utilities
pip install albumentations
pip install timm
```

### Step 6: Install DeepFake-Specific Tools

#### FaceSwap
```bash
git clone https://github.com/deepfakes/faceswap.git
cd faceswap
pip install -r requirements.txt
python faceswap.py gui
```

#### DeepFaceLab
```bash
# Download from:
# https://github.com/iperov/DeepFaceLab
# Windows: Download pre-built package
# Linux: Build from source
```

#### First Order Motion Model
```bash
git clone https://github.com/AliaksandrSiarohin/first-order-model
cd first-order-model
pip install -r requirements.txt
```

## Development Tools

### Code Editors and IDEs

#### Visual Studio Code
```bash
# Download from code.visualstudio.com
# Install extensions:
# - Python
# - Jupyter
# - GitLens
# - Pylance
```

#### PyCharm
- Professional IDE for Python
- Great for large projects
- Download from jetbrains.com/pycharm

#### Jupyter Notebook
```bash
pip install jupyter notebook jupyterlab
jupyter notebook
```

### Version Control

#### Git Setup
```bash
# Install Git
sudo apt install git  # Linux
brew install git       # macOS
# Windows: Download from git-scm.com

# Configure
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

#### GitHub/GitLab
- Create account for code versioning
- Use for backing up projects
- Collaborate with others

### Data Management Tools

#### Download Managers
```bash
# aria2c for fast downloads
sudo apt install aria2

# yt-dlp for video downloads
pip install yt-dlp
```

#### Dataset Tools
```bash
pip install kaggle
pip install gdown  # Google Drive downloads
```

## Cloud Platform Setup (Optional)

### Google Colab
1. Visit colab.research.google.com
2. Sign in with Google account
3. Free GPU access (with limitations)
4. Install packages in each session

### AWS Setup
```bash
# Install AWS CLI
pip install awscli

# Configure credentials
aws configure

# Use EC2 with GPU instances (p3.2xlarge)
```

### Kaggle Notebooks
1. Visit kaggle.com
2. Create account
3. Access free GPU/TPU resources
4. Use public datasets

## Testing Your Setup

### Test Script

Create `test_setup.py`:

```python
import sys
import torch
import cv2
import numpy as np
import face_recognition

def test_environment():
    print("=== Environment Test ===")
    
    # Python version
    print(f"Python: {sys.version}")
    
    # PyTorch
    print(f"PyTorch: {torch.__version__}")
    print(f"CUDA Available: {torch.cuda.is_available()}")
    if torch.cuda.is_available():
        print(f"CUDA Version: {torch.version.cuda}")
        print(f"GPU: {torch.cuda.get_device_name(0)}")
    
    # OpenCV
    print(f"OpenCV: {cv2.__version__}")
    
    # NumPy
    print(f"NumPy: {np.__version__}")
    
    # Face Recognition
    print(f"face_recognition: Available")
    
    print("\n=== All tests passed! ===")

if __name__ == "__main__":
    test_environment()
```

Run: `python test_setup.py`

## Troubleshooting

### Common Issues

#### CUDA Not Detected
```bash
# Check driver version
nvidia-smi

# Reinstall CUDA toolkit
# Verify PATH variables
echo $PATH
```

#### Import Errors
```bash
# Update pip
pip install --upgrade pip

# Reinstall package
pip uninstall package_name
pip install package_name
```

#### Memory Errors
- Reduce batch size
- Use smaller models
- Enable mixed precision training
- Use gradient accumulation

#### Slow Performance
- Enable GPU acceleration
- Use SSD for data
- Increase RAM
- Use data loading workers

## Best Practices

1. **Use Virtual Environments**: Isolate project dependencies
2. **Version Control**: Track all code changes
3. **Document Setup**: Keep notes on configuration
4. **Regular Backups**: Save models and data
5. **Update Regularly**: Keep libraries current
6. **Monitor Resources**: Use nvidia-smi, htop
7. **Clean Workspace**: Remove unused files/models

## Resource Monitoring

### GPU Monitoring
```bash
# Real-time GPU usage
watch -n 0.5 nvidia-smi

# GPU memory usage
nvdia-smi --query-gpu=memory.used --format=csv
```

### System Monitoring
```bash
# CPU/RAM usage
htop

# Disk usage
df -h
du -sh *
```

## Next Steps

After setting up your environment:

1. Download sample datasets
2. Run basic face detection tests
3. Explore pre-trained models
4. Follow tutorials in next chapters
5. Join community forums for support

## Additional Resources

- **PyTorch Documentation**: pytorch.org/docs
- **TensorFlow Guide**: tensorflow.org/guide
- **CUDA Toolkit Docs**: docs.nvidia.com/cuda
- **OpenCV Tutorials**: docs.opencv.org
- **FaceSwap Forum**: faceswap.dev/forum

---

**Pro Tip**: Keep a separate environment for each major project to avoid dependency conflicts.
