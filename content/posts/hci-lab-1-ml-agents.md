+++
title = "HCI Lab 1: Learning to Reach and Chase"
date = 2026-10-16
lastmod = 2026-10-17
description = "Two PPO policies in Unity, checked against random actions in 100 independent trials per task."
tags = ["HCI", "Unity", "ML-Agents", "reinforcement learning", "PPO"]
categories = ["HCI"]
courses = ["HCI"]
source_files = ["HCI/Human Computer Interaction/LAB_homework/ML_agent/Lab1_Unity_ML_agent.pptx", "HCI/lab-ml-agents/README.md", "HCI/lab-ml-agents/experiment-notes.md", "HCI/lab-ml-agents/config/ppo.yaml", "HCI/lab-ml-agents/SignalChase/Assets/Scripts/RollerChaseAgent.cs", "HCI/lab-ml-agents/verification/summary.json", "HCI/lab-ml-agents/verification/random-evaluation.json", "HCI/lab-ml-agents/verification/trained-evaluation.json", "HCI/lab-ml-agents/verification/training-scalars.csv", "HCI/lab-ml-agents/verification/model-verification.json"]
+++

Signal Chase starts with a simple task: move a cyan sphere towards a gold target. The extension makes the target move and reflect from the platform edges. Both tasks use learned PPO policies, not a scripted chasing rule.

{{< portfolio-image src="images/hci/lab-1-ml-agents/chase-runtime.png" alt="A cyan learning agent and gold moving target on the Signal Chase platform, rendered from the running Windows player." >}}

*Runtime camera capture of the moving-target task. The desktop control overlay is not included in this capture.*

## From a fixed target to a moving one

The scene is a 10-by-10 platform. The agent observes the relative target position, its own velocity, the target velocity, and its position on the platform: eight values in total. Two continuous actions apply acceleration along X and Z.

A capture within 0.8 units gives +1 reward. Leaving the platform gives -1. A small distance-progress reward and time penalty guide learning between captures. Each attempt has a 10-second limit; falls and timeouts count as failures.

The moving target travels at 1.2 units per second. Including its velocity lets the policy react to motion rather than only follow a fixed location. In the desktop application, target control can also be enabled for WASD or arrow-key movement.

## Setup and a failed first run

The project uses Unity 6000.0.23f1, ML-Agents 4.0.0 and Python ML-Agents 1.1.0. Python runs in a separate environment on D:, without changing the existing Unity projects or Conda environments.

The first training run exposed a physics problem. Rotation was frozen, and default contact friction resisted small force commands. The agent often stayed still instead of making useful progress. More training alone was not the fix.

I gave the sphere and platform an explicit zero-friction material, keeping Rigidbody damping to control sliding. The second run used a new run ID, so its results stayed separate from the failed attempt.

Each policy then trained for about 200,000 steps, using 16 parallel arenas and a network with two hidden layers of 64 units. The CPU run took about five minutes on 15 October.

{{< portfolio-image src="images/hci/lab-1-ml-agents/training-curves.png" alt="Recorded PPO training curves for mean episode reward and policy entropy in the reaching and chasing tasks." >}}

*The second run's TensorBoard data. Reward improves for both tasks; the right panel shows policy entropy, not test success rate.*

## Independent checks

The final Windows player was tested twice: once with random actions and once with deterministic ONNX inference. Each run contained 100 attempts per task. Both used evaluation seed 20261015, different from training seed 742, with matching reset layouts and target headings.

<div role="region" aria-label="Policy evaluation results" tabindex="0" style="overflow-x:auto">

| Task | Random | Trained | Time |
| --- | --- | --- | --- |
| Static | 10/100 | 100/100 | 1.08 s |
| Moving | 18/100 | 100/100 | 1.19 s |

</div>

All attempts, including failures, are included. Time is the learned policy's mean capture time in simulated seconds. These are automatic trials with reflected target motion, not a usability study or a score against a human-controlled opponent. The result covers this evaluation seed and environment, not every possible target path.

The two exported models are about 24 KB each. They run inside Unity on the CPU, without a Python training process.

## Project files

- {{< portfolio-file src="files/hci/lab-1-ml-agents/signal-chase-source.zip" label="Download the Unity source, trained models and recorded checks" >}}
- {{< portfolio-file src="files/hci/lab-1-ml-agents/evaluation.csv" label="Download the evaluation summary" >}}

Open the SignalChase folder in Unity 6000.0.23f1. The archive includes the saved scene, models, training configuration and reproduction scripts. The earlier [Unity setup record]({{< relref "hci-lab-1-unity-setup.md" >}}) covers the basic environment; this post adds the learning task and its extension.
