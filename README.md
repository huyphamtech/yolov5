
# 🚗 Vehicle Detection using YOLOv5 on Traffic Dataset

This project demonstrates how to train a custom object detection model using YOLOv5 on a traffic dataset. The goal is to identify and classify various types of vehicles in both images and videos.

## 📂 Project Overview

This Colab notebook:
- Downloads a vehicle traffic dataset from KaggleHub
- Uses the YOLOv5 framework to train a model on custom-labeled images
- Visualizes training performance
- Evaluates the model using validation metrics (confusion matrix)
- Tests the model on sample images and video
- Extracts basic traffic analytics

## 🧰 Technologies Used

- Python, PyTorch
- OpenCV, Pandas, Matplotlib
- YOLOv5 (Ultralytics repo)
- Google Colab
- KaggleHub for dataset download

## 📦 Dataset

- Source: KaggleHub (`saumyapatel/traffic-vehicles-object-detection`)
- Classes: Car, Number Plate, Blur Number Plate, Two Wheeler, Auto, Bus, Truck
- Structure:
  ```
  /images/train/
  /images/val/
  /images/test/
  ```

## 🚀 Setup & Training

1. **Clone YOLOv5**
    ```bash
    !git clone https://github.com/ultralytics/yolov5
    %cd yolov5
    ```

2. **Install Dependencies**
    ```bash
    !pip install -r requirements.txt
    ```

3. **Prepare Custom Dataset Configuration**
    A custom `dataset.yaml` is written with 7 classes and correct train/val paths.

4. **Train the Model**
    ```bash
    !python train.py --img 640 --batch 16 --epochs 20 --data dataset.yaml --weights yolov5s.pt --cache
    ```

## 📊 Evaluation & Visualization

- Training and validation losses are plotted over epochs.
- Model is evaluated using:
    ```bash
    !python val.py --img 640 --data dataset.yaml --weights runs/train/exp/weights/best.pt
    ```
- Confusion matrix is displayed as part of the validation result.

## 📷 Testing & Inference

- Run inference on selected test images using:
    ```python
    results = model(img_path)
    results.show()
    ```
- Test the model on a video using:
    ```bash
    !python detect.py --weights ./runs/train/exp/weights/best.pt --source '<video_path>' --project results --name output
    ```

## 📈 Additional Features

- Zip and download trained model weights
- Run simple traffic flow analysis using OpenCV on test video

## 📎 Notes

- Training runs for 20 epochs with YOLOv5s (small) model
- Ensure your Kaggle API is set up if using `kagglehub`
- Trained model can be reused or fine-tuned by loading from `best.pt`
