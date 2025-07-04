
# Underwater Object Detection Framework

This project implements a lightweight underwater object detection framework, integrating image enhancement (RE-MSRCR) and an improved detection model (AFPN-YOLOv8). The method is designed to improve visibility, enhance small object features, and boost detection performance under challenging underwater conditions.

---

## 📁 Project Structure

```
code/
├── RE-MSRCR/          # Image enhancement module
│   ├── demo_some.py   # Demo entry for RE-MSRCR
│   └── code/
│       ├── retinex_red_enhance.py  # Main enhancement algorithm
│       ├── plot.py, tools.py       # Visualization & utilities
│       └── fgb/                    # Fast Gaussian Blur in Cython
├── AFPN-YOLOv8/        # Detection module
│   ├── ultralytics/    # Modified YOLOv8 core with AFPN
│   ├── datasets/       # Dataset loading & processing
│   ├── train.py        # Training entry point
│   └── val.py, detect.py, export.py  # Evaluation and inference
```

---

## 🔧 Installation

### 1. Environment Preparation

Python ≥ 3.8 is recommended. Create a virtual environment:

```bash
conda create -n uwdet python=3.8 -y
conda activate uwdet
```

### 2. Install Required Dependencies

**For RE-MSRCR (Image Enhancement)**

```bash
cd RE-MSRCR/code/fgb
python setup.py build_ext --inplace  # Compile Cython
cd ../..
pip install -r requirements.txt      # If provided
```

Or manually install:

```bash
pip install numpy opencv-python matplotlib
```

**For AFPN-YOLOv8 (Detection Module)**

```bash
cd AFPN-YOLOv8
pip install -e .
```

---

## 🚀 Usage

### 1. Image Enhancement with RE-MSRCR

```bash
cd RE-MSRCR
python demo_some.py --input ./input/ --output ./output/
```

- Input: Folder with underwater images.
- Output: Enhanced images saved to target path.

### 2. Model Training (AFPN-YOLOv8)

```bash
cd AFPN-YOLOv8
python train.py --data ./configs/uw.yaml --img 640 --batch 16 --epochs 100 --device 0
```

- `--data`: Path to the dataset config file (follow YOLOv8 format).
- `--img`: Training image size.
- `--batch`: Batch size.
- `--device`: GPU device id.

### 3. Inference

```bash
python detect.py --weights runs/train/exp/weights/best.pt --source ./samples/
```

---

## 🧪 Dataset Format

Ensure your dataset follows YOLO format:

```
uw_dataset/
├── images/
│   ├── train/
│   ├── val/
├── labels/
│   ├── train/
│   ├── val/
```

The dataset config file (e.g., `uw.yaml`) should include:

```yaml
path: ../uw_dataset
train: images/train
val: images/val
nc: 3
names: ["fish", "cucumber", "urchin"]
```

---

## 📊 Evaluation

Run validation and calculate mAP, precision, recall:

```bash
python val.py --weights runs/train/exp/weights/best.pt --data ./configs/uw.yaml
```

---

## 📎 Citation

If you use this code in your research, please cite our paper:

```bibtex
@article{your2025paper,
  title={A Lightweight Underwater Object Detection Framework via Enhanced MSRCR and Asymptotic Feature Fusion},
  author={Your Name et al.},
  journal={To be submitted to SCI journal},
  year={2025}
}
```

---

## 📮 Contact

For questions or collaboration, feel free to reach out via [your.email@example.com].
