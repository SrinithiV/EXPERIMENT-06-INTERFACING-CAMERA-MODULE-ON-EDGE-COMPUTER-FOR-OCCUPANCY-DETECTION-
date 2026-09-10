# EXPERIMENT-06-INTERFACING-CAMERA-MODULE-ON-EDGE-COMPUTER-FOR-OCCUPANCY-DETECTION-
## Name: SRINITHI V
## Dept. : CSE(IoT)
## REG NO: 212223115003

### AIM:
To interface a USB/CSI camera module with an edge computing platform (e.g., Raspberry Pi, Jetson Nano, etc.) and implement an occupancy detection system using the Histogram of Oriented Gradients (HOG) algorithm.

### Apparatus/Software Required:
S. No.	Equipment / Software	Specification
1.	Edge Computing Device	Raspberry Pi 4 / Jetson Nano
2.	Camera Module	USB Webcam / Pi Camera Module
3.	Operating System	Raspbian OS / Ubuntu
4.	Programming Language	Python 3.x
5.	Libraries	OpenCV, imutils, NumPy
6.	Display Output	HDMI Monitor / VNC Viewer

### Theory:
Histogram of Oriented Gradients (HOG) is a feature descriptor used in computer vision and image processing for the purpose of object detection. It counts occurrences of gradient orientation in localized portions of an image. HOG descriptors are particularly useful for detecting humans (pedestrians) in static images or video frames.

Steps involved in HOG-based Occupancy Detection:

Capture frames from the camera.

Resize and preprocess the image.

Use a pre-trained HOG descriptor with a linear SVM to detect people in the image.

Annotate the image with bounding boxes where people are detected.

Display or store the result.

Circuit Diagram / Setup:
Connect the USB camera to the edge computer via a USB port.

Power on the edge device and boot into the OS.

Ensure necessary Python libraries are installed.

### Procedure:
Set up the edge device with a monitor or SSH/VNC connection.

Connect and verify the camera using commands like ls /dev/video* or vcgencmd get_camera.

Install required libraries:

bash
Copy
Edit
pip install opencv-python imutils numpy
Write the Python code to initialize the camera and implement the HOG algorithm.

Run the code and verify that the system detects human presence and draws bounding boxes.

 ###  Python Code:
 
import cv2
import imutils

###  Initialize HOG descriptor with people detector
hog = cv2.HOGDescriptor()
hog.setSVMDetector(cv2.HOGDescriptor_getDefaultPeopleDetector())

### Initialize video capture
cap = cv2.VideoCapture(0)  # Change index if using CSI camera

while True:
    ret, frame = cap.read()
    if not ret:
        break

 ### Resize frame for faster processing
    frame = imutils.resize(frame, width=640)

 ### Detect people in the image
    (rects, weights) = hog.detectMultiScale(frame, winStride=(4, 4),
                                            padding=(8, 8), scale=1.05)

 ### Draw bounding boxes
    for (x, y, w, h) in rects:
        cv2.rectangle(frame, (x, y), (x + w, y + h), (0, 255, 0), 2)

 ### Display the result
    cv2.imshow("Occupancy Detection", frame)

###  Exit on pressing 'q'
    if cv2.waitKey(1) & 0xFF == ord('q'):
        break

cap.release()
cv2.destroyAllWindows()

### SCREEN SHOTS OF OUTPUT 

<img width="1600" height="900" alt="WhatsApp Image 2026-08-28 at 4 25 34 PM" src="https://github.com/user-attachments/assets/0faaa42d-b5c0-4bed-8182-e7a834956657" />

### RASPI INTERFACE 

<img width="960" height="1280" alt="image" src="https://github.com/user-attachments/assets/f273d00d-b4c0-438a-a706-d7d5ba8f6ca8" />

### Result:
Occupancy detection using the HOG algorithm was successfully implemented. The system was able to identify and highlight human presence in real-time video streams.
