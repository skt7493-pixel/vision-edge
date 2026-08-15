# vision-edge
# Real-Time Vehicle Tracking & Counting using YOLO11

## Overview
This project is a real-time computer vision application that detects, tracks, and counts vehicles in a video stream. It uses the state-of-the-art **YOLO11** object detection model and **OpenCV** to monitor traffic flow, counting vehicles as they cross a designated virtual "tripwire" on the screen.

## Features
- **Real-Time Detection:** Utilizes the YOLO11 Large model to identify vehicles (cars, trucks, buses, motorcycles, bicycles) with high accuracy.
- **Object Tracking:** Assigns unique IDs to detected objects across frames to prevent double-counting.
- **Line Crossing Logic:** Counts a vehicle only when its centroid (center point) crosses a predefined virtual red line.
- **On-Screen Analytics:** Displays live counting statistics, bounding boxes, and object IDs directly on the video feed.

## Prerequisites
Make sure you have Python installed. You will need the following libraries:
- `ultralytics` (for the YOLO AI model)
- `opencv-python` (for video processing and drawing)

## Installation
1. Clone this repository or place the project files in a folder.
2. Install the required dependencies using pip:
   ```bash
   pip install ultralytics opencv-python
   ```

## Project Structure
- `main.py` (or your script name) - The main Python script containing the tracking and counting logic.
- `test_videos/4.mp4` - The sample video file used for testing. *(Note: Ensure this directory and file exist, or update the script to point to your own video).*
- `yolo11l.pt` - The pre-trained YOLO11 Large model (automatically downloaded by the Ultralytics library on the first run).

## Usage
1. Open your terminal or command prompt.
2. Navigate to the directory containing your script.
3. Run the script:
   ```bash
   python your_script_name.py
   ```
4. A window titled **"YOLO Object Tracking & Counting"** will appear, showing the processed video feed.
5. Press the **'q'** key while the video window is active to stop the program and close the window safely.

## How It Works under the Hood
1. **Model Loading:** The script initializes `yolo11l.pt`. Because it is pre-trained on the massive COCO dataset, it inherently knows how to recognize vehicles.
2. **Video Processing & Tripwire:** OpenCV reads the video frame by frame and draws a virtual red line at the Y-coordinate `430`.
3. **Tracking & Filtering:** YOLO tracks objects, but we filter the detections to only pay attention to vehicle classes (COCO classes 1, 2, 3, 5, 6, 7).
4. **The Counting Logic:** 
   - The script calculates the center point `(cx, cy)` of each vehicle's bounding box.
   - If the vehicle's Y-coordinate `(cy)` is greater than `430` (meaning it crossed the line), the script checks a Python `set` called `crossed_ids`.
   - If the vehicle's unique ID is not in that set, it adds it (to prevent double counting) and increments a smart dictionary (`defaultdict`) for that specific vehicle type.

## Acknowledgments
- **Ultralytics** for providing the powerful YOLO11 engine.
- **OpenCV** for the computer vision and image processing tools.
- **COCO Dataset** for the labeled data that makes pre-trained vehicle detection possible.
