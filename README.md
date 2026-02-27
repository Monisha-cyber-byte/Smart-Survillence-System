# 🏠 Smart Surveillance Gist System

An AI-powered home surveillance system that transforms traditional CCTV cameras into intelligent security assistants — providing automated visitor identification, behavior analysis, and daily activity summaries instead of raw continuous footage.

---

## 📌 Overview

Traditional CCTV systems are passive recording devices that require manual review of hours of footage. This project addresses that gap by integrating Computer Vision and AI to:

- Automatically detect and recognize visitors
- Distinguish between **known** and **unknown** individuals
- Detect **suspicious behavior** such as loitering or unauthorized backyard entry
- Generate concise **daily summaries** of surveillance activity
- Provide a clean **Streamlit dashboard** for non-technical users

---

## 🧠 Key Features

- **Visitor Identification** — Compares captured faces against a pre-stored database of known persons
- **Behavior Analysis** — Flags loitering or repeated suspicious movements near gate, doorstep, or backyard
- **Daily Summarization** — Auto-generates a gist of all visitor activity with timestamps and entry points
- **Real-Time Alerts** — Instant notifications for unknown individuals or unusual movements
- **Cross-Zone Rules** — Detects events like backyard entry without prior gate detection
- **Mock/Degraded Mode** — Graceful fallback for demo when CV dependencies are unavailable

---

## 🏗️ System Architecture

The system follows a layered modular pipeline:

```
Input (Video Upload)
     ↓
Pre-Processing (Frame extraction, resizing, frame-skipping)
     ↓
Detection Layer (YOLOv5 — person bounding boxes)
     ↓
Tracking Layer (DeepSort — persistent person IDs across frames)
     ↓
Face Recognition (DeepFace/VGG-Face — embedding pool matching)
     ↓
Analysis & Event Layer (Cross-zone rules, alert classification)
     ↓
Output (Streamlit Dashboard — metrics, gallery, alerts, summaries)
```

---

## 📦 Tech Stack

| Component | Technology |
|---|---|
| Programming Language | Python 3.10+ |
| Person Detection | YOLOv5 |
| Multi-Object Tracking | DeepSort |
| Face Recognition | DeepFace (VGG-Face model) |
| Video Processing | OpenCV |
| UI / Dashboard | Streamlit |
| Database | SQLite / JSON-based store |
| Optional Deployment | Ngrok / Flask |

---

## 💻 Hardware Requirements

| Component | Specification |
|---|---|
| Processor | Intel i5 / AMD Ryzen 5 or higher |
| RAM | 8 GB minimum (16 GB recommended) |
| Storage | 20 GB free space minimum |
| GPU | T4 GPU with CUDA support (recommended) |
| Camera / Input | HD camera or pre-recorded `.mp4` video files |
| Display | 1366 × 768 resolution minimum |

---

## 🚀 Getting Started

### Prerequisites

```bash
# Python 3.10 or higher required
python --version

# Install dependencies
pip install -r requirements.txt
```

### Installation

```bash
# Clone the repository
git clone https://github.com/your-username/smart-surveillance-gist-system.git
cd smart-surveillance-gist-system

# Install required packages
pip install -r requirements.txt
```

### Running the Application

```bash
streamlit run app.py
```

Then open your browser at `http://localhost:8501`.

---

## 🗂️ Module Overview

| Module | Description |
|---|---|
| **Video Input** | Handles `.mp4` uploads for Gate, Doorstep, and Backyard zones |
| **Pre-processing** | Frame extraction, resizing, blank-frame removal, frame-skip logic |
| **Detection** | YOLOv5 person detection with confidence & area-based filtering |
| **Tracking** | DeepSort multi-person tracking with consistent ID assignment |
| **Face Recognition** | DeepFace embedding pool for known/unknown identity matching |
| **Alert Generation** | Cross-zone rule engine classifying events as normal, suspicious, or intrusion |
| **Dashboard** | Streamlit UI with visitor log, face gallery, alerts, and summaries |

---

## 📋 Scope

### ✅ In Scope (Current MVP)
- Multi-zone offline analysis using uploaded video files (Roadside Gate, Front Door, Backyard)
- Person detection and identity tracking via YOLO + DeepSort
- Face embedding extraction and similarity-based matching
- Cross-zone intrusion rule checks
- Streamlit dashboard with login, metrics, gallery, and alert management
- Performance optimizations: frame skipping, embedding rate limiting, IOU-based suppression

### ❌ Out of Scope (Future Work)
- Live camera streaming / IP camera integration
- Production-grade authentication and encrypted data storage
- On-device model training or fine-tuning
- GPU orchestration or horizontal scaling
- Advanced privacy features (GDPR tooling, encrypted face templates)
- Heavy occlusion or extreme low-light edge case handling

---

## ⚙️ Configuration

Key parameters can be tuned in the config file:

```python
FRAME_SKIP_RATE = 10          # Process every Nth frame
EMBEDDING_UPDATE_RATE = 50    # Throttle embedding updates
MIN_BOX_AREA = <threshold>    # Filter out small/noisy detections
EMBEDDING_POOL_SIZE = <n>     # Number of embeddings stored per unique ID
```

---

## 📈 Success Criteria

The system is considered successful when:
- Multi-zone video uploads produce a coherent set of unique person IDs with a first-seen crop gallery
- Cross-zone rules trigger meaningful alerts (e.g., backyard detection without roadside gate entry)
- End-users can upload videos, run analysis, view results, and resolve alerts without developer intervention
- Filtering and pooling strategies demonstrate a measurable reduction in false positives over naïve motion detection

---

## 📚 References

1. Tharun Esta — [AI CCTV Surveillance System using YOLOv8 + DeepSORT](https://github.com/TharunEsta/AI-CCtv-surveilence-and-face-detection)
2. K. S. Rani et al. — [Enhancing Surveillance and Face Recognition with YOLO-Based Object Detection](https://link.springer.com/chapter/10.1007/978-981-99-3982-4_32), Springer, 2024
3. London Journal of Engineering Research — [Smart Surveillance System using Deep Learning](https://journalspress.com/LJER_Volume22/Smart-Surveillance-System-using-Deep-Learning.pdf), Vol. 22, 2023

---

## 🔮 Future Enhancements

- Real-time alert integration with mobile applications
- Advanced crowd and loitering detection
- Automated report generation and email notifications
- Integration with live IP cameras and NAT traversal support
- Scalable backend with GPU orchestration

---
