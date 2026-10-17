+++
title = "Planar AR: matching a marker and replacing it"
date = 2026-10-17
description = "A SIFT and ORB implementation with an interactive GUI. Synthetic tests are complete; phone-to-webcam validation is still pending."
draft = true
tags = ["BCV", "augmented reality", "OpenCV", "feature matching", "Python"]
categories = ["BCV"]
courses = ["BCV"]
source_files = ["BCV/final_project/VAR-BSC-Final-Project-2026.pdf", "BCV/final_project/ar_core.py", "BCV/final_project/ar_app.py", "BCV/final_project/output/synthetic_summary.csv", "BCV/final_project/output/evaluation_metadata.json"]
+++

A reference image, a camera frame and a replacement image. The BCV final project is to find the first image in the frame and put the replacement in the same position. The program and synthetic tests are ready. Testing the marker on a phone in front of the webcam is still pending.

## The matching pipeline

SIFT is the default, with ORB available in the GUI. Both use brute-force kNN matching with two neighbours. A ratio test removes ambiguous matches, and RANSAC estimates the homography from the remaining pairs.

Not every returned homography is useful. The program also checks the inlier count, inlier ratio, spread of reference points and projected outline. If those checks fail, it leaves the current frame unchanged. Otherwise, `warpPerspective` transforms the replacement and a mask limits blending to the marker area.

The main defaults are 1800 features, a 3-pixel RANSAC threshold and at least 10 inliers. The ratio threshold is 0.72 for SIFT and 0.78 in the ORB benchmark. These values are adjustable rather than hidden in the code.

{{< portfolio-image src="images/bcv/marker-ar/perspective-comparison.png" alt="Synthetic perspective test showing the detected marker, inlier matches and replacement image." >}}

*Synthetic perspective test.* The target quadrilateral is known, so the four estimated corners can be checked directly.

## What the synthetic tests show

Two marker types, two descriptors, ten conditions and three small geometric perturbations per condition: 120 runs in total. The images are 800 by 600. A positive case passes when alignment is accepted and mean corner error is at most 5 pixels.

Both methods pass all 27 positive cases for the detailed marker. A plain grey rectangle passes none for either method. No false detections in the 12 marker-absent cases. That is a small set, and the exact reference artwork is reused to construct every positive scene.

The strong perspective case separates the estimates more clearly: mean corner error is about 0.49 pixels for SIFT and 3.50 pixels for ORB. Both still pass the chosen limit. Processing times are in the CSV files; they exclude diagnostic drawing and display, so they are not live-camera FPS.

{{< portfolio-image src="images/bcv/marker-ar/conditions.png" alt="Nine clearly labelled synthetic conditions, including rotation, dim lighting, shadow, blur and partial occlusion." >}}

The 25% and 50% occlusions hide part of the reference image in its own plane. They test whether enough features remain for detection. The rendered replacement still covers the full estimated rectangle, including the occluded area. There is no foreground-hand model.

## Interface and the remaining test

{{< portfolio-image src="images/bcv/marker-ar/gui-synthetic-demo.jpg" alt="Actual AR application GUI playing a labelled synthetic video, with parameter controls and three result views." >}}

The interface accepts a camera or video file. It shows the outline or keypoints, the replacement and the filtered matches. Capture runs in a separate process, which makes a stalled virtual camera easier to stop.

The GUI has been run and inspected with the generated demo. The integrated camera can return frames. Neither check establishes that a phone-displayed marker is tracked reliably.

The next tests need the marker on an actual phone screen: front view, tilt, rotation, changes in brightness, partial covering and a cluttered background. Reflections, focus and motion blur are still open questions. The article remains a draft until there is real marker evidence.

[Reference marker](https://zzefone.github.io/myblog/images/bcv/marker-ar/marker.png) · [Source bundle](https://zzefone.github.io/myblog/files/bcv/marker-ar/Planar_AR_Project.zip)
