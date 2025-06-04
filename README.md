# 🤖 RoboJackson: Imitation Learning Framework for Robotic Dance

RoboJackson is an end-to-end framework that teaches humanoid robots expressive dance movements by learning from short real-world videos. This project combines 3D pose estimation, motion retargeting, and reinforcement learning to enable lifelike, whole-body robotic dancing—starting from YouTube Shorts.

![Pipeline Overview](path/to/pipeline_image.png)

---

## Project Goals

- Extract 3D motion from trending YouTube dance videos.
- Retarget motion to a MuJoCo humanoid model.
- Train the robot using Truncated Quantile Critics (TQC) reinforcement learning.
- Demonstrate expressive, full-body movements learned from video.

---

## Core Components

### 1. Data Collection
- Uses `youtube-dl` to collect dance videos (<60s).
- Filters for quality using Google MediaPipe 2D pose estimation.
- Ranks videos by a custom pose stability score.

### 2. 3D Pose Estimation
- **HybrIK**: Predicts 3D SMPL pose and shape from monocular video.
- **NIKI**: Refines temporal coherence and resolves ambiguities.

### 3. Motion Retargeting
- Maps 29-DOF SMPL joints to 16-DOF MuJoCo humanoid.
- Applies scaling, interpolation, and smoothing for stability.

### 4. Reinforcement Learning
- **Algorithm**: Truncated Quantile Critics (TQC) from `sb3-contrib`.
- **Pretrained** on walking policy from HuggingFace.
- **Reward Terms**:
  - Imitation loss
  - Uprightness
  - Center-of-Mass (CoM) alignment
  - Curiosity (mild exploration encouragement)

---

##  Experiments

### Movements Evaluated
- **APT1**: Simple hip shake
- **APT2**: Full-body choreography
- **WALK**: Realistic locomotion

### Summary of Results

| Setup               | Faster Learning | Better Fidelity | Notes                         |
|--------------------|-----------------|-----------------|-------------------------------|
| No Pretraining      | ❌              | ❌              | Learning is unstable          |
| Pretrained Only     | ✅              | ✅              | Smooth imitation              |
| Pretrained + Curiosity | ✅              | ⚠️              | Great for dance, hinders walk |

---
