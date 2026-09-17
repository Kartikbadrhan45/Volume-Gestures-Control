# Volume-Gestures-Control
# 🖐️ Hand Gesture Master Volume Controller

An interactive computer vision application that dynamically controls system master volume on Windows using real-time hand pinch gestures via **OpenCV**, **MediaPipe (Tasks Vision)**, and **Pycaw**.

---

## 🌟 Key Features

- **⚡ Real-Time Gesture Tracking**: Uses MediaPipe's `HandLandmarker` model to compute Euclidean distances between the thumb tip (Landmark 4) and index finger tip (Landmark 8).
- **🔊 Direct System Audio Integration**: Controls Windows master volume natively via Pycaw scalar endpoints (`0.0` to `1.0`).
- **🤖 Automatic Model Management**: Automatically downloads the required `hand_landmarker.task` file from Google's mirror on first launch if not present locally.
- **📊 Live Visual HUD**: Renders real-time landmark skeletons along with an on-screen volume bar and percentage indicator.

---

## 🛠️ System Architecture & Mapping

```text
  [ Webcam Feed ] ──> [ MediaPipe HandLandmarker ] ──> [ Extract Landmarks #4 & #8 ]
                                                                   │
                                                                   ▼
  [ Windows Master Volume ] <── [ Pycaw Scalar API ] <── [ Map Euclidean Distance ]
   (0% - 100% Volume)           (0.0 to 1.0)               (20px - 180px range)
Distance Calculation: The spatial distance ($d = \sqrt{(x_2 - x_1)^2 + (y_2 - y_1)^2}$) between finger tips is computed per frame.Scalar Normalization: The pixel distance is mapped from $[20, 180]$ pixels to a normalized audio range of $[0.0, 1.0]$.Volume Application: Pycaw's SetMasterVolumeLevelScalar adjusts the Windows Core Audio API endpoints smoothly in real time.📋 Prerequisites & CompatibilityOperating System: Windows 10 / 11 (Pycaw depends on Windows Core Audio APIs)Python Version: Python 3.8 – 3.11Hardware: Standard USB or built-in Webcam🚀 Quick Start Guide1. Clone the RepositoryBashgit clone [https://github.com/your-username/gesture-volume-control.git](https://github.com/your-username/gesture-volume-control.git)
cd gesture-volume-control
2. Set Up Virtual EnvironmentOn Windows:DOSpython -m venv venv
venv\Scripts\activate
3. Install DependenciesBashpip install opencv-python mediapipe pycaw comtypes numpy
requirements.txt contents:Plaintextopencv-python>=4.8.0
mediapipe>=0.10.0
pycaw>=20230407
comtypes>=1.2.0
numpy>=1.24.0
4. Run the ApplicationBashpython app.py
Exit App: Press q while focusing on the video preview window to terminate the camera feed and release hardware resources gracefully.🎮 How to Control VolumeGesture / ActionResultBring Thumb & Index togetherDecreases system volume toward 0% (Mute)Pinch open / Spread fingers apartIncreases system volume up to 100%Press 'q' keyExits the program📂 Project StructurePlaintextgesture-volume-control/
├── app.py                  # Main program script
├── hand_landmarker.task    # Auto-downloaded MediaPipe Vision model file
├── requirements.txt        # Python dependency list
└── README.md               # Documentation
📜 LicenseDistributed under the MIT License. See LICENSE for more information.
