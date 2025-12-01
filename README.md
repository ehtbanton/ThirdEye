# ThirdEye
Edge AI for the visually impaired. See what you don't.

## 1. Overview
ThirdEye is a wearable assistive device for the visually impaired which increases situational awareness through audio feedback. It's a vision-enabled eye-tracking baseball cap connected to a mobile companion app for remote AI workflows.

Built into a baseball cap and powered by a Raspberry Pi Compute Module 4, the system runs real-time gaze tracking using an Edge Impulse model deployed locally at the edge. This gaze signal is used to interact with the environment through audio feedback, allowing users to understand what is around them.

_**Edge Impulse Project: [ThirdEye on Edge Impulse](https://studio.edgeimpulse.com/public/830287/live)**_\
_**Demo Video: [ThirdEye Demonstration Video](https://youtu.be/tBdOVURnGnc)**_\
_**Presentation: **_

## 2. What This Repository Contains
This repository includes:
- Source code for live inference on the CM4
- Preprocessing scripts for eye image extraction
- Links to the Edge Impulse project
- Documentation, pitch deck, and demo videos

## 3. System Architecture
### Hardware
#### Core compute
- Raspberry Pi Compute Module 4 (8GB RAM, 5GHz wireless)
- StereoPi V2 Slim carrier
#### Cameras & audio
- 2x Raspberry Pi Camera V3 Wide (1080p30, 120° FOV)
- 1x Arducam USB mini webcam (1080p30, 75° FOV + mic)
- Bone conduction surface transducer
#### Power & mechanical
- Cableless USB-C battery pack, or with wired connection and no battery
- Baseball cap mounting system (majority of electronics in the visor)

**Edge device for the track: Raspberry Pi CM4 running Linux + Edge Impulse Linux SDK.**

### Software
- Python inference script
- Edge Impulse model (Convolutional Neural Network)

### Edge Impulse model - Gaze Classifier
- **Project:** [link to project]
- **Type:** Image Classification (2D CNN)
- **Input:**
  - Eye crop from the camera
  - Size: 96x96 pixels
  - Colour: Grayscale
- **Output classes:**
  - `{1: far left, 2: left, 3: center, 4: right, 5: far right}`
- **Architecture:**
  - Input layer: 9216 features
  - Conv2D + pooling:
      - Block 1: 16 filters, 3 kernel size, 1 layer
      - Block 1: 32 filters, 3 kernel size, 1 layer
      - Block 1: 64 filters, 3 kernel size, 1 layer
  - Flatten
  - Dense
  - Dropout: rate 0.25
  - Output dense: 5 neurons
- **Training:**
  - Samples:
  - Train/validation split:
  - Training cycles:
  - Learning rate:

#### Dataset
Self-recorded 30 fps video from the eye camera, subsampled at 10Hz. Extracted frames were cropped to a fixed eye region and resized to 96x96. Each crop manually labelled into one of five horizontal bins based on reference point. All images are self captured by the team and are **not** from third-party datasets.

### IMPORTANT - PLEASE NOTE
**Dataset is not public in this repository - contact the owner.**  
For privacy purposes, the linked project contains an imported version of the original Edge Impulse model only. **The full original project and dataset can be made available to judges upon request under controlled access.**
