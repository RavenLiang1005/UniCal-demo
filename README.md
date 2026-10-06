# UniCal Demo

[Download complete demo ZIP](https://github.com/RavenLiang1005/UniCal-demo/releases/download/demo-v1.0.0/UniCal-demo.zip) · [Project page](https://ravenliang1005.github.io/UniCal-web-page/)

The complete code, pretrained weights, and sample images are distributed together in the ZIP attached to the Release. Download and extract it before following the instructions below.

Inference demo for depth reconstruction, contact masks, and normal-force-map visualization on GelSight, Tac3D, DM-Tac, and 9DTact images.

## Setup

The supplied environment targets NVIDIA CUDA 12.1:

```bash
conda env create -f environment.yml
conda activate monocular_tac
```

## Run

```bash
python infer.py --sensor_type GelSight
python infer.py --sensor_type Tac3D --no_open3d --save_mask
```

Use `--image_path` for an image or image directory and `--output_dir` for the output location. Inputs are resized to 640 × 480 by default. Use `--no_open3d` on machines without a graphical display.

## Models and outputs

Each sensor has separate `depth_encoder.pth` and `force_encoder.pth` files, loaded into independent encoder instances. The supplied encoder files are copies of the same demo checkpoint and can be replaced independently. Contact-mask weights are stored in `weights_mask/`.

Outputs are saved under `output/{sensor_type}/`:

- `depth_pred_npy/`: depth arrays in mm, using the default 0–10 mm range.
- `force_map/`: per-image normalized force-map heatmaps.
- `open3d_view/`: per-image normalized 3D displays in image coordinates.
- `mask_pred/`: binary contact masks when `--save_mask` is enabled.

The PNG visualizations do not encode metric XYZ coordinates or calibrated force magnitudes. This package contains inference examples; training and global three-axis force regression are not included.

## License

See LICENSE.
