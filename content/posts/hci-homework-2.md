+++
title = "HCI Homework 2: Body Interfaces and the Ultimate Display"
date = 2026-10-14
description = "Pedro Lopes's research, Sutherland's display vision, and a wristband that reads muscle activity."
tags = ["HCI", "haptics", "input devices", "sEMG"]
categories = ["HCI"]
courses = ["HCI"]
source_files = ["HCI/Human Computer Interaction/Lecture_homework/HW2.pdf", "HCI/homework-2/research-notes.md"]
+++

## Lecture 4 - An HCI researcher: Pedro Lopes

Pedro Lopes leads the Human Computer Integration Lab at the University of Chicago. His work studies interfaces that connect to the body through touch, muscle stimulation, and other sensations. The computer can provide physical feedback instead of only showing instructions on a screen.

Two recent projects make this approach quite concrete:

- **Generative Muscle Stimulation, CHI 2026.** The system uses a person's view and body pose to generate physical assistance for everyday tasks. It constrains the generated instructions using joint limits and knowledge about muscle stimulation. This makes context important: the same object can require different actions in different situations.
- **Myo Action, CHI 2026.** Muscle signals trigger stimulation that assists an action the person has already started. The aim is to speed up movement while preserving the person's decision to act.

The interesting HCI question is control. Assistance should be easy to interrupt, and the person should understand when the system is acting. A technically effective movement could still feel wrong if it happens unexpectedly.

## Lecture 5 - Reading The Ultimate Display

In 1965, Ivan Sutherland described displays that could engage several senses and let people explore computer-generated worlds. Some parts are now familiar. Interactive 3D graphics can show impossible objects and simulated physics. Eye tracking can help select interface elements; force-feedback devices can resist a movement.

He also discussed pointing and dragging, which were already being explored at the time. Their everyday use today shows how ideas that once needed special equipment can become ordinary interactions.

The difficult part is physical presence. A virtual chair can look convincing without supporting a person's weight. Images, sound, and vibration don't automatically reproduce the forces of a real object.

I expect better combinations of visual tracking, wearable feedback, and movable physical props. These could make training more convincing. A room that creates arbitrary solid matter is much further away; improving an illusion doesn't mean producing the object itself.

## Lecture 6 - A surface-EMG wristband

A 2025 research system from CTRL-labs at Reality Labs uses a wristband to measure electrical activity from muscles. A decoder turns these signals into computer commands. The paper demonstrates continuous control, discrete gestures, and handwriting input.

{{< portfolio-image src="images/hci/homework-2/semg-input.svg" alt="Concept diagram: a deliberate hand movement produces muscle signals, a wristband measures them, and a decoder turns them into an interface command." >}}

*Concept diagram of the input path. EMG measures activity; it does not stimulate the muscles.*

I would classify it as **wearable physiological input** used for explicit, gesture-based interaction. It can support a spatial interface, but the wristband itself doesn't necessarily track a hand's full 3D position. It isn't an implanted brain interface either.

The advantage is small movements without a controller or a camera needing to see the hand. This could suit lightweight AR glasses. However, the system must distinguish a command from an ordinary movement. Fit, individual differences, and error recovery matter as much as recognition accuracy.

My prediction: useful for short commands such as selecting or scrolling, with clear feedback and an undo action. Replacing a keyboard for long writing sessions is a harder claim. A successful demonstration alone doesn't establish everyday comfort or adoption.
