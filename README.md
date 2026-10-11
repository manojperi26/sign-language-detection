# 🤟 Real-Time ASL Alphabet Recognition Using YOLOv5

A computer vision project for detecting American Sign Language (ASL) alphabet hand signs using **YOLOv5 and OpenCV**. The system processes webcam frames, identifies hand signs, and supports chaining detected letters into words.

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.7-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python"/>
  <img src="https://img.shields.io/badge/PyTorch-1.12-EE4C2C?style=for-the-badge&logo=pytorch&logoColor=white" alt="PyTorch"/>
  <img src="https://img.shields.io/badge/YOLOv5-Object%20Detection-00FFFF?style=for-the-badge" alt="YOLOv5"/>
  <img src="https://img.shields.io/badge/OpenCV-Computer%20Vision-5C3EE8?style=for-the-badge&logo=opencv&logoColor=white" alt="OpenCV"/>
</p>

**Author:** [Peri Naga Venkata Sai Manoj](https://github.com/manojperi26) · [LinkedIn](https://linkedin.com/in/manojperi26)

---

## 🎯 Project Overview

Communication barriers can make everyday interactions difficult for people who use sign language. This project explores real-time hand-sign recognition using object detection.

A YOLOv5s model is trained to identify ASL alphabet signs from images and webcam frames. Detected letters can be combined into words, with further improvements needed to make word formation reliable.

### ✨ Key Features

- **Real-time detection:** Processes webcam frames using OpenCV.
- **Alphabet recognition:** Detects trained ASL alphabet classes.
- **Word formation:** Supports combining detected letters into words.
- **Transfer learning:** Starts from pretrained YOLOv5s weights.
- **Model evaluation:** Uses precision, recall, mAP, and confusion-matrix analysis.
- **Visual inspection:** Includes validation predictions and training results.

## 🎬 Demo

The following demonstration illustrates the system recognizing the word **HELLO**.

<p align="center">
  <img src="Sign-Language-yolo/Result/hello.gif" alt="Real-time ASL alphabet recognition spelling HELLO" width="800"/>
</p>

<p align="center"><em>Real-time ASL hand-sign detection demonstration.</em></p>

> **Note:** The GIF path is relative to the repository root. Ensure the file exists at the specified location and renders correctly on GitHub.

## 📊 Model Performance

The model was evaluated on a held-out validation split containing **144 images**, using YOLOv5s at a resolution of 448 × 448 pixels.

| Evaluation Metric | Reported Result |
|:---|---:|
| Precision | 0.90 |
| Recall | 0.87 |
| mAP@0.5 | 0.95 |
| mAP@0.5:0.95 | 0.78 |
| Inference time | ~5 ms/image |

**Hardware:** Google Colab · NVIDIA Tesla T4

### Understanding the Results

- **Precision (90%):** Measures the proportion of predicted detections that are correct.
- **Recall (87%):** Measures the proportion of ground-truth objects successfully detected.
- **mAP@0.5 (95%):** Measures average precision at an IoU threshold of 0.50.
- **mAP@0.5:0.95 (78%):** Measures average precision across IoU thresholds from 0.50 to 0.95.
- **Inference time (~5 ms):** Reported model inference time; it should not be interpreted as end-to-end webcam latency or guaranteed FPS.

### Confusion Matrix

<p align="center">
  <img src="Sign-Language-yolo/Result/ASL/confusion_matrix.png" alt="YOLOv5 ASL alphabet confusion matrix" width="800"/>
</p>

### Ground Truth vs. Model Predictions

<table>
  <tr>
    <th align="center">Ground-Truth Labels</th>
    <th align="center">Model Predictions</th>
  </tr>
  <tr>
    <td align="center">
      <img src="Sign-Language-yolo/Result/ASL/val_batch0_labels.jpg" alt="Ground-truth labels from a validation batch" width="400"/>
    </td>
    <td align="center">
      <img src="Sign-Language-yolo/Result/ASL/val_batch0_pred.jpg" alt="YOLOv5 predictions on a validation batch" width="400"/>
    </td>
  </tr>
</table>

These visualizations help inspect localization quality, classification errors, and differences between ground-truth annotations and model predictions.

## 🧠 Training Configuration

| Parameter | Configuration |
|:---|:---|
| Model | YOLOv5s v6.1 |
| Initial weights | `yolov5s.pt` |
| Input resolution | 448 × 448 |
| Batch size | 64 |
| Maximum epochs | 500 |
| Best checkpoint | Epoch 383 |
| Optimizer | SGD |
| Training environment | Google Colab |
| GPU | NVIDIA Tesla T4 |
| Dataset format | YOLO object detection |
| Dataset | [Roboflow ASL Letters](https://public.roboflow.com/object-detection/american-sign-language-letters/1) |

The best checkpoint was selected during training using validation performance. The reported validation metrics are therefore model-selection results, not an independent estimate of generalization performance.

## 🛠️ Tech Stack

| Technology | Purpose |
|:---|:---|
| Python | Core programming language |
| PyTorch | Deep learning framework |
| YOLOv5 | Object detection |
| OpenCV | Webcam capture and image processing |
| Albumentations | Image augmentation |
| Roboflow | Dataset access and preparation |
| TensorBoard | Training visualization |

## 📁 Project Structure

```text
Sign-Language-yolo/
├── American Sign Language dataset/
│   ├── train/
│   ├── valid/
│   ├── test/
│   └── data.yaml
├── Result/
│   ├── hello.gif
│   └── ASL/
│       ├── confusion_matrix.png
│       ├── val_batch0_labels.jpg
│       └── val_batch0_pred.jpg
└── Yolov5_ASL_training_testing/
    ├── Real-Time ASL Detection - Training.ipynb
    └── Real-Time ASL Detection - Testing.ipynb
```

*The tree illustrates the intended organization. Adjust filenames and directories to match the actual repository.*

## 🚀 Getting Started

### Prerequisites

- Python environment compatible with the project dependencies.
- Git.
- A webcam for live detection.
- A trained YOLOv5 checkpoint, such as `best.pt`.
- Google Colab for the provided training workflow, if needed.

### 1. Clone the Repository

```bash
git clone https://github.com/manojperi26/Sign-Language-yolo.git
cd Sign-Language-yolo
```

### 2. Train the Model

Open `Real-Time ASL Detection - Training.ipynb` in Google Colab.

Configure the dataset paths, verify the YOLOv5 dependencies, and execute the notebook to train the model.

### 3. Run Real-Time Detection

Open `Real-Time ASL Detection - Testing.ipynb` in a compatible local Jupyter environment.

Configure the webcam and model checkpoint paths, then execute the notebook cells.

**Important:** The repository must contain the correct notebook filenames, and the testing notebook must point to the actual location of `best.pt`. The original training configuration uses older dependencies, so reproduce the notebook environment before upgrading packages.

## ⚠️ Limitations

- **Limited validation data:** The 144-image validation set contains only 1–9 samples per letter, making per-class metrics potentially unstable.
- **Potential validation bias:** The best checkpoint was selected using the same validation split used for reporting.
- **Confusable signs:** Visually similar hand signs can be difficult to distinguish, and some letters may have weaker precision or recall.
- **Motion-dependent letters:** ASL letters J and Z involve movement. A single-frame detector may not reliably recognize their complete motion.
- **Word formation:** Combining frame-by-frame predictions can introduce duplicate or incorrect letters without temporal smoothing.
- **Limited real-world evaluation:** Webcam testing was visual only; no quantitative real-world performance score was established.
- **Inference speed:** The reported timing does not establish end-to-end latency on consumer hardware.

This project is an experimental alphabet-recognition system, not a complete sign-language translation solution.

## 🔮 Future Improvements

- [ ] Evaluate the final model on the untouched test split.
- [ ] Test on unseen signers, backgrounds, lighting conditions, and camera positions.
- [ ] Expand the dataset for difficult and underrepresented classes.
- [ ] Add temporal smoothing and confidence-based letter stabilization.
- [ ] Implement duplicate-letter prevention and a manual word-reset control.
- [ ] Explore sequence modeling for motion-dependent signs such as J and Z.
- [ ] Measure end-to-end webcam latency and FPS on different devices.
- [ ] Package the detector into a simple, accessible web application.

## 📚 Dataset and Acknowledgements

- **Dataset:** [Roboflow — American Sign Language Letters](https://public.roboflow.com/object-detection/american-sign-language-letters/1)
- **Detection framework:** [Ultralytics YOLOv5](https://github.com/ultralytics/yolov5)
- **Dataset platform:** [Roboflow](https://roboflow.com/)

Please review the applicable dataset license and framework license before redistributing data, weights, or derived artifacts.

## 👨‍💻 Author

**Peri Naga Venkata Sai Manoj**

B.Tech CSE (AI & Data Science)

- GitHub: [@manojperi26](https://github.com/manojperi26)
- LinkedIn: [manojperi26](https://linkedin.com/in/manojperi26)

---

<p align="center">
  <strong>Built with Python, computer vision, and deep learning.</strong>
</p>
