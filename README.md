# yolo and other models of onnxruntime from usls
we can interference yolo models and other models by usls in rust easily,thanks to jamjamjon.
## fork

📔 we changed fork from
https://github.com/ultralytics/ultralytics to https://github.com/jamjamjon/usls, which provides yolo examples to ultralytics,
📔 ultralytics add examples:
`examples/YOLO-Series-ONNXRuntime-Rust`, it used usls crate directly.
📔 so we use usls crate directly.in it:

* yolo5~yolo11 are supported.

## Features

* Support `Classification`, `Segmentation`, `Detection`, `Pose(Keypoints)-Detection` tasks.
* Support `FP16` & `FP32` ONNX models.
* Support `CPU`, `CUDA` and `TensorRT` execution provider to accelerate computation.
* Support dynamic input shapes(`batch`, `width`, `height`).
* more details,please check usls crate doc.

## ⛳️ Installation ONNXRuntime Linking

You have two options to link the ONNXRuntime library

* ### Option 1: Manual Linking
  ⚠️
  ```txt
  onnxruntime version >=1.20.1,
  ort version>=2.0.0.rc.9
  usls version >=0.0.20
```
  * For detailed setup instructions, refer to the [ORT documentation](https://ort.pyke.io/setup/linking).
  * This repository use `ort` crate, which is ONNXRuntime wrapper for Rust. (https://docs.rs/ort/latest/ort/)
  * #### For Linux or macOS Users:
    * Download the ONNX Runtime package from the [Releases page](https://github.com/microsoft/onnxruntime/releases).
    * Set up the library path by exporting the `ORT_DYLIB_PATH` environment variable:
      `vim ~/.bashrc`
      add the following line to ~/.bashrc
      `txt
         export ORT_DYLIB_PATH=/path/to/onnxruntime/lib/libonnxruntime.so.1.20.1
         `
      `source ~/.bashrc`
  * ### Option 2: Automatic Download
  Just use `--features auto`
  ```shell
  cargo run -r --example yolo --features auto
  ```
* ### Optional 3: Install CUDA & CuDNN & TensorRT
* CUDA execution provider requires CUDA v11.6+.
* TensorRT execution provider requires CUDA v11.4+ and TensorRT v8.4+.

## models

### Option 1:Download the YOLOv8 ONNX Models

usls:https://github.com/jamjamjon/assets/releases/tag/yolo ,or other models.

### Option 2:Export the YOLOv8 ONNX Models

```bash
pip install -U ultralytics
# export onnx model with dynamic shapes
yolo export model=yolov8m.pt format=onnx  simplify dynamic
yolo export model=yolov8m-cls.pt format=onnx  simplify dynamic
yolo export model=yolov8m-pose.pt format=onnx  simplify dynamic
yolo export model=yolov8m-seg.pt format=onnx  simplify dynamic
# export onnx model with constant shapes
yolo export model=yolov8m.pt format=onnx  simplify
yolo export model=yolov8m-cls.pt format=onnx  simplify
yolo export model=yolov8m-pose.pt format=onnx  simplify
yolo export model=yolov8m-seg.pt format=onnx  simplify
```

## Run Inference

### yolo
For examples,model path is relative to `../models.`:
- Detect
```sh
cargo run -r --example yolo -- --task detect --ver v8 --scale n --model../models/v8-m.onnx  --source assets/bus.jpg
cargo run -r --example yolo -- --task detect --ver v11 --scale n --model../models/v11-m.onnx  --source assets/bus.jpg
```
- Pose
```sh
cargo run -r --example yolo -- --task pose --ver v8 --scale n --model ../models/v8-m-pose.onnx  --source assets/bus.jpg
cargo run -r --example yolo -- --task pose --ver v11 --scale n --model ../models/v11-m-pose.onnx  --source assets/bus.jpg
```
### other

check `README.md` in examples.

not yet test, testing soon.
## TODO

test other models.
