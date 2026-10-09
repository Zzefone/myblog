+++
title = "La Cigale (the cicada) et la Fourmi (the ant) modelling with Blender"
date = 2026-10-09
description = "A low-poly cicada, an ant carrying grain, and a short pause between them. CG final project in Blender."
tags = ["CG", "Blender", "modelling", "low-poly", "animation"]
categories = ["CG"]
courses = ["CG"]
source_files = ["CG/brief/Final_project_La_Fontaine.pdf", "CG/README.md", "CG/scripts/make_project.py", "CG/output/validation.json", "CG/output/video_validation.json", "CG/output/Wang/image.png", "CG/output/Wang/video.mp4", "CG/output/Wang/project.blend"]
+++

For the CG final project, I chose *La Cigale et la Fourmi*, a fable by Jean de La Fontaine. *Cigale* means cicada; *fourmi* means ant.

One small moment: an ant carries a grain past a cicada resting on a rock. It stops, turns its head, then keeps going. The cicada stays where it is.

{{< portfolio-image src="images/cg/la-cigale-et-la-fourmi/image.png" alt="A reddish-brown low-poly ant carrying a grain beside a green cicada resting on a rock." >}}

*The still render, taken at frame 174 during the pause.*

## The brief

Two animal characters, a small set, coloured materials, and a keyframed animation of at least ten seconds. A framed camera shot and lighting too. UV unwrapping and texture painting were optional.

The required files were `project.blend`, a 1920 × 1080 `image.png`, and `video.mp4`, packed into a folder named with my surname. Keeping the scene simple was part of the brief.

## Building the scene

The characters are made from basic geometry using Blender's Python API. Scaled icospheres for the bodies and eyes, narrow cylinders for the legs and antennae. The ant has three body sections and six legs. Its grain moves with the head.

For the cicada, the broad eyes and veined wings do most of the work. The wings are flat polygon meshes, with thin cylinders along the edges and veins. Still quite angular. Enough detail to recognise it in the wide shot.

The set is just a ground plane, a rock, and a fallen branch. Brown for the ant, olive green for the cicada, pale wings. Each visible object has a material with base colour, roughness, and metallic settings; metallic stays at zero. No external textures or add-ons.

An orthographic camera keeps the whole action in view. Two area lights: a warm key and a softer fill. The final image and video use EEVEE.

## A pause in the walk

The animation runs from frame 1 to 360 at 30 fps. Twelve seconds in total.

The ant moves across the foreground until around frame 135, pauses near the cicada, then continues after frame 205. During that stop, its head turns towards the rock. A small gesture, but it gives the two characters a connection.

The legs alternate through a repeating cycle, with a slight lift and body bob while walking. The motion uses ordinary editable keyframes with linear interpolation. No armature. The main movement and the head turn can be adjusted separately in the `.blend` file.

{{< portfolio-video src="files/cg/la-cigale-et-la-fourmi/video.mp4" poster="images/cg/la-cigale-et-la-fourmi/image.png" title="La Cigale et la Fourmi: 12-second Blender animation" >}}

*1920 × 1080, 30 fps, H.264 / MP4. Use the player to watch the full animation.*

## Files and checks

The saved project and exported video were checked separately. The video contains 360 frames; frames 1, 120, 174, 270, and 360 were decoded to check the rendered sequence. The project has no external image dependencies, and the submission archive contains the three required files.

- {{< portfolio-file src="files/cg/la-cigale-et-la-fourmi/project.blend" label="Download the editable Blender project" >}}
- {{< portfolio-file src="files/cg/la-cigale-et-la-fourmi/Wang.zip" label="Download the submission archive" >}}
- {{< portfolio-file src="files/cg/la-cigale-et-la-fourmi/video.mp4" label="Download the video" >}}

Open the project in Blender 5.2.2 LTS and press Space to play. It opens at frame 174, the same moment as the still image.

The walk is stylised, and the cicada has no movement of its own. A more convincing foot contact would be the next thing to adjust.
