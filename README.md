# Face Detection using OpenCV and dlib

This Python script demonstrates real-time face detection using OpenCV and the dlib library. It captures video from your computer's default camera, detects faces in each frame, and draws bounding boxes around the detected faces.

## Prerequisites
- Python
- OpenCV
- dlib
- A webcam or built-in camera on your computer

## Installation

To run this script, you need to have Python installed. You can install the required libraries using `pip`:

```bash
pip install opencv-python dlib
```

## Usage

1. Clone or download this repository to your local machine.

2. Open a terminal and navigate to the directory containing the script.

3. Run the script using the following command:

```bash
python face_detection.py
```

4. The script will open a window showing the video feed from your camera. It will start detecting faces in real-time.

5. To exit the application, press the 'q' key on your keyboard.

## Explanation

The script consists of the following parts:

1. Importing the necessary libraries:

```python
import cv2
import numpy as np
import dlib
```

2. Connecting to the default camera:

```python
cap = cv2.VideoCapture(0)
```

3. Creating a face detector object using dlib:

```python
detector = dlib.get_frontal_face_detector()
```

4. Capturing frames continuously and processing them for face detection:

```python
while True:
    ret, frame = cap.read()
    frame = cv2.flip(frame, 1)

    gray = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)
    faces = detector(gray)

    i = 0
    for face in faces:
        # Detect faces, draw bounding boxes, and label them
        x, y = face.left(), face.top()
        x1, y1 = face.right(), face.bottom()
        cv2.rectangle(frame, (x, y), (x1, y1), (0, 255, 0), 2)
        i = i + 1
        cv2.putText(frame, 'face num' + str(i), (x - 10, y - 10), cv2.FONT_HERSHEY_SIMPLEX, 0.7, (0, 0, 255), 2)
        print(face, i)

    cv2.imshow('frame', frame)

    if cv2.waitKey(1) & 0xFF == ord('q'):
        break
```

5. Releasing the camera and closing the window when the 'q' key is pressed:

```python
cap.release()
cv2.destroyAllWindows()
```

The script continuously captures frames from your camera, converts them to grayscale, and detects faces using dlib's face detector. It then draws bounding boxes around the detected faces and labels them with a numerical identifier. Pressing 'q' closes the application.

Enjoy experimenting with face detection using OpenCV and dlib!
