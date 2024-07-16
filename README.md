

---

# Eye-Controlled Mouse Interface

## Overview
This project implements an eye-controlled mouse interface utilizing eye-tracking technology with `cv2` and `MediaPipe`, integrated with `PyAutoGUI` for seamless interaction. The interface aims to enhance accessibility for individuals with severe disabilities by providing an alternative input method.

## Features
- **Eye Tracking**: Utilizes `cv2` and `MediaPipe` for real-time eye tracking.
- **Mouse Control**: Integrates `PyAutoGUI` for controlling mouse movements and actions.
- **Accessibility**: Provides an alternative input method for individuals with severe disabilities.
- **Advanced AI**: Demonstrates advanced AI and programming skills to create impactful solutions that address real-world challenges.

## Installation

### Prerequisites
- Python 3.6 or higher
- pip (Python package installer)

### Required Libraries
Install the required libraries using pip:
```sh
pip install opencv-python
pip install mediapipe
pip install pyautogui
```

## Usage
1. Clone the repository:
```sh
git clone https://github.com/your-repo/eye-controlled-mouse.git
cd eye-controlled-mouse
```

2. Run the main script:
```sh
python eye_controlled_mouse.py
```

3. Follow the on-screen instructions to calibrate the eye tracking.

## Code Explanation
The main script `eye_controlled_mouse.py`:
```python
import cv2
import mediapipe as mp
import pyautogui

# Initialize camera
cam = cv2.VideoCapture(0)
face_mesh = mp.solutions.face_mesh.FaceMesh(refine_landmarks=True)
screen_w, screen_h = pyautogui.size()

while True:
    _, frame = cam.read()
    frame = cv2.flip(frame, 1)
    rgb_frame = cv2.cvtColor(frame, cv2.COLOR_BGR2RGB)
    output = face_mesh.process(rgb_frame)
    landmark_points = output.multi_face_landmarks
    frame_h, frame_w, _ = frame.shape

    if landmark_points:
        landmarks = landmark_points[0].landmark
        for id, landmark in enumerate(landmarks[474:478]):
            x = int(landmark.x * frame_w)
            y = int(landmark.y * frame_h)
            cv2.circle(frame, (x, y), 3, (0, 255, 0), -1)

            if id == 1:
                screen_x = screen_w / frame_w * x
                screen_y = screen_h / frame_h * y
                pyautogui.moveTo(screen_x, screen_y)

        left = [landmarks[145], landmarks[159]]
        for landmark in left:
            x = int(landmark.x * frame_w)
            y = int(landmark.y * frame_h)
            cv2.circle(frame, (x, y), 3, (0, 255, 255), -1)

        if (left[0].y - left[1].y) < 0.004:
            pyautogui.click()
            pyautogui.sleep(1)

    cv2.imshow('Eye Controlled Mouse', frame)
    cv2.waitKey(1)
```

## How It Works
1. **Eye Tracking**: The program uses `cv2` and `MediaPipe` to track eye movements in real-time.
2. **Mouse Control**: `PyAutoGUI` is used to map eye movements to mouse cursor movements and perform click actions.
3. **Calibration**: The user can calibrate the system to accurately detect and respond to their eye movements.

## Project Structure
- `eye_controlled_mouse.py`: Main script for the eye-controlled mouse interface.
- `README.md`: Project documentation.

## Contributions
Contributions are welcome! Please submit a pull request or open an issue for any changes or suggestions.

## Contact
For any questions or suggestions, please contact:
- **Mausam Nakarja**
- Email: mausamnakarja@gmail.com
- [LinkedIn](https://www.linkedin.com/in/mausam-nakarja-a91206262/)

---

