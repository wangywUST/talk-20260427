---
theme: dracula
title: Signal is Physics
info: |
  Group Meeting Talk · 2026
highlighter: shiki
drawings:
  persist: false
transition: slide-left
mdc: true
download: true
fonts:
  sans: Noto Serif SC
  mono: Noto Serif SC
---

<span class="title-slide-marker"></span>

# Signal is Physics
## Structured Reasoning for Multimodal World Understanding

**Yiwei Wang** · University of California, Merced

May 2026

![UC Merced](/Image/uc_yellow.svg)

---

# Three Questions, One Principle

- ① Given multiple microphones, can we tell where a sound is coming from?

- ② Given a video, can AI tell whether the camera is pushing forward or rotating?

- ③ Given an underwater sonar array, can AI reconstruct a target's position from multi-transducer signals?

→ These three questions are, fundamentally, the same question.

![Figure](/Image/fig_1.png)

---

# Signal is Physics

Audio  =  Spatiotemporal encoding of pressure waves

Image  =  2D projection of a light field

Video  =  Continuous sampling of spatiotemporal dynamics

The structure of a signal is the structure of physical law.

![Figure](/Image/fig_2.png)

---

# Do Models Really Understand This?

### How Current Models Work

**Statistical pattern matching**: inputs similar to those seen during training tend to produce similar outputs. Without an explicit **physical prior**, they can fail systematically on **out-of-distribution** cases.

### Our Claim

Signals are not just observations; they are traces of physical processes. Reasoning over them should therefore preserve physical operations and produce steps that can be interpreted and verified.

![Figure](/Image/fig_3.png)

---

# Part 1 · Perception ≠ Understanding

![Figure](/Image/fig_23.png)

---

# Capability Boundary of Current Multimodal AI

### What Models Have Achieved

- Image recognition and generation: near or beyond human-level
- Video QA and cross-modal retrieval: rapid progress
- Speech understanding and audio generation: fast breakthroughs

### But There Are Systematic Failures in Physical Constraint Reasoning

- Cannot perceive the spatial motion direction of a sound source
- Systematic temporal misalignment between audio and video
- Longer reasoning chains can drift further from physical truth

Scale and data alone cannot fix a missing understanding of physics.

---

# What Are Physical Constraints?

#### Spatial Constraints

Perspective, occlusion, parallax

The 3D spatial layout of objects leaves deterministic traces in 2D images.

#### Temporal Constraints

Motion continuity, causal order

Physical events on the time axis must obey causality — they cannot be reversed.

#### Multi-source Constraints

Observations of the same physical event across multiple signal sources must be mutually consistent.

Multi-source constraints cover: cross-modal (visual + audio) and cross-sensor (multi-microphone / multi-camera / multi-transducer).

---

# Evidence 1 · Spatial Blind Spot

## Audio LLMs Cannot Perceive Sound Source Direction

### Key Finding

- When a sound source moves from left to right, the model can barely determine the direction
- Accuracy approaches random-chance level

### Physical Interpretation
The **inter-microphone time delay** encodes complete spatial information — yet the model does not use it at all.

Conclusion: The model is listening, but not reasoning about space.

![Figure](/Image/fig_4.png)

<footer>Spatial Blind Spot: Auditory Motion Perception Deficits in Audio LLMs. Zhe Sun, Yujun Cai, Jiayu Yao, Yiwei Wang. 2025</footer>

---

# Evidence 2 · Not in Sync

## Systematic Temporal Bias in Audio Chat Models

### Key Finding

- Models show a significant, systematic bias in localizing audio events in time
- The bias does not improve with model scale

### Physical Interpretation
Audio and video describe **the same physical event** — temporal inconsistency means the model has lost the physical causal chain.

Conclusion: The model sees the frames, but loses the physical meaning of temporal order.

![Figure](/Image/fig_6.png)

<footer>Not in Sync: Unveiling Temporal Bias in Audio Chat Models · J Yao, S Liu, Y Wang, R Cheng, L Mei, B Bi, Z Xiong, X Cheng</footer>

---

# Evidence 3 · Fragile Visual Reasoning

## Visual CoT Makes VLMs Smarter but More Fragile

### Key Finding

- Visual chain-of-thought simultaneously introduces new, systematic error patterns
- More reasoning steps → certain errors become worse

### Physical Interpretation

The reasoning chain is not anchored to physical constraints, so the longer it runs, the more it drifts.

Conclusion: More reasoning steps ≠ better physical understanding.

![Figure](/Image/fig_7.png)

<footer>Visual CoT Makes VLMs Smarter but More Fragile · Chunxue Xu, Yiwei Wang, Yujun Cai, Bryan Hooi, Songze Li</footer>

---

# Problem Framework

**The gap**: middle layer → top layer lacks physical priors. This is where our work begins.

![Figure](/Image/fig_8.png)

---

# Part 2 · Structured Reasoning & Multi-source Consistency

![Figure](/Image/fig_24.png)

---

# Three Forms of Structured Reasoning

The reasoning process is **transparent and interpretable** with respect to physical constraints.

| Form | Mechanism | Representative Work |
|------|-----------|-------------------|
| Reasoning Chain | Each step maps to a physical operation | ViewFusion, Thinking with Sound |
| Path Selection | RL learns physically consistent reasoning order | CamReasoner, AudioRouter |
| Structure Injection | Hard-coded physical constraints injected into reasoning | PAS (Phase Aggregated Smoothing) |

---

# What Is Multi-source Consistency?

Core principle: The physical world is singular. Any set of independent observations of it must yield mutually consistent conclusions.

```text
Visual reasoning chain    ──┐
Audio reasoning chain     ──┤
Microphone array          ──┼──→  Consistency Check  ──→  Physical Truth Confirmed
Multi-view cameras        ──┤              ↑
Underwater transducers    ──┘     Inconsistent → Re-reason
```

Analogy: Multiple independent witnesses in court — consistent testimony is credible; contradiction reveals the flaw.

---

# Part 3 · Spatial Reasoning

![Figure](/Image/fig_25.png)

---

# The Challenge of Spatial Reasoning

### Why Is Spatial Reasoning Hard?

Insufficient Single-frame Information

Depth is lost in projection; a single image cannot determine 3D position.

Viewpoint Dependence

The same scene leads to completely different spatial descriptions from different viewpoints.

Occlusion

Spatial relations of hidden parts can only be inferred from constraints.

**Our approach**: use structured reasoning chains to make spatial relations explicit.

→ This is Signal is Physics instantiated on the visual channel.

---

# ViewFusion · Multi-view Spatial Reasoning Chain

### Task

Spatial relation QA under multi-view settings

### Core Innovation

Structured Spatial Thinking Chain — each reasoning step maps to a spatial geometric operation and is verifiable.

### Results

Significantly outperforms baselines on multi-view spatial reasoning benchmarks.

![Figure](/Image/fig_9.png)

<footer>ViewFusion: Structured Spatial Thinking Chains for Multi-View Reasoning. Xingjian Tao, Yiwei Wang, Yujun Cai, Yifan Song, Jing Tang. 2026</footer>

---

# ViewFusion · Physical Significance

### Reasoning Step → Physical Operation

### Multi-source Consistency

Conclusions from different viewpoints must be geometrically consistent.

Conclusion: The reasoning structure is the linguistic expression of spatial physical constraints.

| Reasoning Step | Physical Operation |
|------------|------------------------------|
| Coordinate alignment | Extrinsic matrix transform |
| Triangulation | Multi-view geometry |
| Relation inference | 3D spatial computation |

![Figure](/Image/fig_10.png)

<footer>ViewFusion: Structured Spatial Thinking Chains for Multi-View Reasoning. Xingjian Tao, Yiwei Wang, Yujun Cai, Yifan Song, Jing Tang. 2026</footer>

---

# CamReasoner · Camera Motion Understanding

![Figure](/Image/fig_11.png)

<footer>CamReasoner: Reinforcing Camera Movement Understanding via Structured Spatial Reasoning. Hang Wu, Yujun Cai, Zehao Li, Haonan Ge, Bowen Sun, Junsong Yuan, Yiwei Wang. 2026</footer>

---

# CamReasoner · Physical Significance

### Camera Motion Is a Direct Visual Carrier of Physical Constraints

Every camera motion corresponds to a deterministic 3D geometric transformation.

The video frame sequence must be physically consistent with that transformation.

### Role of RL

Not learning "which answer is correct", but learning "which reasoning path is consistent with physical motion laws".

### Benefit

Reasoning paths that violate physical constraints are penalized, forcing the model to internalize physical laws.

Conclusion: Understanding camera motion is the first step toward understanding visual physics.

<footer>CamReasoner: Reinforcing Camera Movement Understanding via Structured Spatial Reasoning. Hang Wu, Yujun Cai, Zehao Li, Haonan Ge, Bowen Sun, Junsong Yuan, Yiwei Wang. 2026</footer>

---

# Spatial Reasoning — Summary

### Position in the Framework

### Connecting to Core Themes

**Signal is Physics**: Spatial reasoning recovers 3D physical space from image signals.

**Multi-source**: Geometric consistency across viewpoints is the validator for spatial reasoning.

Spatial reasoning answers "**where**".

→ Temporal reasoning answers "**when**".

| Work | Problem Solved |
|------|---------------|
| ViewFusion | Multi-view geometric consistency |
| CamReasoner | Physical understanding of camera motion |

---

# Part 4 · Temporal Reasoning

![Figure](/Image/fig_26.png)

---

# The Challenge of Temporal Reasoning

### Why Is Temporal Reasoning Particularly Hard?

**Frame Sampling Loses Information**

Video is a discrete sampling of continuous time; events between frames are invisible.

Non-uniform sampling further blurs temporal relations.

**Systematic Bias in Positional Encoding**

Existing models have known biases in temporal positional encoding, leading to systematic offsets in perceived event timing.

**Our approach**: calibrate temporal perception without retraining.

→ Temporal continuity is the most fundamental physical constraint on video signals.

---

# PAS · Phase Aggregated Smoothing

### Task

Temporal encoding bias in Video LLMs

### Core Innovation

Training-free stabilizer

Injects temporal physical constraints directly at inference time, no retraining required.

### Results

Significantly reduces temporal perception bias; improves temporal QA accuracy.

Conclusion: Temporal continuity is the foundational guarantee of physical fidelity.

![Figure](/Image/fig_12.png)

<footer>PAS: A Training-Free Stabilizer for Temporal Encoding in Video LLMs. Bowen Sun, Yujun Cai, Ming-Hsuan Yang, Hang Wu, Yiwei Wang. 2026</footer>

---

# PAS · How It Works

Video LLMs accumulate **positional encoding bias** — frames are perceived at wrong temporal locations. PAS corrects this at inference time by enforcing smooth, monotonically increasing temporal positions. **Training-free**, no fine-tuning required.

![Figure](/Image/fig_13.png)

<footer>PAS: A Training-Free Stabilizer for Temporal Encoding in Video LLMs. Bowen Sun, Yujun Cai, Ming-Hsuan Yang, Hang Wu, Yiwei Wang. 2026</footer>

---

# FrameMind · Inter-frame Reasoning with RL

**Task**: Video frame interleaved reasoning. **Core idea**: adjacent frames are temporal samples of the same physical scene — reasoning across them must respect physical causality, enforced via RL rewards.

![Figure](/Image/fig_14.png)

<footer>FrameMind: Frame-Interleaved Video Reasoning via Reinforcement Learning. Haonan Ge, Yiwei Wang, Kai-Wei Chang, Hang Wu, Yujun Cai. 2025</footer>

---

# FrameMind · Causal Consistency Check

RL rewards reasoning paths that are physically causal; inconsistent inter-frame transitions incur penalties and trigger model self-correction.

![Figure](/Image/fig_15.png)

<footer>FrameMind: Frame-Interleaved Video Reasoning via Reinforcement Learning. Haonan Ge, Yiwei Wang, Kai-Wei Chang, Hang Wu, Yujun Cai. 2025</footer>

---

# Deeper Meaning of Temporal Reasoning

Reasoning on the time axis = Modeling the **physical causal chain**

**Intuitive example**: a glass shattering

Temporal reasoning can tell us:
- Magnitude of the impact force (inferred from sound intensity and fracture pattern)
- Material properties (inferred from the fracture mode)
- Motion trajectory (inferred from the frame sequence)

Causal order is one of the most fundamental constraints of the physical world.

---

# Temporal Reasoning — Summary

### Position in the Framework

### Connecting to Core Themes

**Signal is Physics**: Temporal reasoning recovers the physical causal chain from video signals.

**Multi-source**: Audio-video timestamp alignment is the validator for temporal reasoning.

Space and time are both addressed.

→ Now let multiple signal sources **verify each other**.

| Work | Problem Solved |
|------|---------------|
| PAS | Calibration of temporal positional encoding bias |
| FrameMind | Inter-frame causal reasoning and decision-making |

---

# Part 5 · Implementing Multi-source Consistency

![Figure](/Image/fig_27.png)

---

# From Single-source Reasoning to Multi-source Validation

### Recap

Spatial and temporal reasoning are both structured reasoning **within a single channel**.

- ViewFusion: spatial reasoning within the visual channel
- PAS / FrameMind: causal reasoning along the time dimension

### New Question

How do different signal sources validate each other?

**Physical basis**: the same physical event leaves **redundant but consistent** traces across multiple signal sources.

This redundancy is a natural verification resource.

The same sound is recorded by multiple microphones; the same scene is captured by multiple cameras. They all describe the same physical truth.

---

# Audio as an Independent Reasoning Channel

### Unique Physical Properties of Audio

Audio = spatiotemporal encoding of pressure waves, carrying complete spatial geometry. Audio is a severely underestimated reasoning channel.

![Figure](/Image/fig_16.png)

---

# Thinking with Sound · Audio Reasoning Chain

Audio chain-of-thought for multimodal reasoning. Each reasoning step maps to an acoustic physical operation.

Conclusion: Audio is not just a feature — it can carry complete reasoning logic.

![Figure](/Image/fig_17.png)

<footer>Thinking with sound: Audio chain-of-thought enables multimodal reasoning in large audio-language models. Zhen Xiong, Yujun Cai, Zhecheng Li, Junsong Yuan, Yiwei Wang. 2025</footer>

---

# AudioRouter · Audio-only Chain-of-Thought Reasoning

RL trains the model to route each reasoning step through the appropriate acoustic operation, producing interpretable and physically grounded audio reasoning chains.

![Figure](/Image/fig_18.png)

<footer>AudioRouter: Data Efficient Audio Understanding via RL based Dual Reasoning. Liyang Chen, Hongkai Chen, Yujun Cai, Sifan Li, Qingwen Ye, Yiwei Wang. 2026</footer>

---

# AudioRouter · Results

RL-guided routing consistently outperforms chain-of-thought baselines across audio reasoning benchmarks, with gains especially pronounced on spatial and temporal acoustic tasks.

![Figure](/Image/fig_19.png)

<footer>AudioRouter: Data Efficient Audio Understanding via RL based Dual Reasoning. Liyang Chen, Hongkai Chen, Yujun Cai, Sifan Li, Qingwen Ye, Yiwei Wang. 2026</footer>

---

# Multi-source Consistency — Unified View

All signal channels converge at a **Consistency Check**: agreement confirms physical truth; inconsistency triggers re-reasoning. Underwater acoustics simultaneously validates cross-modal and cross-sensor inputs, making it the hardest and most complete test of this framework.

![Figure](/Image/fig_20.png)

---

# Multi-source Reasoning — Summary

**Signal is Physics**: Multi-source consistency reasoning verifies whether multiple independent observations describe the same physical truth.

### Core Claim Formally Established

**Multi-source Consistency is the Validator of Physical Truth**

Where can this framework be applied?

---

# Part 6 · Looking Up: From Reasoning to Action

---

# Reasoning-Driven Decision Making

Physical signal input → structured reasoning → planning → RL optimization → execution. The reasoning chain is not a byproduct — it directly generates the action sequence.

Conclusion: The endpoint of physical reasoning is reliable action.

![Figure](/Image/fig_21.png)

---

# GUI and Embodied Scenarios

### Dimo-gui

Visual reasoning drives GUI interaction

Understanding the visual-physical structure of a UI → reliably executing action sequences.

### CamReasoner in Embodied Navigation

Camera motion understanding → spatial reasoning about the robot's own motion

Understanding "where am I" and "where am I going".

### Multi-source Connection

An embodied agent must integrate:

- Vision (camera)
- Touch (force sensor)
- Motion (IMU, encoder)
- Audio (ambient sound)

Multi-sensor signals must be physically consistent to support reliable decision-making.

Conclusion: Physical reasoning is the cognitive foundation of embodied intelligence.

---

# The Complete Chain: From Signal to Action

This is the complete research framework we have built. Every step practices **Signal is Physics**.

![Figure](/Image/fig_22.png)

---

# Part 7 · Underwater Acoustics AI: The Ultimate Test

![Figure](/Image/fig_29.png)

---

# Why Underwater Acoustics Is the Ultimate Test

### Extreme Physical Constraints

- **Multipath reflections**: complex propagation paths in water
- **Temperature gradients**: sound speed changes continuously with depth
- **Limited visual aid**: poor visibility.
- **Extremely high noise**: low SNR, strong background interference

### Connecting to Core Themes

**Signal is Physics**: Underwater acoustics is the most extreme embodiment of "signal is physics" — only acoustic signals and physical laws, no other assistance.

**Multi-source**: Every transducer in a sonar array is an independent observation; their consistency is the sole basis for target localization.

Underwater acoustics pushes every assumption of our framework to the limit.

---

# Applications of Underwater Acoustics AI

### Ocean Exploration

Deep-sea species detection, marine environment monitoring, acoustic tomography.

### Underwater Autonomous Systems

AUV navigation, underwater communication, cooperative operations.

### Seabed Resource Survey

Mineral localization, pipeline inspection, geological structure analysis.

**Status**: lowest AI penetration, most complex physical modeling, highest application value.

**Opportunity**: precisely because AI has not yet entered this domain, first-mover advantage is enormous.

---

# Methodology Transfer

Conclusion: We are not starting from scratch — we are entering a new domain with a validated toolbox.

| Existing Capability | Underwater Acoustics Mapping |
|--------------------|------------------------------|
| Multi-view spatial reasoning (ViewFusion) | Array localization: inter-transducer time delays → source direction |
| Temporal stability calibration (PAS) | Multipath suppression: separating direct arrivals from reflections |
| Audio reasoning chain (Thinking with Sound) | Underwater feature analysis: from raw IQ signals to target reconstruction |

---

# Part 8 · Conclusion

---

# Our Research Landscape

Perception layer reveals the **problems**.

Reasoning layer provides the **methods**.

Decision layer validates the **value**.

| Layer | Works |
|-------|-------|
| **Perception Layer** | Spatial Blind Spot · Not in Sync · Visual CoT |
| **Reasoning Layer** | ViewFusion · CamReasoner · PAS · Thinking with Sound · AudioRouter |
| **Decision Layer** | Dimo-gui · CamReasoner |

---

# Core Claims

Signal is Physics

Structured Reasoning is the Language of Physical Constraints

Multi-source Consistency is the Validator of Physical Truth

---

# Thank You!

Questions and discussion welcome.

wangyw.evan@gmail.com

![UC Merced](/Image/uc_yellow.svg)
