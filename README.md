# Ali Raza AI — Hand + Voice PC Controller

Control your Windows PC with **hand gestures** and **voice commands** using your **iPhone camera** (clearer than a laptop webcam) and your **microphone**.

**Flow:** iPhone Camera → Wi-Fi/USB video stream → Hand Tracking → Gesture Recognition → PC Action
**Plus:** Microphone → Voice Recognition → Command Detection → PC Action

Both work together in real time. All processing is **local** — no camera or video data is ever sent to external servers.

> This is a **Windows desktop application** (Python). It runs locally on your PC, not in a browser.

## Live site
https://raza077-coder.github.io/alirazaai/

## Features
- **iPhone camera** — IP Webcam / DroidCam / USB UVC, auto-detect, low latency
- **Hand tracking** — 21 landmarks, left/right hand, movement, direction, speed
- **Gesture control** — mouse move, pinch click, drag, right-click, swipes, configurable
- **Voice control** — English + Roman Urdu ("Chrome kholo", "Volume barhao", "Computer lock karo")
- **Gaming mode** — editable gesture→key mapping (Tekken etc.), no hard-coded controls
- **Punch detection** — temporal detector (speed + fist shape), adjustable sensitivity
- **Voice + gesture combo** — "Isay open karo", "Click karo"
- **Safety** — ENABLE/DISABLE, emergency stop Ctrl+Alt+X, voice confirmation for shutdown
- **Full settings** — saved locally in settings.json

## Architecture

```
project/
├── main.py                      # Orchestrator: safety, emergency stop, main loop
├── requirements.txt
├── README.md
├── camera/iphone_camera.py      # iPhone via IP Webcam / DroidCam / USB UVC
├── vision/hand_tracker.py       # MediaPipe hand tracking (21 landmarks, L/R)
├── vision/gesture_detector.py   # Configurable gesture recognition
├── vision/punch_detector.py     # Temporal punch detection (speed + fist shape)
├── voice/speech_recognition.py  # English + Urdu (SpeechRecognition)
├── voice/command_processor.py   # Command parsing + execution
├── control/mouse_controller.py  # pyautogui mouse with smoothing
├── control/keyboard_controller.py # pynput keyboard
├── control/pc_controller.py     # Apps, volume, screenshot, lock, shutdown
├── gaming/game_controller.py    # Editable gesture→key mapping (Tekken etc.)
├── config/settings.json         # All settings (persist across restarts)
├── config/settings_manager.py   # Load/save settings
└── ui/dashboard.py              # Desktop dashboard (Tkinter)
```

## Installation

1. Install **Python 3.9+** (check "Add Python to PATH").
2. Install dependencies:
   ```bash
   cd project
   pip install -r requirements.txt
   ```
   If PyAudio fails on Windows: `pip install pipwin && pipwin install pyaudio`
3. Connect your iPhone (IP Webcam / DroidCam / USB UVC) and set the stream URL in Settings.
4. Run:
   ```bash
   python main.py
   # or the dashboard:
   python ui/dashboard.py
   ```

## Safety
- **Emergency stop:** Ctrl+Alt+X disables all automated control instantly.
- **Enable/Disable** controller button.
- Shutdown/restart require voice confirmation.

## License
Open source. Built by [Ali Raza](https://github.com/Raza077-coder).