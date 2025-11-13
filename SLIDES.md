# 🚘 Driver Drowsiness Detection System
### AI-Powered Driver Safety Monitoring

**Harshith Pabbati**

---

## 🎯 The Problem

**Road accidents due to driver drowsiness are a critical safety concern:**

- 💤 Drowsiness causes 20% of all traffic accidents
- 😴 Fatigue-related crashes result in 1,550 deaths annually (US)
- ⏰ Most common during early morning and late night hours
- 🚫 Often goes undetected until it's too late

**We need a real-time solution to detect and alert drowsy drivers!**

---

## 💡 Our Solution

**A real-time AI-powered safety monitoring system** using computer vision and deep learning:

### Core Technologies:
- 🎥 **Computer Vision**: OpenCV + MediaPipe Face Mesh
- 🧠 **Machine Learning**: Real-time landmark detection (478 facial points)
- 🖥️ **Dual Interface**: CLI + Streamlit Web App
- 📊 **Multi-metric Analysis**: Comprehensive driver state monitoring

### Key Innovation:
**Non-intrusive, camera-based monitoring** - no wearables required!

---

## ✨ Key Features

### 👁️ Eye & Gaze Monitoring
- **Eye Aspect Ratio (EAR)** detection for drowsiness
- **PERCLOS Score** - industry standard metric
- **Iris tracking** for accurate gaze estimation
- **Blink rate monitoring** (normal: 12-25/min)

### 🧑 Head & Body Tracking
- **3D Head Pose** estimation (roll, pitch, yaw)
- **Distraction detection** when looking away
- **Posture analysis** for side-view monitoring
- **Yawn detection** using Mouth Aspect Ratio

### 🚨 Advanced Safety
- **Multi-level alerts** (drowsy, asleep, distracted, yawning)
- **Crash detection** via optical flow analysis
- **Audio alarms** for critical situations
- **Screenshot capture** for incident logging

---

## 🏗️ System Architecture

```
Input (Webcam/Camera/Video)
          ↓
MediaPipe Face Mesh (478 landmarks)
          ↓
    ┌─────┴─────┬─────────────┐
    ↓           ↓             ↓
Eye Detector  Head Pose   Posture
(EAR/Gaze)   (3D Orient)  (Pose Model)
    ↓           ↓             ↓
    └─────┬─────┴─────────────┘
          ↓
  Attention Scorer + Alert System
          ↓
   Real-time UI Display
```

**Real-time processing** with optimized pipeline for <30ms latency

---

## 📊 Detection Capabilities

### Alert Levels:
| Alert | Trigger | Action |
|-------|---------|--------|
| 🟡 **DROWSY** | PERCLOS threshold exceeded | Warning sound |
| 🔴 **ASLEEP** | Eyes closed >2 seconds | Loud alarm + screenshot |
| 🟠 **LOOK AWAY** | Gaze off-road >2 seconds | Alert sound |
| 🟣 **DISTRACTED** | Head turned >20° for >2.5s | Warning |
| 🥱 **YAWNING** | Mouth open >1.5 seconds | Fatigue warning |
| 👀 **ABNORMAL BLINK** | Unusual frequency | Alert |
| 💥 **CRASH** | Sudden deceleration | Emergency alert |

### Adjustable Thresholds:
- Configurable sensitivity for different driving conditions
- Customizable time windows and alert parameters

---

## 🚀 Usage & Demo

### CLI Mode:
```bash
python main.py --camera 0
```

### Web Interface:
```bash
streamlit run app.py
```

**Live Dashboard Features:**
- ✅ Real-time video feed with overlay annotations
- 📈 Live metrics (FPS, alert count, blink rate)
- 🎨 Visual indicators for each alert type
- 📸 Screenshot gallery of all incidents
- ⚙️ Easy configuration via sidebar

**System Requirements:** Python 3.8+, Webcam, works on CPU or GPU

---

## 📈 Results & Impact

### Performance Metrics:
- ⚡ **Real-time processing**: 30+ FPS on standard hardware
- 🎯 **Accuracy**: High precision with MediaPipe landmarks
- 🔄 **Reliability**: Continuous monitoring without interruption
- 💾 **Lightweight**: Runs efficiently on standard laptops

### Real-world Applications:
- 🚛 Commercial trucking fleets
- 🚕 Ride-sharing services (Uber, Lyft)
- 🚗 Personal vehicle safety systems
- 🏢 Corporate driver safety programs

**Potential to save lives by preventing drowsy driving accidents!**

---

## 🔮 Future Work

### Planned Enhancements:
- 📱 **Mobile app** integration for broader accessibility
- ☁️ **Cloud analytics** for fleet management
- 🤖 **Deep learning models** for improved accuracy
- 🔊 **Voice alerts** with personalized messages
- 📊 **Driver behavior analytics** dashboard
- 🌐 **Multi-camera support** for comprehensive monitoring
- 🔗 **Vehicle integration** (CAN bus, dashboard displays)

### Research Directions:
- Personalized threshold adaptation based on individual baselines
- Integration with autonomous vehicle systems
- Predictive drowsiness detection using historical patterns

---

## 🙏 Thank You!

### 🚘 Driver Drowsiness Detection System
**Making roads safer with AI**

---

**Questions?**

📧 Contact: [GitHub Repository](https://github.com/harshithpabbati/hci)

🔗 **Tech Stack:** Python | OpenCV | MediaPipe | Streamlit | PyGame

⭐ **Open Source** - MIT License

---

## 📚 References & Resources

### Key Technologies:
- **MediaPipe Face Mesh**: Google's real-time face landmark detection
- **OpenCV**: Computer vision library for image processing
- **Streamlit**: Interactive web application framework

### Research Basis:
- Eye Aspect Ratio (EAR) for drowsiness detection
- PERCLOS (Percentage of Eye Closure) - NHTSA standard
- Head Pose Estimation using PnP algorithm
- Optical flow for crash detection

### Installation:
```bash
git clone https://github.com/harshithpabbati/hci.git
cd hci
pip install -r requirements.txt
python main.py
```

**Start building safer driving experiences today!**
