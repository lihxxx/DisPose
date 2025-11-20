# [ICLR2025] DisPose: Disentangling Pose Guidance for Controllable Human Image Animation
This repository is the official implementation of [DisPose](https://arxiv.org/abs/2412.09349).

[![arXiv](https://img.shields.io/badge/arXiv-2412.09349-b31b1b.svg)](https://arxiv.org/abs/2412.09349)
[![Project Page](https://img.shields.io/badge/Project-Website-green)](https://lihxxx.github.io/DisPose/)

## 🔥 News
- **`2025/01/23`**: DisPose is accepted to ICLR 2025.
- **`2024/12/13`**: We have released the inference code and the checkpoints for DisPose.
  
**📖 Table of Contents**
- [DisPose: Disentangling Pose Guidance for Controllable Human Image Animation](#dispose-disentangling-pose-guidance-for-controllable-human-image-animation)
  - [🎨 Gallery](#-gallery)
  - [🧙 Method Overview](#-method-overview)
  - [🔧 Preparations](#-preparations)
    - [Setup repository and conda environment](#setup-repository-and-conda-environment)
    - [Prepare model weights](#prepare-model-weights)
  - [💫 Inference](#-inference)
    - [Tips](#tips)
  - [📣 Disclaimer](#-disclaimer)
  - [💞 Acknowledgements](#-acknowledgements)
  - [🔍 Citation](#-citation)

## 🎨 Gallery
<table class="center">
<tr>
  <td><video src="https://github.com/user-attachments/assets/e2f5e263-3f86-4778-98b9-6d2d451b7516" autoplay></td>
  <td><video src="https://github.com/user-attachments/assets/f8e761e3-7a7a-4812-ad61-023b33034a42" autoplay></td>
  <td><video src="https://github.com/user-attachments/assets/9a6c7ea6-8c73-4a50-b594-f8eba239c405" autoplay></td>
  <td><video src="https://github.com/user-attachments/assets/a0f97ac4-429e-4ca9-a794-7c02b5dc5405" autoplay></td>
  <td><video src="https://github.com/user-attachments/assets/6e9d463c-f7c5-4de8-924b-1ad591e3a9a4" autoplay></td>
</tr>
</table>

## 🧙 Method Overview
We present **DisPose** to mine more generalizable and effective control signals without additional dense input, which disentangles the sparse skeleton pose in human image animation into motion field guidance and keypoint correspondence.
<div align='center'>
<img src="https://anonymous.4open.science/r/DisPose-AB1D/pipeline.png" class="interpolation-image" alt="comparison." height="80%" width="80%" />
</div>


## 🔧 Preparations
### Setup repository and conda environment
The code requires `python>=3.10`, as well as `torch>=2.0.1` and `torchvision>=0.15.2`. Please follow the instructions [here](https://pytorch.org/get-started/locally/) to install both PyTorch and TorchVision dependencies. The demo has been tested on CUDA version of 12.4.
```
conda create -n dispose python==3.10
conda activate dispose
pip install -r requirements.txt
```

### Prepare model weights
1. Download the weights of  [DisPose](https://huggingface.co/lihxxx/DisPose) and put `DisPose.pth` into `./pretrained_weights/`.

2. Download the weights of other components and put them into `./pretrained_weights/`:
  - [stable-video-diffusion-img2vid-xt-1-1](https://huggingface.co/stabilityai/stable-video-diffusion-img2vid-xt-1-1/tree/main)
  - [stable-diffusion-v1-5](https://huggingface.co/stable-diffusion-v1-5/stable-diffusion-v1-5/tree/main)
  - [dwpose](https://huggingface.co/yzd-v/DWPose/tree/main)
  - [MimicMotion](https://huggingface.co/tencent/MimicMotion/tree/main)
3. Download the weights of [CMP](https://huggingface.co/MyNiuuu/MOFA-Video-Hybrid/resolve/main/models/cmp/experiments/semiauto_annot/resnet50_vip%2Bmpii_liteflow/checkpoints/ckpt_iter_42000.pth.tar) and put it into `./mimicmotion/modules/cmp/experiments/semiauto_annot/resnet50_vip+mpii_liteflow/checkpoints`

Finally, these weights should be organized in `./pretrained_weights/`. as follows:


```
./pretrained_weights/
|-- MimicMotion_1-1.pth
|-- DisPose.pth
|-- dwpose
|   |-- dw-ll_ucoco_384.onnx
|   └── yolox_l.onnx
|-- stable-diffusion-v1-5
|-- stable-video-diffusion-img2vid-xt-1-1
```

## 💫 Inference

A sample configuration for testing is provided as `test.yaml`. You can also easily modify the various configurations according to your needs.

```
bash scripts/test.sh 
```

### Tips
- If your GPU memory is limited, try set `decode_chunk_size` in `test.yaml` to 1.
- If you want to enhance the quality of the generated video, you could try some post-processing such as face swapping ([insightface](https://github.com/deepinsight/insightface)) and frame interpolation ([IFRNet](https://github.com/ltkong218/IFRNet)).

## 📣 Disclaimer
This is official code of DisPose.
All the copyrights of the demo images and videos are from community users. 
Feel free to contact us if you would like to remove them.

## 💞 Acknowledgements
We sincerely appreciate the code release of the following projects: [MimicMotion](https://github.com/Tencent/MimicMotion), [Moore-AnimateAnyone](https://github.com/MooreThreads/Moore-AnimateAnyone), [CMP](https://github.com/XiaohangZhan/conditional-motion-propagation).

## 🔍 Citation

```
@inproceedings{
li2025dispose,
title={DisPose: Disentangling Pose Guidance for Controllable Human Image Animation},
author={Hongxiang Li and Yaowei Li and Yuhang Yang and Junjie Cao and Zhihong Zhu and Xuxin Cheng and Long Chen},
booktitle={The Thirteenth International Conference on Learning Representations},
year={2025},
url={https://openreview.net/forum?id=AumOa10MKG}
}
```
