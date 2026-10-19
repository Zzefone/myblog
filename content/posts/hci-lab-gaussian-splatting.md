+++
title = "HCI Lab: Gaussian Splatting from Images to Unity"
date = 2026-10-10
lastmod = 2026-10-19
description = "A recorded Brush training run, simple splat filtering, and a tested Unity desktop viewer."
tags = ["HCI", "Unity", "Gaussian splatting", "3D reconstruction", "Brush"]
categories = ["HCI"]
courses = ["HCI"]
source_files = ["HCI/Human Computer Interaction/LAB_homework/3D Gaussian splatting in unity.pptx", "HCI/lab-gaussian-splatting/README.md", "HCI/lab-gaussian-splatting/data/source-manifest.json", "HCI/lab-gaussian-splatting/scripts/train.py", "HCI/lab-gaussian-splatting/scripts/prepare_models.py", "HCI/lab-gaussian-splatting/training/run-01/config.json", "HCI/lab-gaussian-splatting/training/run-01/status.json", "HCI/lab-gaussian-splatting/verification/summary.json", "HCI/lab-gaussian-splatting/verification/REPORT.md", "HCI/lab-gaussian-splatting/UnityProject/Assets/Editor/SplatLabBuild.cs", "HCI/lab-gaussian-splatting/UnityProject/Assets/Scripts/SplatLabController.cs"]
+++

This lab connects image-based training to a Unity scene. The trained model stores coloured, transparent 3D Gaussians rather than a triangle mesh. Each Gaussian has a position, scale, rotation and opacity; overlapping splats form the image seen by the camera.

*Experiment and Windows verification completed on 19 October 2026. The article sits in the October lab sequence; the measurements below come from that later run.*

{{< portfolio-image src="images/hci/gaussian-splatting/unity-filtered.png" alt="Two reconstructed hotdogs on a plate, rendered by the tested Unity Windows player using the filtered Gaussian model." >}}

*Actual Unity camera capture, with the desktop control overlay excluded. Soft edges and stretched details are still visible.*

## Input and training

The course slides introduce capture, training and importing a Gaussian asset into Unity. For this reproducible run, the input is the public **NeRF Synthetic Hotdog** scene: 100 training images and ten validation images with supplied camera poses. The original model is by [erickfree, released as CC0](https://www.blendswap.com/blend/23962); the rendered views come from a [public dataset mirror](https://huggingface.co/datasets/pablovela5620/nerf-synthetic-mirror).

This covers reconstruction from posed images. Personal photography and COLMAP camera estimation have not been carried out. The supplied poses let the experiment concentrate on training and Unity integration.

Images were resized from 800 × 800 to 400 × 400. Validation uses every tenth frame from the original validation split, giving ten views separate from the 100 training views. The source manifest records the original file hashes.

[Brush v0.3.0](https://github.com/ArthurBrussee/brush/releases/tag/v0.3.0) trained for 3,000 steps on an NVIDIA RTX 3060 Laptop GPU, using Vulkan. Settings: seed 20261019, spherical harmonics degree 3, refinement every 100 steps, growth stopping at step 2,500, and a cap of 100,000 splats. The process took 38.94 seconds including startup, evaluation and exports; Brush reported 33 seconds for training.

| Step | Validation PSNR | Validation SSIM |
| --- | --- | --- |
| 1,000 | 23.61 dB | 0.8682 |
| 2,000 | 28.69 dB | 0.9406 |
| 3,000 | 30.40 dB | 0.9542 |

{{< portfolio-image src="images/hci/gaussian-splatting/training-progress.png" alt="One held-out reference image beside actual Brush renders at 1,000 and 3,000 training steps, showing improved shape and surface detail." >}}

*Same validation camera at both checkpoints. The final render recovers more of the bread, sausage and plate, though fine texture remains blurred.*

An independent RGB check of the ten saved final renders gives mean per-image PSNR **30.3958 dB**, with transparent reference pixels composited on black. These are validation measurements used during training. They are neither an untouched final test nor measurements of the Unity renderer.

## Filtering and importing

The final PLY contains **9,020 Gaussians**. A small Python filter removes splats with opacity below 0.01 or a centre more than two scene units from the median centre. It removes 200 splats, leaving **8,820**. There are 199 low-opacity splats and three distant splats, with two in both groups.

The raw export is preserved. These thresholds are specific to this experiment, and removing splats alone does not demonstrate better image quality. The raw and filtered Unity captures look very similar at this scale. This cleanup was scripted; no SuperSplat editing session is claimed.

The Unity project uses **6000.0.23f1** and [aras-p's Gaussian Splatting viewer](https://github.com/aras-p/UnityGaussianSplatting), pinned to commit `2c6fed37da67a217367261fcfcd3316d34c73e76` (package 1.1.1). Both PLY files were imported with its Medium preset. The viewer source and MIT licence are included in the download.

A minimal package manifest first failed because the renderer references `XRSettings`. Adding the Unity VR module alongside XR resolved compilation. The Windows player uses **Direct3D 12**, Linear colour and no MSAA; this viewer does not support Direct3D 11. Reflecting Z for both the model and the provided camera poses keeps them in the same Unity coordinate system.

## Checking the running scene

The Windows build completed and the actual player rendered both models from three cameras: six captures in total. Runtime records confirm Direct3D 12 on the RTX 3060, with the expected 9,020 and 8,820 splats. A debug-point capture also shows the Gaussian centres.

{{< portfolio-image src="images/hci/gaussian-splatting/unity-second-view.png" alt="A second camera angle of the filtered reconstruction rendered in the running Unity player." >}}

{{< portfolio-image src="images/hci/gaussian-splatting/debug-points.png" alt="Unity debug view showing the reconstructed object's individual Gaussian centres as coloured points." >}}

Left/Right selects the three cameras, **C** switches raw/filtered data, and **P** switches splats/debug points. The camera captures were inspected for visible content and consistent orientation. This check does not establish a frame rate, VR support or mobile compatibility.

The editor reported two persistent allocations when exiting after import. The build and player checks passed, but that importer warning remains in the local log.

## Files and remaining work

- {{< portfolio-file src="files/hci/gaussian-splatting/gaussian-splat-lab-source.zip" label="Download the Unity project, PLY models, preparation scripts and recorded checks" >}}
- {{< portfolio-file src="files/hci/gaussian-splatting/results.json" label="Download the experiment results" >}}

Open `UnityProject/Assets/Scenes/SplatLab.unity` in Unity 6000.0.23f1. The archive includes the imported assets, so viewing the scene does not require retraining. Its README explains downloading the input images and Brush separately for a new training run.

The next useful extension is a personally captured object with estimated camera poses. That would check the capture stage, where coverage, lighting and pose errors are less controlled than in this synthetic scene.
