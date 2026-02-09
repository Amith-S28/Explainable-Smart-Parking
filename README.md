# 🧠 Explainable Smart Parking
**An Explainable Temporal–Spatial Deep Learning Framework for Parking Occupancy Forecasting**

This repository contains the full implementation, trained models, and research paper for the project:

> **“An Explainable Temporal–Spatial Deep Learning Framework for Smart Parking Occupancy Forecasting”**  
> *Prakhyat Singh, Sirisilla Jayadevgari Amith, Ankita Wadhawan*  
> Lovely Professional University, Phagwara, Punjab, India  

---

## 🏙️ Overview
This work introduces an **explainable temporal–spatial deep learning framework** for real-time parking occupancy forecasting.  
The system unifies three major components:
1. **YOLOv8n** for spatial detection of occupied/free slots  
2. **LSTM** for temporal forecasting of future parking states  
3. **Explainable AI (XAI)** using **Grad-CAM** and **Integrated Gradients** for transparent model reasoning  

By integrating spatial perception and temporal prediction, the system delivers accurate, interpretable, and real-time parking intelligence suitable for **intelligent transportation systems**.

---

## 🧩 System Architecture
```
┌────────────────────────────┐
│   Input Camera Stream      │
└──────────────┬─────────────┘
               │
               ▼
   ┌────────────────────────┐
   │ YOLOv8n Detector       │ → Slot-level Occupied/Free States
   └────────────┬───────────┘
                │
                ▼
   ┌────────────────────────┐
   │ LSTM Forecaster        │ → Next-frame Occupancy Prediction
   └────────────┬───────────┘
                │
                ▼
   ┌────────────────────────┐
   │ Explainability Module  │
   │  • Grad-CAM (Spatial)  │
   │  • Integrated Gradients│
   │  • Permutation Analysis│
   └────────────────────────┘
```

---

## ⚙️ Model Components

### 🔸 YOLOv8n (Spatial Detection)
- Lightweight single-stage detector for per-slot classification  
- Trained on **CNR-EXT FULL_IMAGE_1000×750** dataset  
- Mean Average Precision (**mAP@0.5**) = **0.995**  
- Precision = **0.996**, Recall = **0.995**  
- Maintains **27 FPS** inference speed on an RTX 3060  
- Spatial explainability through **Grad-CAM** overlays highlighting vehicle regions

### 🔸 LSTM (Temporal Forecasting)
- Input: 5-step historical sequence `[p_occ, hour/23, day/6]`  
- Forecasts one frame ahead per slot  
- Accuracy = **0.91**, F1-Score = **0.93**, Brier Score = **0.065**  
- Well-calibrated probabilities verified via reliability diagrams  
- Temporal explainability via **Integrated Gradients** and **Feature Sensitivity Curves**

### 🔸 Explainable AI (XAI)
- **Grad-CAM:** Localizes spatial features driving YOLO detections  
- **Integrated Gradients:** Quantifies temporal feature contribution across history  
- **Permutation Importance:** Ranks global feature influence (e.g., occupancy > hour > day)

---

## 🧪 Experimental Setup

| Component | Specification |
|------------|---------------|
| **CPU** | AMD Ryzen 9 5900HX |
| **GPU** | NVIDIA RTX 3060 (6 GB VRAM) |
| **RAM** | 16 GB DDR4 |
| **Frameworks** | PyTorch 2.7.1 + cu118, Ultralytics 8.3.223 |
| **OS** | Windows 11 Pro 23H2 |
| **Epochs** | 50 (YOLOv8), 15 (LSTM) |

---

## 📈 Results Summary

| Module | Metric | Score |
|---------|---------|--------|
| **YOLOv8n** | mAP@0.5 | 0.995 |
|  | Precision | 0.996 |
|  | Recall | 0.995 |
| **LSTM** | Accuracy | 0.91 |
|  | F1-Score | 0.93 |
|  | Brier Score | 0.065 |

---

## 🎯 Key Findings
- Integrating LSTM forecasting reduced temporal state oscillations by **22 %** compared to YOLO-only detections.  
- Explainability confirmed that recent occupancy probabilities contribute **>80 %** of forecast influence.  
- The framework sustained real-time inference while providing transparent interpretability.  

---

## 🧠 Explainability Highlights

| Method | Domain | Insight |
|---------|---------|----------|
| **Grad-CAM** | Spatial | Model focuses on car roofs and slot edges during detection |
| **Integrated Gradients** | Temporal | Recent occupancy ($t-1$, $t-2$) dominates prediction |
| **Feature Sensitivity** | Temporal | Hour-of-day encodes cyclic rush-hour patterns |
| **Permutation Importance** | Global | Confirms $p_{occ}$ ≫ time-based features in influence |

---

## 🚀 Quick Start

### 1️⃣ Clone Repository
```bash
git clone https://github.com/Illicitus25/Explainable-Smart-Parking.git
cd Explainable-Smart-Parking
```

### 2️⃣ Install Requirements
```bash
pip install -r requirements.txt
```

### 3️⃣ Run YOLOv8 Detection
```bash
python detect.py --weights model/best.pt --source test_videos/ --conf 0.4
```

### 4️⃣ Run LSTM Forecasting
```bash
python forecast_lstm.py --input detections.csv --horizon 1
```

### 5️⃣ Generate Explainability Visuals
```bash
python explain_xai.py --gradcam --integrated-gradients
```

---

## 📘 Publication
This work is prepared for submission to **IEEE Access** / **IEEE Intelligent Transportation Systems Magazine** — both **Scopus-indexed** venues for AI and Smart City research.  

---

## 🧾 Citation
```bibtex
@article{Singh2025ExplainableParking,
  title={An Explainable Temporal–Spatial Deep Learning Framework for Smart Parking Occupancy Forecasting},
  author={Prakhyat Singh and Sirisilla Jayadevgari Amith and Ankita Wadhawan},
  journal={IEEE Access / IEEE ITS Magazine},
  year={2025}
}
```

---

## 🏁 License
Released under the **MIT License** — free for academic and research use with attribution.

---

## 💬 Contact
📧 **prakhyatsingh0777@gmail.com**  
📍 Lovely Professional University, Phagwara, Punjab, India
📧 **amithsirisilla28@gmail.com**  
📍 Lovely Professional University, Phagwara, Punjab, India

---

**© 2025 Lovely Professional University — All Rights Reserved.**
****
