# 🧠 People Flow Detection with Object Tracking & Heatmap Visualization

## 🎥 Video Example
[people-walking.mp4](https://media.roboflow.com/supervision/video-examples/people-walking.mp4)

---

## 🔮 Objective
Build an intelligent computer vision system that:
- Tracks people in a video
- Counts how many entered or exited based on crossing virtual lines
- Generates a heatmap of presence/movement intensity

---

## 📊 Project Overview
| Component | Description |
|----------|-------------|
| **Model** | YOLOv8x (or yolov8n for faster inference) |
| **Tracking** | ByteTrack (via `model.track(...)`) |
| **Counting Method** | Two horizontal lines drawn in the frame |
| **Line Logic** |
  - If a person crosses **top line downward** → Count as `IN`
  - If a person crosses **bottom line upward** → Count as `OUT` |
| **Heatmap** | Accumulate center points of bounding boxes across all frames |

---

## 📆 Requirements
Install dependencies in Colab:
```bash
!pip install -q ultralytics opencv-python tqdm
```

---

## 🔢 Logic Summary

### ✈️ Detection
- YOLOv8 detects `person` class only (class id = 0)
- Each person is tracked with a unique ID (via ByteTrack)

### ⏱️ Tracking & Counting
- Maintain previous y-coordinate for each ID
- Compare current vs. previous position against the line to determine IN/OUT

### 🔍 Heatmap
- Each detected center `(cx, cy)` is plotted on a floating-point canvas
- Canvas decays slightly each frame using `fade_alpha = 0.95`
- Final heatmap created using Gaussian blur + color mapping

---

## 📹 Output
- `annotated_video_tracked.avi`: Video with:
  - Bounding boxes
  - Person IDs
  - IN/OUT counters
  - Color-coded lines
  - Live heatmap overlay

- `final_heatmap.jpg`: Still image showing areas of high presence

---

## 📄 Deliverables
- Google Colab Python notebook (`.ipynb`)
- Output video and image
- This README

---

## 🚀 Optional Enhancements
- Use trajectory lines for smoother movement trails
- Save per-frame statistics (IN/OUT timeline)
- Add GUI slider to view progression

---

## 🚀 Credits
Developed using [Ultralytics YOLOv8](https://github.com/ultralytics/ultralytics), OpenCV, and Python ❤️

---

## 🎨 Screenshot (Optional)
Add a sample frame here to show what the result looks like.

---

## 🔗 How to Run (Colab)
1. Open Colab notebook
2. Upload your own video or use the Roboflow sample
3. Run all cells
4. Download final `.mp4` and `.jpg` files

Happy Coding!
