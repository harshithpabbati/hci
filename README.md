# 🚘 Driver Drowsiness Detection System

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue.svg)](https://www.python.org/)
[![OpenCV](https://img.shields.io/badge/OpenCV-4.11-green.svg)](https://opencv.org/)
[![MediaPipe](https://img.shields.io/badge/MediaPipe-Latest-orange.svg)](https://mediapipe.dev/)
[![Streamlit](https://img.shields.io/badge/Streamlit-1.44-red.svg)](https://streamlit.io/)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

A real-time AI-powered driver safety monitoring system that detects drowsiness, distraction, and poor posture to prevent accidents. Built with computer vision and deep learning technologies.

## 📊 Presentation Materials

**3-minute presentation slides available!** Perfect for demos, talks, and project showcases:

- **[SLIDES.md](SLIDES.md)**: Markdown presentation with all content organized in slide format
- **[presentation.html](presentation.html)**: Interactive HTML presentation using Reveal.js (open in browser)
- **[PRESENTATION_README.md](PRESENTATION_README.md)**: Complete usage guide and presentation tips

## ✨ Features

### 🎯 Core Detection Capabilities

#### **Face & Eye Monitoring (Front View)**
- **Eye Aspect Ratio (EAR) Detection**: Monitors eye closure to detect drowsiness
- **PERCLOS Score**: Percentage of Eye Closure - industry-standard drowsiness metric
- **Gaze Tracking**: Detects when driver is looking away from the road
- **Iris Landmark Detection**: Precise pupil tracking for accurate gaze estimation
- **Real-time Eye Processing**: Optional visualization of eye region analysis
- **Blink Rate Monitoring**: Tracks blink frequency to detect abnormal patterns indicating fatigue
  - Normal range: 12-25 blinks per minute
  - Alerts on abnormally high or low rates

#### **Head Pose Estimation**
- **3D Head Orientation**: Tracks roll, pitch, and yaw angles
- **Distraction Detection**: Identifies when the driver's head is turned away
- **Visual Axis Display**: Optional 3D axis overlay showing head orientation
- **Camera Calibration Support**: Uses custom camera parameters for improved accuracy

#### **Fatigue Detection**
- **Yawn Detection**: Monitors mouth opening using Mouth Aspect Ratio (MAR)
  - Detects prolonged mouth opening (>1.5 seconds)
  - Tracks yawn frequency for fatigue assessment
  - Strong indicator of driver drowsiness

#### **Crash Detection**
- **Motion-based Analysis**: Uses optical flow to detect sudden deceleration
- **Real-time Motion Tracking**: Monitors frame-to-frame movement patterns
- **Sudden Stop Detection**: Alerts when significant motion suddenly drops to near-zero
- **Visual Feedback**: Displays motion vectors and magnitude on screen
- **Configurable Sensitivity**: Adjustable motion threshold for different environments

#### **Posture Analysis (Side View)**
- **Back Posture Classification**: Detects reclined or slouched positions
- **Arm Extension Monitoring**: Identifies overextended or improper arm positions
- **MediaPipe Pose Integration**: Full-body landmark detection
- **Real-time Posture Feedback**: Visual indicators for correct/incorrect posture

#### **Alert System**
- **Multi-level Alerts**:
  - 🟡 **DROWSY**: PERCLOS threshold exceeded
  - 🔴 **ASLEEP**: Extended eye closure detected
  - 🟠 **LOOK AWAY**: Gaze diverted from road
  - 🟣 **DISTRACTED**: Head pose threshold exceeded
  - 🥱 **YAWNING**: Prolonged mouth opening detected
  - 👀 **ABNORMAL BLINK RATE**: Unusual blink frequency
  - 💥 **CRASH DETECTED**: Sudden deceleration detected
- **Audio Alarms**: Pygame-based sound alerts for critical conditions
- **Screenshot Capture**: Automatic screenshot when alerts are triggered
- **Alert Gallery**: Historical view of all captured alert events

## 🏗️ System Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                     Input Sources                            │
│  (Webcam / External Camera / Video File)                     │
└────────────────┬────────────────────────────────────────────┘
                 │
                 ▼
┌─────────────────────────────────────────────────────────────┐
│              MediaPipe Face Mesh                             │
│  • 478 Facial Landmarks (468 face + 10 iris)                │
│  • Real-time landmark detection                              │
└────────────────┬────────────────────────────────────────────┘
                 │
      ┌──────────┴──────────┬─────────────────┐
      ▼                     ▼                  ▼
┌─────────────┐   ┌─────────────────┐   ┌──────────────┐
│ Eye Detector│   │ Head Pose       │   │ Posture      │
│  • EAR      │   │ Estimator       │   │ Classifier   │
│  • Gaze     │   │ • Roll/Pitch/Yaw│   │ • Pose Model │
└──────┬──────┘   └────────┬────────┘   └──────┬───────┘
       │                   │                    │
       └───────────┬───────┴──────────┬─────────┘
                   ▼                  ▼
           ┌────────────────┐  ┌─────────────┐
           │ Attention      │  │ Alert       │
           │ Scorer         │  │ System      │
           └────────┬───────┘  └──────┬──────┘
                    │                 │
                    ▼                 ▼
           ┌─────────────────────────────┐
           │    UI Layer (CLI/Web)       │
           │  • Real-time Display        │
           │  • Metrics & Visualization  │
           └─────────────────────────────┘
```

## 📦 Installation

### Prerequisites
- Python 3.8 or higher
- Webcam or external camera
- (Optional) GPU for faster processing

### Steps

1. **Clone the repository**
```bash
git clone https://github.com/harshithpabbati/hci.git
cd hci
```

2. **Create a virtual environment** (recommended)
```bash
python -m venv venv

# On Windows
venv\Scripts\activate

# On macOS/Linux
source venv/bin/activate
```

3. **Install dependencies**
```bash
pip install -r requirements.txt
```

## 🚀 Usage

### CLI Mode (Recommended for Testing)

**Basic usage with default settings:**
```bash
python main.py
```

**With custom camera:**
```bash
python main.py --camera 1
```

**With camera calibration file:**
```bash
python main.py --camera_params assets/camera_params.json
```

**With custom thresholds:**
```bash
python main.py --ear_thresh 0.2 --gaze_thresh 0.02 --pose_time_thresh 3.0
```

**Enable/disable specific features:**
```bash
# Disable crash detection
python main.py --enable_crash_detection False

# Adjust crash detection sensitivity
python main.py --crash_motion_thresh 20.0

# Adjust yawn detection threshold
python main.py --yawn_thresh 0.7
```

**Enable debug visualization:**
```bash
python main.py --show_eye_proc True --show_axis True --verbose True
```

### Streamlit Web Interface

**Launch the web app:**
```bash
streamlit run app.py
```

Then open your browser to `http://localhost:8501`

**Features:**
- Use the sidebar to switch between Front View, Side View, and Alerts Gallery
- Click "Start Camera" to begin monitoring
- Click "Stop Camera" to end the session
- Real-time metrics: FPS, frame count, alerts, yawn count, blink rate
- Screenshots are automatically saved to `screenshots/` directory
- View all captured alerts in the Gallery tab
- Monitor crash detection with motion visualization

## ⚙️ Configuration

### Command-Line Arguments

#### Core Detection Parameters

| Argument | Type | Default | Description |
|----------|------|---------|-------------|
| `--camera` | int | 0 | Camera device number (0 for webcam) |
| `--camera_params` | str | None | Path to camera calibration JSON file |
| `--ear_thresh` | float | 0.15 | Eye Aspect Ratio threshold for drowsiness |
| `--ear_time_thresh` | float | 2.0 | Seconds of low EAR before "ASLEEP" alert |
| `--gaze_thresh` | float | 0.015 | Gaze deviation threshold |
| `--gaze_time_thresh` | float | 2.0 | Seconds of gaze deviation before alert |
| `--roll_thresh` | float | 20.0 | Head roll angle threshold (degrees) |
| `--pitch_thresh` | float | 20.0 | Head pitch angle threshold (degrees) |
| `--yaw_thresh` | float | 20.0 | Head yaw angle threshold (degrees) |
| `--pose_time_thresh` | float | 2.5 | Seconds of pose threshold before alert |
| `--show_fps` | bool | True | Display FPS counter |
| `--show_proc_time` | bool | True | Display processing time |
| `--show_eye_proc` | bool | False | Show eye processing windows |
| `--show_axis` | bool | True | Show head pose 3D axis |
| `--verbose` | bool | False | Print detailed debug information |

#### Advanced Features

| Argument | Type | Default | Description |
|----------|------|---------|-------------|
| `--enable_crash_detection` | bool | True | Enable crash detection using motion analysis |
| `--crash_motion_thresh` | float | 15.0 | Motion change threshold for crash detection |
| `--enable_yawn_detection` | bool | True | Enable yawn detection for fatigue monitoring |
| `--yawn_thresh` | float | 0.6 | Mouth Aspect Ratio threshold for yawn detection |
| `--enable_blink_rate` | bool | True | Enable blink rate monitoring |

### Camera Calibration

For improved accuracy, you can provide camera calibration parameters:

**Example `camera_params.json`:**
```json
{
  "camera_matrix": [
    [800, 0, 320],
    [0, 800, 240],
    [0, 0, 1]
  ],
  "dist_coeffs": [0, 0, 0, 0, 0]
}
```

## 🔬 How It Works

### Eye Aspect Ratio (EAR)
The EAR is calculated using eye landmark distances:
```
EAR = (||p2 - p6|| + ||p3 - p5||) / (2 * ||p1 - p4||)
```
Where p1-p6 are eye landmarks. Lower EAR values indicate closed eyes.

### PERCLOS (Percentage of Eye Closure)
Industry-standard drowsiness metric that measures the percentage of time eyes are closed over a rolling time window (default: 60 seconds).

### Head Pose Estimation
Uses solvePnP algorithm to estimate 3D head orientation from 2D facial landmarks:
- **Roll**: Head tilt left/right
- **Pitch**: Head nod up/down
- **Yaw**: Head turn left/right

### Attention Scoring
Combines multiple metrics with time-based smoothing:
- Accumulates time when conditions are met (eyes closed, looking away, etc.)
- Applies decay factor when conditions are not met
- Triggers alerts when accumulated time exceeds thresholds

## 📁 Project Structure

```
hci/
├── app.py                  # Streamlit web application
├── main.py                 # CLI application
├── arg_parser.py          # Command-line argument parser
├── attention_scorer.py    # Attention/drowsiness scoring logic
├── eye_detector.py        # Eye detection and EAR calculation
├── pose_estimation.py     # Head pose estimation
├── posture.py             # Body posture classification
├── crash_detector.py      # Crash detection using optical flow
├── yawn_detector.py       # Yawn detection for fatigue monitoring
├── blink_rate_monitor.py  # Blink rate monitoring
├── face_geometry.py       # 3D face geometry utilities
├── metric_landmarks.py    # Facial landmark metrics
├── utils.py               # Utility functions
├── requirements.txt       # Python dependencies
├── SLIDES.md              # Markdown presentation slides (3-min)
├── presentation.html      # Interactive HTML presentation (Reveal.js)
├── PRESENTATION_README.md # Presentation usage guide
├── assets/
│   ├── alarm.mp3         # Alert sound file
│   └── camera_params.json # Camera calibration parameters
├── screenshots/           # Auto-generated alert screenshots
└── README.md             # This file
```
