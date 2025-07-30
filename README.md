Real-Time Object Detection Application
This project showcases a robust real-time object detection application developed in Python, designed to identify and localize objects within live video streams. Leveraging cutting-edge deep learning and computer vision techniques, it provides immediate visual insights into dynamic environments.

Overview
The application processes video footage frame by frame, applying a pre-trained YOLOv5 model to detect various objects. The detected objects are then highlighted with bounding boxes and displayed in real-time, offering an intuitive and dynamic visualization of object presence and location. This project emphasizes efficiency and practical application, making it suitable for a range of real-world scenarios.

Features
Instantaneous Object Detection: Identifies and localizes multiple objects in video streams with minimal latency, crucial for real-time applications.

High-Performance Model Integration: Utilizes the highly optimized YOLOv5s model from Ultralytics, known for its balance of speed and accuracy.

Versatile Video Input: Capable of processing pre-recorded video files, easily adaptable for live camera feeds (e.g., webcam, CCTV).

Clear Visual Output: Renders bounding boxes and detection results directly onto the video frames using OpenCV for intuitive interpretation.

Pythonic & Modular Design: Built with clean, well-structured Python code, making it easy to understand, modify, and extend.

How It Works
The core of this real-time object detection system operates through a streamlined pipeline:

Model Loading: A pre-trained yolov5s model is loaded using torch.hub.load, providing powerful object recognition capabilities out-of-the-box.

Video Stream Capture: OpenCV (cv2) is employed to capture video frames sequentially from a specified video file.

Real-Time Inference: Each captured frame is fed into the loaded YOLOv5 model, which performs rapid object detection.

Result Rendering: The model's detection results (bounding box coordinates, class labels, confidence scores) are processed and rendered directly onto the original video frame using OpenCV's drawing functionalities.

Live Visualization: The annotated frames are displayed in a dedicated window, providing a continuous, real-time visual feed of detected objects. The process continues until manually stopped.

Setup and Installation
To run this real-time object detection application, ensure you have Python 3.7+ installed.

Clone YOLOv5 Repository:

git clone https://github.com/ultralytics/yolov5
cd yolov5

Install Dependencies:

pip install -r requirements.txt

(Note: This will install torch, opencv-python, matplotlib, numpy, and other necessary libraries. A strong internet connection is recommended for downloading PyTorch and other large packages.)

Place Video File:
Place your video file (e.g., Motorway CCTV - 4 Split - 10mins - 1280 x 720.mp4) in a location accessible by your script. Update the video variable in the Python script with the correct path.

Usage
Navigate to Script Directory: Open your terminal or command prompt and navigate to the directory where your Python script is located.

Run the Script:

python your_script_name.py

(Replace your_script_name.py with the actual name of your Python file.)

View Detections: A new window will pop up, displaying the video stream with real-time object detections.

Exit: Press the 'q' key on your keyboard to close the detection window and terminate the script.

Customization Options
Video Source: Easily change the video variable in the script to point to a different video file or even a live webcam feed (e.g., cap = cv2.VideoCapture(0) for default webcam).

YOLOv5 Model: Experiment with different YOLOv5 model sizes (e.g., 'yolov5m', 'yolov5l', 'yolov5x') by changing 'yolov5s' in model = torch.hub.load(...) to balance speed and accuracy for your specific needs.

Confidence Thresholds: (Requires minor code modification) You can add logic to filter detections based on a confidence score, controlling which objects are displayed.

Skills Demonstrated
This project effectively showcases my expertise in:

Python Programming: Developing robust and efficient applications.

Deep Learning: Practical application of state-of-the-art neural networks (YOLOv5) for computer vision tasks.

Computer Vision (CV): Video processing, image manipulation, and real-time visualization with OpenCV.

PyTorch: Loading and performing inference with deep learning models.

Model Integration: Seamlessly integrating pre-trained models into custom applications.

Real-time Systems: Designing and implementing solutions that process data continuously and provide immediate feedback.

Problem Solving: Addressing challenges in video analysis and object detection.

Potential Applications
Beyond the initial use case of motorway CCTV analysis, this real-time object detection capability can be extended to:

Intelligent Transportation Systems: Traffic flow analysis, accident detection, pedestrian safety.

Security & Surveillance: Automated monitoring, anomaly detection, access control.

Retail Analytics: Customer behavior tracking, inventory management.

Industrial Automation: Quality control, safety compliance, asset tracking.

Sports Analytics: Player and ball tracking for performance analysis.
