Simple Online and Realtime Tracker
This repository provides an implementation of the SORT (Simple Online and Realtime Tracker) algorithm for multi-object tracking. The algorithm uses a Kalman Filter for state estimation and the Hungarian algorithm for data association based on Intersection over Union (IoU) scores. It is suitable for real-time applications and can be integrated with detection outputs (e.g., from YOLOv5).

Overview
Kalman Filter: Used for predicting the state (position, scale, aspect ratio, and their velocities) of each tracked object.
Data Association: Matches detections to existing trackers using the Hungarian algorithm (via scipy.optimize.linear_sum_assignment or the lap package).
Configurable Parameters: Easily adjust parameters such as maximum age of a track, minimum hits to confirm a track, and the IoU threshold for matching.
Visualization: Optionally visualize tracking results with matplotlib.
Dependencies
Ensure you have the following Python libraries installed:

Python 2.7/3.x (with __future__ for Python 2 compatibility)
numpy
matplotlib
scikit-image (for image I/O)
filterpy (for the Kalman Filter)
scipy (for linear assignment)
(Optional) lap (an alternative linear assignment solver)
You can install the required packages using pip:

bash
Copy
Edit
pip install numpy matplotlib scikit-image filterpy scipy
If you want to use the optional lap package:

bash
Copy
Edit
pip install lap
Installation
Clone this repository:

bash
Copy
Edit
git clone https://github.com/your-username/sort-tracker.git
cd sort-tracker
Usage
The main script (sort_tracker.py) accepts detections and tracks objects across frames. It expects detection files in a directory structure similar to:

bash
Copy
Edit
data/<phase>/*/det/det.txt
Each detection file should contain comma-separated values in the following format:

arduino
Copy
Edit
frame, id, x, y, width, height, score, ...
Command-line Arguments:

--display: Flag to display online tracker output using matplotlib (may slow down processing).
--seq_path: Path to the detection data (default: data).
--phase: Subdirectory within seq_path (default: train).
--max_age: Maximum number of frames to keep a track alive without an associated detection (default: 1).
--min_hits: Minimum number of detections before a track is confirmed (default: 3).
--iou_threshold: Minimum IoU required for a match (default: 0.3).
Example Usage:

bash
Copy
Edit
python sort_tracker.py --seq_path data --phase train --max_age 1 --min_hits 3 --iou_threshold 0.3
Tracking outputs will be saved in the output directory.

File Structure
bash
Copy
Edit
.
├── README.md          # This file
├── sort_tracker.py    # Main tracking script
├── data/              # Folder for detection data (organized as data/<phase>/*/det/det.txt)
└── output/            # Folder where tracking outputs are saved
