[readme_md.md](https://github.com/user-attachments/files/34245671/readme_md.md)

# PathSense 👁️🔊

> **Real-time spatial awareness and obstacle warning assistant app for blind and low-vision individuals.**

PathSense is an assistive mobile application designed to enhance safety and mobility for blind and visually impaired users. By combining computer vision, audio classification, and sensor data, PathSense detects obstacles, estimates distance and direction, and delivers clear, timely feedback using spatial audio, text-to-speech, and haptics.

*Important Note: PathSense is an assistive tool designed to complement—not replace—a white cane, guide dog, or Orientation and Mobility (O&M) training.*

---

## 🌟 Key Features

- **Real-Time Obstacle Detection (P0):** Detects static and moving hazards (vehicles, pedestrians, poles, stairs, curbs, drop-offs) at $\ge 15$ FPS using on-device models.
- **Monocular & Hardware Depth Estimation:** Accurately estimates obstacle distance (in meters or steps) and direction (clock positions or relative placement).
- **Ambient Sound Awareness (P1):** Listens for sirens, vehicle horns, and bicycle bells to elevate threat levels when combined with visual cues.
- **Audio & Haptic Feedback System:** Short, non-overloading spoken phrases, spatial 3D audio tones, and distinct vibration pulses.
- **Voice-Driven & Screen-Free Navigation:** Built from the ground up to be fully operable via voice commands and platform screen readers (TalkBack / VoiceOver).
- **Offline-First Architecture:** Core safety detection, speech recognition, and emergency functions run 100% offline.
- **Safety & Fall Detection:** Automatic fall detection, battery warnings, camera blockage alerts, and instant SOS messaging with live location.

---

## 🏗️ Architecture & Tech Stack

### Tech Stack

- **Android (Primary):** Kotlin, CameraX, ARCore Depth API, TensorFlow Lite / ONNX Runtime, Android Foreground Service, Vosk / Whisper-tiny (Offline ASR).
- **iOS (Phase 2):** Swift, AVFoundation, ARKit / LiDAR, Core ML, Core Haptics.
- **Backend Services:** Node.js / Python / Firebase (Auth, cloud vision-language models, SOS routing).

### System Pipeline

```text
[ Camera Feed ] ───► [ Object Detection & Monocular Depth ] ──┐
[ Microphone  ] ───► [ Sound Classification (Horns/Sirens) ] ──┼─► [ Risk & Priority Logic ] ─► [ Audio / Haptics ]
[ Sensors/IMU ] ───► [ Speed & Motion / Fall Detection    ] ──┘
```

---

## 📁 Repository Structure

```text
pathsense/
├── android/                 # Native Android application codebase
│   ├── app/src/main/
│   │   ├── java/com/pathsense/
│   │   │   ├── perception/   # ML models, TFLite integration, depth pipelines
│   │   │   ├── audio/        # Spatial audio generator & TTS engine
│   │   │   ├── haptics/      # Haptic feedback patterns
│   │   │   ├── sensors/      # Accelerometer, step detection, fall risk
│   │   │   └── ui/           # Accessible, high-contrast UI screens
│   │   └── assets/models/    # Quantized TFLite object detection models
├── ios/                     # Native iOS application (Phase 2)
├── backend/                 # Minimal backend for SOS messaging and cloud AI
└── README.md                # Project documentation
```

---

## ⚙️ Performance & Safety Targets

| Metric | Target Standard |
| :--- | :--- |
| **End-to-End Latency** | $< 300\text{ ms}$ (Target: $200\text{ ms}$) |
| **Frame Rate** | $\ge 15\text{ FPS}$ (Mid-range) / $30\text{ FPS}$ (Flagship) |
| **Obstacle Recall** | $\ge 95\%$ for critical path hazards in daylight |
| **Distance Accuracy** | Within $15\%$ error margin up to $5\text{ meters}$ |
| **Battery Draw** | $\le 20\% \text{ per hour}$ in continuous standard mode |
| **App Size** | $< 150\text{ MB}$ (inclusive of local ML models) |

---

## 🚀 Getting Started

### Prerequisites

- **Android:** Android Studio Jellyfish/Ladybug or newer, Android SDK 24+, physical Android test device (4GB+ RAM recommended).
- **iOS (Phase 2):** Xcode 15+, iOS 16+.
- **Backend:** Node.js v18+ and `npm`.

### Installation

1. **Clone the repository:**
   ```bash
   git clone https://github.com/your-username/pathsense.git
   cd pathsense
   ```

2. **Run the Backend (Optional for cloud/SOS functionality):**
   ```bash
   cd backend
   npm install
   npm start
   ```

3. **Build the Android App:**
   - Open the `android/` folder in **Android Studio**.
   - Download/place the quantized models into `app/src/main/assets/models/`.
   - Connect a supported Android device and click **Run**.

---

## 🗣️ Voice Commands Quick Reference

| Command Phrase | Action |
| :--- | :--- |
| `"Start"` / `"Stop"` | Begin or pause real-time obstacle scanning. |
| `"What is in front of me?"` | Requests an on-demand detailed scene description. |
| `"Speech only"` / `"Tones only"` | Switches alert feedback mode. |
| `"Minimal mode"` / `"Detailed mode"`| Adjusts warning verbosity level. |
| `"Help"` | Triggers immediate emergency contact alert with live GPS link. |

---

## 🛡️ Privacy & Security

- **On-Device Data Processing:** Camera and microphone streams are processed strictly in RAM and discarded immediately. No video or voice recordings leave the device by default.
- **Opt-In Cloud Features:** Extended natural-language visual descriptions use opt-in encrypted channels.
- **Anonymized Analytics:** Optional model improvement data is fully anonymized on-device (faces and license plates blurred) before transmission.

---

## 📄 License

This project is licensed under the [MIT License](LICENSE).
