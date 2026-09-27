# Fish Detection and Tracking System

A real-time fish detection and tracking system using YOLOv4 and TensorFlow, specifically designed for monitoring aquarium fish species.

## 🐟 Overview

This system is capable of detecting and tracking two specific fish species commonly found in aquariums:
- Paracheirodon innesi (neon_bleu)
- Paracheirodon axelrodi (cardinalis)

The project uses YOLOv4 (You Only Look Once) for real-time object detection, combined with TensorFlow for efficient processing.

## ✨ Features

- Real-time fish detection and tracking
- Support for both video files and webcam input
- Fish counting functionality
- Automatic logging of detection data
- Support for both CPU and GPU environments
- Option to use either full YOLOv4 or YOLOv4-tiny models
- Detection cropping capability
- Detailed detection information output

## 🛠️ Installation

### Prerequisites
- Python 3.7+
- CUDA-capable GPU (optional, for GPU support)
- Webcam (for live detection)

### Environment Setup

1. Clone the repository:
```bash
git clone https://github.com/yourusername/fish-detector.git
cd fish-detector
```

2. Create and activate the conda environment:

For CPU-only setup:
```bash
conda env create -f conda-cpu.yml
conda activate yolov4-cpu
```

For GPU setup:
```bash
conda env create -f conda-gpu.yml
conda activate yolov4-gpu
```

3. Download the pre-trained weights:
- Download YOLOv4 weights: [yolov4_93map.weights](https://drive.google.com/file/d/17yiD7xVCRPZotjC0yaFAiP5wz6Umd2HW/view?usp=sharing)
- Place the weights file in the `data` directory

## 🚀 Usage

### Converting Weights
First, convert the Darknet weights to TensorFlow format:
```bash
python save_model.py --weights ./data/yolov4_93map.weights --output ./checkpoints/yolov4-416 --input_size 416 --model yolov4
```

### Running Detection

1. **Image Detection**:
```bash
python detect.py --weights ./checkpoints/yolov4-416 --size 416 --model yolov4 --images ./data/images/<YOUR_IMAGE>
```

2. **Video Detection**:
```bash
python detect_video.py --weights ./checkpoints/yolov4-416 --size 416 --model yolov4 --video ./data/video/<YOUR_VIDEO> --output ./detections/results.avi
```

3. **Webcam Detection**:
```bash
python detect_video.py --weights ./checkpoints/yolov4-416 --size 416 --model yolov4 --video 0 --output ./detections/webcam.avi
```

### Additional Features

1. **Enable Fish Counting**:
Add the `--count` flag to any command:
```bash
python detect_video.py --weights ./checkpoints/yolov4-416 --size 416 --model yolov4 --video 0 --count
```

2. **Crop Detections**:
Add the `--crop` flag to save individual detections:
```bash
python detect_video.py --weights ./checkpoints/yolov4-416 --size 416 --model yolov4 --video 0 --crop
```

3. **Show Detection Info**:
Add the `--info` flag to display detailed detection information:
```bash
python detect_video.py --weights ./checkpoints/yolov4-416 --size 416 --model yolov4 --video 0 --info
```

## 📊 Logging

The system automatically logs detection information every 30 seconds to `fish_detection_log.txt` in the root directory. The log includes:
- Timestamp
- Current FPS
- Fish counts by species
- Detection statistics

## 🎯 Using YOLOv4-tiny

For systems with limited computing power, you can use the YOLOv4-tiny model:

1. Download YOLOv4-tiny weights: [yolov4-tiny_93map.weights](https://drive.google.com/file/d/175rwTsZLAkaqbiJoY00vK0m5AHqzuvFh/view?usp=sharing)

2. Convert weights:
```bash
python save_model.py --weights ./data/yolov4-tiny_93map.weights --output ./checkpoints/yolov4-tiny-416 --input_size 416 --model yolov4 --tiny
```

3. Run detection with tiny model:
```bash
python detect_video.py --weights ./checkpoints/yolov4-tiny-416 --size 416 --model yolov4 --video 0 --tiny
```

## 📁 Project Structure

```
fish-detector/
├── assets/              # Project assets and images
├── checkpoints/         # Model checkpoints
├── core/               # Core functionality
├── data/               # Data and weights
├── detections/         # Detection outputs
├── utils/              # Utility functions
├── conda-cpu.yml       # CPU environment config
├── conda-gpu.yml       # GPU environment config
├── detect.py           # Image detection script
├── detect_video.py     # Video detection script
└── save_model.py       # Model conversion script
```

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- YOLOv4 implementation by [AlexeyAB](https://github.com/AlexeyAB/darknet)
- TensorFlow implementation by [hunglc007](https://github.com/hunglc007/tensorflow-yolov4-tflite)
- Project modifications and improvements by [ameyasharma999](https://github.com/ameyasharma999)
