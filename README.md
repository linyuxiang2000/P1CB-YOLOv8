# P1CB-YOLOv8s: A small object detection method for traffic scenes integrating high-resolution detection heads and adaptive weighted fusion
The new version of this code, DCAS++, will be released.
<div align=center>
<img src="./ultralytics/assets/VisDrone_mAP_Params.png" alt="VisDrone_mAP_Params" width = "549" />
</div>


## <div align="center">Documentation</div>

### Benchmark
| **Model**     | **Datasets** |  **mAP@0.5<sup>val**  | **mAP@0.5:0.95<sup>val** | **Params** | **Weight**                                                                                           |
|:-------------:|:------------:|:---------------------:|:------------------------:|:----------:|:----------------------------------------------------------------------------------------------------:|
| YOLOv8s       | VisDrone     |         33.1%         |          18.9%           | 11.1M      | [Download](https://pan.baidu.com/s/1fvyu_ZMK8CFsWPI69ClVKA?pwd=m5ja) |
| YOLOv8s+P1CB  | VisDrone     |         39.7%         |          23.2%           | 5.1M      | [Download](https://pan.baidu.com/s/1ZR0aqnQ-pTGmIP8uOZ06KQ?pwd=ptb8) |
| YOLOv8s       | BDD100K      |         53.6%         |          31.1%           | 11.1M      | [Download](https://pan.baidu.com/s/1pdX5B97T1_Jlz33e3JKkBA?pwd=2hqz) |
| YOLOv8s+P1CB  | BDD100K      |         58.1%         |          34.4%           | 5.1M      | [Download](https://pan.baidu.com/s/10kP0swizT-FPApCVp4vxAQ?pwd=b5v9) |
| YOLOv8s       | TT100K       |         85.4%         |          65.4%           | 11.1M      | [Download](https://pan.baidu.com/s/1aVF3kHTi06_0vQlTT7pJhg?pwd=mb9p) |
| YOLOv8s+P1CB  | TT100K       |         94.6%         |          72.6%           | 5.1M      | [Download](https://pan.baidu.com/s/1FlDthdsDCMxwh88Xc8smcw?pwd=hsr6) |

Table Notes
- No pre-trained weights were used during training.
- The input image resolution is 640×640.
- The default training epochs=300.
- For YOLOv8s+P1CB model, the recommended batch size for VisDrone, BDD100K, and TT100K is 2, 8, 12, respectively.
- All other parameters follow the settings of the baseline model.

### Quick Start
<details open>
<summary>Install</summary>

Clone repository and install [requirements.txt](./requirements.txt) in a [**Python==3.10**](https://www.python.org/) environment, 
including [**PyTorch==2.0.1**](https://pytorch.org/get-started/previous-versions/) and [**CUDA==11.7**](https://pytorch.org/get-started/previous-versions/).
```bash
pip install -e .  # Install the package in editable mode for development
```
</details>

<details open>
<summary>Training</summary>
The commands below reproduce the training results. You can also run train1.py to start training.

```bash
yolo task=detect mode=train model=yolov8s+P1CB.yaml data=VisDrone.yaml epochs=300 batch=2 device=0
```
</details>

<details open>
<summary>Evaluation</summary>
The commands below reproduce the evaluation results.

```bash
yolo task=detect mode=val model=weights/best.pt data=VisDrone.yaml batch=2 device=0
```
</details>

<details open>
<summary>Inference</summary>

The commands below reproduce the inference results. You can also run predict1.py to start predicting.

```bash
yolo task=detect mode=predict model=weights/best.pt device=0 source=path/to/image.jpg  # image
                                                                    path/to/video.mp4  # video
                                                                    path/to/dir  # directory
```
</details>

### Implementation details
Please note
- The overall architecture of P1CB is located at `ultralytics/models/v8/yolov8+P1CB.yaml`.
- The DAM module is located at `ultralytics/nn/modules.py` and calls `ultralytics/nn/DAM.py`.
- The dataset paths in `ultralytics/nn/DAM.py` and `ultralytics/datasets/` need to be changed to the root directory where the datasets are stored.
- The configuration file is located at `ultralytics/yolo/cfg/default.yaml`.
- Representative images of small objects are located at `ultralytics/assets/small_object/`.

### Data download
Note that all data has been cleaned and converted to YOLO format labels.
- VisDrone (1.81 GB): [GoogleDrive](https://drive.google.com/file/d/18rZfHuRK40nH43iVbLOd95h6Yv6BoKKl/view?usp=sharing)
- BDD100K (4.25 GB): [GoogleDrive](https://drive.google.com/file/d/1-ghEyaWKQ1lna4kcxXrUKfAAZygpMlh0/view?usp=sharing)
- TT100K (8.74 GB): [GoogleDrive](https://drive.google.com/file/d/10V2pUSmd6nzD5Cs9o0E_4IUfRjVYr6RK/view?usp=sharing)

## Acknowledgement
The code implementation is based on [YOLOv8](https://github.com/ultralytics/ultralytics) and [YOLOv8+DCAS](https://github.com/crafly/DCAS), thanks to their open-source code.
The data is based on the [VisDrone](https://github.com/VisDrone/VisDrone-Dataset), [BDD100K](https://www.vis.xyz/bdd100k/), and [TT100K](https://cg.cs.tsinghua.edu.cn/traffic-sign/) datasets, thanks to their open-source data.
