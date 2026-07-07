# 🏸 Badminton Footwork Detection & Performance Dashboard

<div align="center">

**An AI-powered end-to-end system that processes raw badminton match videos and transforms them into actionable coaching insights.**

[🚀 Live Demo](https://bappton-dashboard-with-app-ccbaa8jaq4n7ydirsu2vps.streamlit.app/) • [📄 Documentation](#-dashboard-tabs) • [🔧 Installation](#-installation)

**Python 3.11 &nbsp;|&nbsp; YOLOv8 &nbsp;|&nbsp; MediaPipe &nbsp;|&nbsp; Random Forest &nbsp;|&nbsp; Streamlit &nbsp;|&nbsp; SQLite**

</div>

---

## 📌 Overview

The Badminton Footwork Detection & Performance Dashboard is a full-stack AI application that automatically analyses a player's footwork from raw match footage. Upload a video — the system handles everything else:

- **Detects** the player using YOLOv8
- **Tracks** 33 body landmarks using MediaPipe Pose
- **Classifies** footwork/shot type using a trained Random Forest (88.89% accuracy)
- **Scores** performance across 5 biomechanical dimensions
- **Generates** a complete coaching report with strengths, weaknesses, and training recommendations
- **Saves** every session to a SQLite database for long-term progress tracking

---

## 🎯 Key Features

| Feature | Description |
|---|---|
| 🎥 **Player Detection** | YOLOv8 detects and isolates the active player from every frame |
| 🦴 **Pose Estimation** | MediaPipe extracts 33 full-body landmarks per frame |
| 🤖 **Footwork Classification** | Random Forest classifies shot type with 88.89% accuracy |
| 📊 **BPS Score** | Single 0–100 performance score combining 5 weighted efficiency metrics |
| 🗺️ **Court Heatmap** | Position density map + movement trajectory visualisation |
| 🧍 **Player Identity** | Playstyle archetype, dominant side, court preference, style tags |
| 🎯 **Tactical Analysis** | Shot-side breakdown, court depth usage, strengths & weaknesses |
| 🤖 **AI Coach Report** | Written coaching report with 6 expandable sections |
| 📚 **Session History** | SQLite-backed history tab for cross-session comparison |
| ☁️ **Live Deployment** | Deployed on Streamlit Community Cloud — no install needed |

---

## 🏗️ System Architecture

```
Raw Video (.mp4)
      │
      ▼
┌─────────────┐
│  YOLOv8     │  ── Player detection + bounding box
└──────┬──────┘
       │
       ▼
┌─────────────┐
│  MediaPipe  │  ── 33 body landmarks per frame
└──────┬──────┘
       │
       ▼
┌─────────────────────┐
│  Feature Engineering │  ── Speed, acceleration, direction change,
│  (Pandas + NumPy)   │      recovery distance, path efficiency, etc.
└──────┬──────────────┘
       │
       ▼
┌──────────────────┐
│  Random Forest   │  ── Footwork classification (88.89% accuracy)
│  (scikit-learn)  │      Forehand Front | Backhand Front | Recovery Ready
└──────┬───────────┘
       │
       ▼
┌─────────────────────────────────────────────┐
│              Analytics Engine               │
│  BPS Score │ Efficiency Scores │ Grading    │
│  Identity  │ Tactical Analysis │ Coach Report│
└──────┬──────────────────────────────────────┘
       │
       ▼
┌─────────────┐     ┌──────────┐
│  Streamlit  │────▶│  SQLite  │  ── Session history
│  Dashboard  │     │  Database│
└─────────────┘     └──────────┘
```

---

## 🖥️ Dashboard Tabs

### 1. 🎥 Video
Interactive frame inspector with a scrubber slider — view any specific frame with skeleton overlay, bounding box, and the model's per-frame prediction and confidence score.

### 2. 📤 Upload
Upload a raw `.mp4` badminton video to trigger the full pipeline. Real-time progress bar shows each stage: Frames → Landmarks → Features → RF Predictions.

### 3. 📍 Court Intelligence
- Position heatmap (player density across the court)
- Movement trajectory plot
- Front/Mid/Back court time percentage
- 9-zone court grid from RF model predictions

### 4. 📊 Performance Analytics *(Member 2)*
- **Match Overview** — total distance, avg/peak speed, recovery time %
- **Movement Efficiency** — 5 scores (0–100) on a radar chart:
  - **Agility** (25%) — direction change rate
  - **Recovery** (25%) — return-to-base speed
  - **Explosiveness** (20%) — peak acceleration bursts
  - **Consistency** (15%) — movement rhythm stability
  - **Path Efficiency** (15%) — directness of movement routes
- **BPS Score** — weighted composite score out of 100
- **Session Grade** — A+ to D letter grade

### 5. 🧍 Player Identity
Playstyle archetype classification (Defensive Anchor / Aggressive Attacker / All-Court Controller / One-Sided Specialist / Developing Player), dominant side split, court preference, and style descriptor tags.

### 6. 🎯 Tactical Analysis
Forehand vs backhand pie chart, court depth stacked bar, top 3 strengths and weaknesses with blurbs, training priority meter with urgency scores and specific drill suggestions.

### 7. 🤖 AI Coach Report
Six expandable sections: Session Summary, Strength Analysis, Weakness Analysis, Tactical Insights, Recovery Recommendations, and Training Suggestions. Rule-based template engine — deterministic, free, no API key required. Structured for easy LLM swap-in.

### 8. 📚 History
All past sessions retrieved from SQLite database. Compare BPS, grade, and efficiency scores across multiple sessions to track player progress over time.

---

## 🛠️ Tech Stack

### Video Processing & Detection
| Tool | Purpose |
|---|---|
| `OpenCV (cv2)` | Frame extraction, annotated video output |
| `Ultralytics YOLOv8` | Player detection and bounding box generation |
| `imageio-ffmpeg` | H.264 video re-encoding for browser playback |

### Pose Estimation & Feature Engineering
| Tool | Purpose |
|---|---|
| `MediaPipe Pose` | 33 full-body landmark extraction per frame |
| `Pandas` | Per-frame features.csv processing |
| `NumPy` | Landmark math — distances, angles, normalisation |

### Machine Learning
| Tool | Purpose |
|---|---|
| `scikit-learn` | Random Forest classifier (88.89% accuracy) |
| `joblib` | Model serialisation and loading |

### Analytics & Dashboard
| Tool | Purpose |
|---|---|
| `Plotly` | All charts — radar, gauge, heatmap, pie, bar |
| `Streamlit` | Full web dashboard — all 8 tabs |
| `streamlit-option-menu` | Sidebar navigation |

### Storage & Deployment
| Tool | Purpose |
|---|---|
| `SQLite` | Persistent session history database |
| `json / csv` | Shared analytics contract between pipeline modules |
| `Streamlit Community Cloud` | Live public deployment |
| `GitHub` | Version control + auto-deploy on push |

---

## ⚙️ Installation

### Prerequisites
- Python 3.11
- Git

### Steps

```bash
# 1. Clone the repository
git clone https://github.com/your-username/badminton-dashboard.git
cd badminton-dashboard

# 2. Create and activate a virtual environment
python -m venv venv

# Windows
venv\Scripts\activate

# Mac/Linux
source venv/bin/activate

# 3. Install dependencies
pip install -r requirements.txt

# 4. Run the dashboard
streamlit run app.py
```

> **Note:** MediaPipe 0.10.9 is pinned in `requirements.txt` for API compatibility. Do not upgrade without checking the pipeline code.

---

## 📁 Project Structure

```
badminton-dashboard/
│
├── app.py                          # Main Streamlit entry point
├── requirements.txt                # All Python dependencies
├── packages.txt                    # System-level dependencies (cloud)
├── runtime.txt                     # Python version pin (cloud)
│
├── pipeline/
│   └── run_pipeline.py             # Full video → features → predictions pipeline
│
├── sections/
│   ├── video_section.py            # Tab 1: Video + frame inspector
│   ├── upload_section.py           # Tab 2: Upload + pipeline trigger
│   ├── court_section.py            # Tab 3: Court Intelligence
│   ├── performance_section.py      # Tab 4: Performance Analytics (Member 2)
│   ├── identity_section.py         # Tab 5: Player Identity (Member 3)
│   ├── tactical_section.py         # Tab 6: Tactical Analysis (Member 3)
│   ├── coach_report.py             # Tab 7: AI Coach Report (Member 3)
│   └── history_section.py          # Tab 8: Session History
│
├── utils/
│   ├── scoring_engine.py           # BPS, efficiency scores computation
│   ├── grade_engine.py             # BPS → letter grade mapping
│   ├── visualization_utils.py      # Heatmap, trajectory helpers
│   └── session_utils.py            # Session state management
│
├── data/
│   ├── analytics.json              # Shared cross-module analytics contract
│   ├── features.csv                # Per-frame engineered features
│   ├── predictions.csv             # Per-frame RF predictions
│   └── badminton_history.db        # SQLite session history database
│
├── models/
│   └── rf_model.pkl                # Trained Random Forest model
│
└── styling.py                      # Custom dark theme (Oswald/Inter fonts)
```

---

## 📈 Model Performance

| Metric | Value |
|---|---|
| Model Type | Random Forest Classifier |
| Training Features | 53 engineered features from pose landmarks |
| Classes | Forehand Front, Backhand Front, Recovery Ready |
| Accuracy | **88.89%** |
| Feature Importance (top) | court_zone (3.9%), speed, direction_change, recovery_distance |

---

## 🔬 Comparison with Base Paper

This project extends *"A Deep Learning Approach to Badminton Player Footwork Detection Based on YOLO Models"* (ICSIPA 2024):

| Aspect | Base Paper | This Project |
|---|---|---|
| Player Detection | YOLOv8 / YOLOv9 | YOLOv8 ✅ |
| Task | Court corner detection | Full footwork classification |
| Best mAP | 0.633 (YOLOv8) | — (different task) |
| Accuracy | — | **88.89%** (Random Forest) |
| Pose Estimation | ❌ | ✅ MediaPipe (33 landmarks) |
| Performance Scoring | ❌ | ✅ BPS + 5 efficiency metrics |
| Coaching Output | ❌ | ✅ Full written coach report |
| Session History | ❌ | ✅ SQLite database |

---

## 🔮 Future Roadmap

- [ ] **Two-Player Tracking** — simultaneous analysis of both players
- [ ] **Real-Time Live Analysis** — process live camera feed during match
- [ ] **Mobile App** — iOS/Android app with cloud ML backend
- [ ] **Long-Term Progress Tracking** — BPS trend graphs across sessions
- [ ] **LLM Coach Report** — swap rule-based templates for GPT/Gemini
- [ ] **Shot Classification** — smash, drop, clear, drive beyond footwork position
- [ ] **3D Pose Estimation** — depth-aware biomechanical analysis

---

## 👥 Team

| Member | Role |
|---|---|
| **Pranathi** | Video & Court Analytics |
| **Sahana Krithi** | Performance Analytics Lead |
| **Sreeja** | Tactical & AI Coach Lead |

---

## 📄 License

This project was developed as part of a university milestone submission.

---

<div align="center">

**🏸 Turning Every Match into a Learning Opportunity**

*Built with Python • YOLOv8 • MediaPipe • scikit-learn • Streamlit*

</div>
