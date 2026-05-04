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

# Signal is Physics
## Structured Reasoning for Multimodal World Understanding

**Yiwei Wang** · University of California, Merced

<div class="pt-4 text-gray-400">
May 2026
</div>

<img src="/Image/uc_yellow.svg" class="absolute top-8 right-8 h-16" />

---

# Three Questions, One Principle

<div class="flex flex-col h-full pt-2">

<v-clicks>

<div class="text-base font-bold mb-2">① &nbsp;Given multiple microphones, can we tell where a sound is coming from?</div>

<div class="text-base font-bold mb-2">② &nbsp;Given a video, can AI tell whether the camera is pushing forward or rotating?</div>

<div class="text-base font-bold mb-2">③ &nbsp;Given an underwater sonar array, can AI reconstruct a target's position from multi-transducer signals?</div>

</v-clicks>

<div v-click class="mt-1 text-sm text-gray-500 italic">
→ These three questions are, fundamentally, the same question.
</div>

<img v-click src="/Image/fig_1.png" class="mt-3 w-full object-contain max-h-72" />

</div>

---

# Signal is Physics

<v-clicks>

<div class="text-2xl mt-4">Audio &nbsp;=&nbsp; Spatiotemporal encoding of pressure waves</div>

<div class="text-2xl mt-4">Image &nbsp;=&nbsp; 2D projection of a light field</div>

<div class="text-2xl mt-4">Video &nbsp;=&nbsp; Continuous sampling of spatiotemporal dynamics</div>

</v-clicks>

<div v-click class="pt-4 text-center text-lg text-gray-500">
The structure of a signal is the structure of physical law.
</div>

<img v-click src="/Image/fig_2.png" class="mt-4 w-full object-contain max-h-52" />

---

# Do Models Really Understand This?

<div class="flex gap-8 mt-6">

<div class="flex-1 flex flex-col">

### How Current Models Work

Statistical pattern matching

- Similar input seen before → similar output
- No physical prior
- Systematic failure on out-of-distribution cases

<img src="/Image/fig_3.png" class="mt-4 w-full object-contain max-h-52" />

</div>

<div class="flex-1">

### Our Claim

Signals are encodings of physical processes and should be reasoned about as such.

- Each reasoning step maps to a physical operation
- Multi-source signals must be mutually consistent
- Reasoning is interpretable and verifiable

<div class="mt-6 p-4 bg-gray-100 rounded text-center text-gray-700">
Analogy: Memorizing answers vs. understanding the formula
</div>

<div class="mt-4 text-center text-gray-500">
→ This is the problem structured reasoning is built to solve.
</div>

</div>

</div>

---

# Part 1 · Perception ≠ Understanding

<img src="/Image/fig_23.png" class="w-full object-contain max-h-88 mt-4" />

---

# The Capability Boundary of Current Multimodal AI

### What Models Have Achieved

- Image recognition and generation: near or beyond human-level
- Video QA and cross-modal retrieval: rapid progress
- Speech understanding and audio generation: fast breakthroughs

<div class="mt-6 p-4 border-l-4 border-red-400 bg-red-50 text-gray-700">

### But There Are Systematic Failures in Physical Constraint Reasoning

- Cannot perceive the spatial motion direction of a sound source
- Systematic temporal misalignment between audio and video
- Longer reasoning chains can drift further from physical truth

</div>

<div class="mt-4 text-gray-500 text-center">
Scale and data alone cannot fix a missing understanding of physics.
</div>

---

# What Are Physical Constraints?

<div class="grid grid-cols-3 gap-3 mt-8">

<div class="p-3 border rounded">

#### Spatial Constraints

Perspective, occlusion, parallax

The 3D spatial layout of objects leaves deterministic traces in 2D images.

</div>

<div class="p-3 border rounded">

#### Temporal Constraints

Motion continuity, causal order

Physical events on the time axis must obey causality — they cannot be reversed.

</div>

<div class="p-3 border rounded">

#### Multi-source Constraints

Observations of the same physical event across multiple signal sources must be mutually consistent.

</div>

</div>

<div class="mt-6 text-gray-500 text-sm">
Multi-source constraints cover: cross-modal (visual + audio) and cross-sensor (multi-microphone / multi-camera / multi-transducer).
</div>

---

# Evidence 1 · Spatial Blind Spot

## Audio LLMs Cannot Perceive Sound Source Direction

<div class="grid grid-cols-2 gap-8 mt-6">

<div>

### Key Finding

- When a sound source moves from left to right, the model can barely determine the direction
- Accuracy approaches random-chance level

### Physical Interpretation
The **inter-microphone time delay** encodes complete spatial information — yet the model does not use it at all.

</div>

<div class="flex items-center justify-center">

<img src="/Image/fig_4.png" class="w-full object-contain max-h-64" />

</div>

</div>

<div class="mt-4 p-3 bg-yellow-50 border-l-4 border-yellow-400 text-gray-700">
Conclusion: The model is listening, but not reasoning about space.
</div>

<div class="absolute bottom-1 left-1 right-10 text-xs text-gray-400">
Spatial Blind Spot: Auditory Motion Perception Deficits in Audio LLMs. Zhe Sun, Yujun Cai, Jiayu Yao, Yiwei Wang. 2025
</div>

---

# Evidence 2 · Not in Sync

## Systematic Temporal Bias in Audio Chat Models

<div class="grid grid-cols-2 gap-8 mt-6">

<div>

### Key Finding

- Models show a significant, systematic bias in localizing audio events in time
- The bias does not improve with model scale

### Physical Interpretation
Audio and video describe **the same physical event** — temporal inconsistency means the model has lost the physical causal chain.

</div>

<div class="relative w-full" style="height: 14rem;">

<img src="/Image/fig_5.png" class="absolute top-0 w-full object-contain object-top transition-all duration-500" :class="$clicks >= 1 ? 'blur-sm opacity-50' : ''" style="max-height: 14rem;" />

<img v-click src="/Image/fig_6.png" class="absolute w-full object-contain object-top rounded shadow-lg" style="top: 4rem; max-height: 13rem; background: white;" />

</div>

</div>

<div class="mt-4 p-3 bg-yellow-50 border-l-4 border-yellow-400 text-gray-700">
Conclusion: The model sees the frames, but loses the physical meaning of temporal order.
</div>

<div class="absolute bottom-1 left-1 right-10 text-xs text-gray-400">
Not in Sync: Unveiling Temporal Bias in Audio Chat Models · J Yao, S Liu, Y Wang, R Cheng, L Mei, B Bi, Z Xiong, X Cheng
</div>

---

# Evidence 3 · Fragile Visual Reasoning

## Visual CoT Makes VLMs Smarter but More Fragile

<div class="relative mt-3">

<div class="grid grid-cols-2 gap-3">

<div>

### Key Finding

- Visual chain-of-thought simultaneously introduces new, systematic error patterns
- More reasoning steps → certain errors become worse

### Physical Interpretation

The reasoning chain is not anchored to physical constraints, so the longer it runs, the more it drifts.

</div>

<img src="/Image/fig_7.png" class="w-full h-auto object-contain object-top" />

</div>

<div v-click class="absolute bottom-0 left-0 right-0 p-3 bg-yellow-50 border-l-4 border-yellow-400 text-gray-700 float-up">
Conclusion: More reasoning steps ≠ better physical understanding.
</div>

</div>

<div class="absolute bottom-1 left-1 right-10 text-xs text-gray-400">
Visual CoT Makes VLMs Smarter but More Fragile · Chunxue Xu, Yiwei Wang, Yujun Cai, Bryan Hooi, Songze Li
</div>

---

# Problem Framework

<div class="flex flex-col items-center mt-2">

<img src="/Image/fig_8.png" class="w-full max-h-80 object-contain" />

<div class="mt-4 p-3 bg-red-50 border-l-4 border-red-400 text-gray-700 text-sm w-full">

**The gap**: middle layer → top layer lacks physical priors. This is where our work begins.

</div>

</div>

---

# Part 2 · Structured Reasoning & Multi-source Consistency

<img src="/Image/fig_24.png" class="w-full object-contain max-h-88 mt-4" />

---

# Three Forms of Structured Reasoning

| Form | Mechanism | Representative Work |
|------|-----------|-------------------|
| Reasoning Chain | Each step maps to a physical operation | ViewFusion, Thinking with Sound |
| Path Selection | RL learns physically consistent reasoning order | CamReasoner, AudioRouter |
| Structure Injection | Hard-coded physical constraints injected into reasoning | PAS (Phase Aggregated Smoothing) |

<div class="mt-8 p-4 bg-gray-100 rounded text-gray-700">

The reasoning process is **transparent and interpretable** with respect to physical constraints.

</div>

---

# What Is Multi-source Consistency?

<div class="mt-4 p-4 bg-blue-50 border-l-4 border-blue-400 text-gray-700">
Core principle: The physical world is singular. Any set of independent observations of it must yield mutually consistent conclusions.
</div>

<pre class="mt-6 font-mono text-sm p-4 bg-gray-100 rounded text-gray-700 leading-relaxed" style="font-family: monospace; background: #f3f4f6; color: #374151;">Visual reasoning chain    ──┐
Audio reasoning chain     ──┤
Microphone array          ──┼──→  Consistency Check  ──→  Physical Truth Confirmed
Multi-view cameras        ──┤              ↑
Underwater transducers    ──┘     Inconsistent → Re-reason</pre>

<div class="mt-6 text-center text-gray-500">
Analogy: Multiple independent witnesses in court — consistent testimony is credible; contradiction reveals the flaw.
</div>

---

# Part 3 · Spatial Reasoning

<img src="/Image/fig_25.png" class="w-full object-contain max-h-88 mt-4" />

---

# The Challenge of Spatial Reasoning

### Why Is Spatial Reasoning Hard?

<div class="grid grid-cols-3 gap-4 mt-6">

<div class="p-4 border rounded text-center">
<strong>Insufficient Single-frame Information</strong>

Depth is lost in projection; a single image cannot determine 3D position.
</div>

<div class="p-4 border rounded text-center">
<strong>Viewpoint Dependence</strong>

The same scene leads to completely different spatial descriptions from different viewpoints.
</div>

<div class="p-4 border rounded text-center">
<strong>Occlusion</strong>

Spatial relations of hidden parts can only be inferred from constraints.
</div>

</div>

<div class="mt-8 p-4 bg-blue-50 border-l-4 border-blue-400 text-gray-700">

**Our approach**: use structured reasoning chains to make spatial relations explicit.

→ This is Signal is Physics instantiated on the visual channel.

</div>

---

# ViewFusion · Multi-view Spatial Reasoning Chain

<div class="grid grid-cols-3 gap-6 mt-4">

<div class="p-3 bg-gray-50 rounded border">

### Task

Spatial relation QA under multi-view settings

</div>

<div class="p-3 bg-blue-50 rounded border">

### Core Innovation

Structured Spatial Thinking Chain — each reasoning step maps to a spatial geometric operation and is verifiable.

</div>

<div class="p-3 bg-green-50 rounded border">

### Results

Significantly outperforms baselines on multi-view spatial reasoning benchmarks.

</div>

</div>

<img src="/Image/fig_9.png" class="absolute bottom-4 left-2 right-2 w-[calc(100%-1rem)] object-contain max-h-52" />

<div class="absolute bottom-1 left-1 right-10 text-xs text-gray-400">
ViewFusion: Structured Spatial Thinking Chains for Multi-View Reasoning. Xingjian Tao, Yiwei Wang, Yujun Cai, Yifan Song, Jing Tang. 2026
</div>

---

# ViewFusion · Physical Significance

<div class="grid grid-cols-2 gap-8 mt-8">

<div>

### Reasoning Step → Physical Operation

| Coordinate alignment | Extrinsic matrix transform |
|------------|------------------------------|
| Triangulation | Multi-view geometry |
| Relation inference | 3D spatial computation |

</div>

<div class="flex flex-col gap-3">

### Multi-source Consistency

Conclusions from different viewpoints must be geometrically consistent.

<img src="/Image/fig_10.png" class="w-full object-contain max-h-52 mt-0 mb-0" />

</div>

</div>

<div class="mt-6 p-3 bg-blue-50 border-l-4 border-blue-400 text-gray-700">
Conclusion: The reasoning structure is the linguistic expression of spatial physical constraints.
</div>

<div class="absolute bottom-1 left-1 right-10 text-xs text-gray-400">
ViewFusion: Structured Spatial Thinking Chains for Multi-View Reasoning. Xingjian Tao, Yiwei Wang, Yujun Cai, Yifan Song, Jing Tang. 2026
</div>

---

# CamReasoner · Camera Motion Understanding

<img src="/Image/fig_11.png" class="w-full object-contain mt-0" />

<div class="absolute bottom-1 left-1 right-10 text-xs text-gray-400">
CamReasoner: Reinforcing Camera Movement Understanding via Structured Spatial Reasoning. Hang Wu, Yujun Cai, Zehao Li, Haonan Ge, Bowen Sun, Junsong Yuan, Yiwei Wang. 2026
</div>

---

# CamReasoner · Physical Significance

<div class="mt-8">

### Camera Motion Is a Direct Visual Carrier of Physical Constraints

Every camera motion corresponds to a deterministic 3D geometric transformation.

The video frame sequence must be physically consistent with that transformation.

</div>

<div class="mt-6 grid grid-cols-2 gap-8">

<div class="p-4 border rounded">

### Role of RL

Not learning "which answer is correct", but learning "which reasoning path is consistent with physical motion laws".

</div>

<div class="p-4 border rounded">

### Benefit

Reasoning paths that violate physical constraints are penalized, forcing the model to internalize physical laws.

</div>

</div>

<div class="mt-6 p-3 bg-blue-50 border-l-4 border-blue-400 text-gray-700">
Conclusion: Understanding camera motion is the first step toward understanding visual physics.
</div>

<div class="absolute bottom-1 left-1 right-10 text-xs text-gray-400">
CamReasoner: Reinforcing Camera Movement Understanding via Structured Spatial Reasoning. Hang Wu, Yujun Cai, Zehao Li, Haonan Ge, Bowen Sun, Junsong Yuan, Yiwei Wang. 2026
</div>

---

# Spatial Reasoning — Summary

<div class="grid grid-cols-2 gap-8 mt-6">

<div>

### Position in the Framework

| Work | Problem Solved |
|------|---------------|
| ViewFusion | Multi-view geometric consistency |
| CamReasoner | Physical understanding of camera motion |

</div>

<div>

### Connecting to Core Themes

**Signal is Physics**: Spatial reasoning recovers 3D physical space from image signals.

**Multi-source**: Geometric consistency across viewpoints is the validator for spatial reasoning.

</div>

</div>

<div class="mt-8 p-4 bg-green-50 border-l-4 border-green-400 text-gray-700">

Spatial reasoning answers "**where**".

→ Temporal reasoning answers "**when**".

</div>

---

# Part 4 · Temporal Reasoning

<img src="/Image/fig_26.png" class="w-full object-contain max-h-88 mt-4" />

---

# The Challenge of Temporal Reasoning

### Why Is Temporal Reasoning Particularly Hard?

<div class="grid grid-cols-2 gap-6 mt-6">

<div class="p-4 border rounded">

**Frame Sampling Loses Information**

Video is a discrete sampling of continuous time; events between frames are invisible.

Non-uniform sampling further blurs temporal relations.

</div>

<div class="p-4 border rounded">

**Systematic Bias in Positional Encoding**

Existing models have known biases in temporal positional encoding, leading to systematic offsets in perceived event timing.

</div>

</div>

<div class="mt-8 p-4 bg-blue-50 border-l-4 border-blue-400 text-gray-700">

**Our approach**: calibrate temporal perception without retraining.

→ Temporal continuity is the most fundamental physical constraint on video signals.

</div>

---

# PAS · Phase Aggregated Smoothing

<div class="grid grid-cols-2 gap-8 mt-6">

<div>

### Task

Temporal encoding bias in Video LLMs

### Core Innovation

Training-free stabilizer

Injects temporal physical constraints directly at inference time, no retraining required.

### Results

Significantly reduces temporal perception bias; improves temporal QA accuracy.

</div>

<img src="/Image/fig_12.png" class="w-full object-contain max-h-52" />

</div>

<div class="mt-4 p-3 bg-blue-50 border-l-4 border-blue-400 text-gray-700">
Conclusion: Temporal continuity is the foundational guarantee of physical fidelity.
</div>

<div class="absolute bottom-1 left-1 right-10 text-xs text-gray-400">
PAS: A Training-Free Stabilizer for Temporal Encoding in Video LLMs. Bowen Sun, Yujun Cai, Ming-Hsuan Yang, Hang Wu, Yiwei Wang. 2026
</div>

---

# PAS · How It Works

Video LLMs accumulate **positional encoding bias** — frames are perceived at wrong temporal locations. PAS corrects this at inference time by enforcing smooth, monotonically increasing temporal positions. **Training-free**, no fine-tuning required.

<img src="/Image/fig_13.png" class="w-full object-contain max-h-88 mt-3" />

<div class="absolute bottom-1 left-1 right-10 text-xs text-gray-400">
PAS: A Training-Free Stabilizer for Temporal Encoding in Video LLMs. Bowen Sun, Yujun Cai, Ming-Hsuan Yang, Hang Wu, Yiwei Wang. 2026
</div>

---

# FrameMind · Inter-frame Reasoning with RL

**Task**: Video frame interleaved reasoning. **Core idea**: adjacent frames are temporal samples of the same physical scene — reasoning across them must respect physical causality, enforced via RL rewards.

<img src="/Image/fig_14.png" class="w-full object-contain max-h-88 mt-3" />

<div class="absolute bottom-1 left-1 right-10 text-xs text-gray-400">
FrameMind: Frame-Interleaved Video Reasoning via Reinforcement Learning. Haonan Ge, Yiwei Wang, Kai-Wei Chang, Hang Wu, Yujun Cai. 2025
</div>

---

# FrameMind · Causal Consistency Check

RL rewards reasoning paths that are physically causal; inconsistent inter-frame transitions incur penalties and trigger model self-correction.

<img src="/Image/fig_15.png" class="w-full object-contain max-h-88 mt-3" />

<div class="absolute bottom-1 left-1 right-10 text-xs text-gray-400">
FrameMind: Frame-Interleaved Video Reasoning via Reinforcement Learning. Haonan Ge, Yiwei Wang, Kai-Wei Chang, Hang Wu, Yujun Cai. 2025
</div>

---

# Deeper Meaning of Temporal Reasoning

<div class="mt-6 text-center text-xl">
Reasoning on the time axis = Modeling the **physical causal chain**
</div>

<div class="mt-8 p-4 bg-gray-100 rounded text-gray-700">

**Intuitive example**: a glass shattering

Temporal reasoning can tell us:
- Magnitude of the impact force (inferred from sound intensity and fracture pattern)
- Material properties (inferred from the fracture mode)
- Motion trajectory (inferred from the frame sequence)

</div>

<div class="mt-4 text-center text-gray-500">
Causal order is one of the most fundamental constraints of the physical world.
</div>

---

# Temporal Reasoning — Summary

<div class="grid grid-cols-2 gap-8 mt-6">

<div>

### Position in the Framework

| Work | Problem Solved |
|------|---------------|
| PAS | Calibration of temporal positional encoding bias |
| FrameMind | Inter-frame causal reasoning and decision-making |

</div>

<div>

### Connecting to Core Themes

**Signal is Physics**: Temporal reasoning recovers the physical causal chain from video signals.

**Multi-source**: Audio-video timestamp alignment is the validator for temporal reasoning.

</div>

</div>

<div class="mt-8 p-4 bg-green-50 border-l-4 border-green-400 text-gray-700">

Space and time are both addressed.

→ Now let multiple signal sources **verify each other**.

</div>

---

# Part 5 · Implementing Multi-source Consistency

---

# From Single-source Reasoning to Multi-source Validation

<div class="grid grid-cols-2 gap-8 mt-8">

<div>

### Recap

Spatial and temporal reasoning are both structured reasoning **within a single channel**.

- ViewFusion: spatial reasoning within the visual channel
- PAS / FrameMind: causal reasoning along the time dimension

</div>

<div>

### New Question

How do different signal sources validate each other?

**Physical basis**: the same physical event leaves **redundant but consistent** traces across multiple signal sources.

This redundancy is a natural verification resource.

</div>

</div>

<div class="mt-8 p-4 bg-blue-50 border-l-4 border-blue-400 text-gray-700">
The same sound is recorded by multiple microphones; the same scene is captured by multiple cameras. They all describe the same physical truth.
</div>

---

# Audio as an Independent Reasoning Channel

### Unique Physical Properties of Audio

<img src="/Image/fig_16.png" class="w-full object-contain max-h-64 mt-3" />

<div class="mt-4 p-4 bg-yellow-50 border-l-4 border-yellow-400 text-gray-700">

Audio = spatiotemporal encoding of pressure waves, carrying complete spatial geometry. Audio is a severely underestimated reasoning channel.

</div>

---

# Thinking with Sound · Audio Reasoning Chain

Audio chain-of-thought for multimodal reasoning. Each reasoning step maps to an acoustic physical operation.

<img src="/Image/fig_17.png" class="w-full object-contain max-h-72 mt-3" />

<div class="mt-4 p-3 bg-blue-50 border-l-4 border-blue-400 text-gray-700">
Conclusion: Audio is not just a feature — it can carry complete reasoning logic.
</div>

<div class="absolute bottom-1 left-1 right-10 text-xs text-gray-400">
Thinking with sound: Audio chain-of-thought enables multimodal reasoning in large audio-language models. Zhen Xiong, Yujun Cai, Zhecheng Li, Junsong Yuan, Yiwei Wang. 2025
</div>

---

# AudioRouter · Audio-only Chain-of-Thought Reasoning

RL trains the model to route each reasoning step through the appropriate acoustic operation, producing interpretable and physically grounded audio reasoning chains.

<img src="/Image/fig_18.png" class="w-full object-contain max-h-80 mt-3" />

<div class="absolute bottom-1 left-1 right-10 text-xs text-gray-400">
AudioRouter: Data Efficient Audio Understanding via RL based Dual Reasoning. Liyang Chen, Hongkai Chen, Yujun Cai, Sifan Li, Qingwen Ye, Yiwei Wang. 2026
</div>

---

# AudioRouter · Results

RL-guided routing consistently outperforms chain-of-thought baselines across audio reasoning benchmarks, with gains especially pronounced on spatial and temporal acoustic tasks.

<img src="/Image/fig_19.png" class="w-full object-contain max-h-80 mt-3" />

<div class="absolute bottom-1 left-1 right-10 text-xs text-gray-400">
AudioRouter: Data Efficient Audio Understanding via RL based Dual Reasoning. Liyang Chen, Hongkai Chen, Yujun Cai, Sifan Li, Qingwen Ye, Yiwei Wang. 2026
</div>

---

# Multi-source Consistency — Unified View

All signal channels converge at a **Consistency Check**: agreement confirms physical truth; inconsistency triggers re-reasoning. Underwater acoustics simultaneously validates cross-modal and cross-sensor inputs, making it the hardest and most complete test of this framework.

<img src="/Image/fig_20.png" class="w-full object-contain max-h-80 mt-4" />

---

# Multi-source Reasoning — Summary

<div class="mt-6 p-4 bg-blue-50 border-l-4 border-blue-400 text-gray-700">

**Signal is Physics**: Multi-source consistency reasoning verifies whether multiple independent observations describe the same physical truth.

</div>

<div class="mt-6 p-6 border-2 border-blue-400 rounded text-center">

### Core Claim Formally Established

**Multi-source Consistency is the Validator of Physical Truth**

</div>

<div class="mt-6 text-center text-gray-500 text-xl">
Where can this framework be applied?
</div>

---

# Part 6 · Looking Up: From Reasoning to Action

---

# Reasoning-Driven Decision Making

Physical signal input → structured reasoning → planning → RL optimization → execution. The reasoning chain is not a byproduct — it directly generates the action sequence.

<img src="/Image/fig_21.png" class="w-full object-contain max-h-72 mt-3" />

<div class="mt-4 p-3 bg-green-50 border-l-4 border-green-400 text-gray-700">
Conclusion: The endpoint of physical reasoning is reliable action.
</div>

---

# GUI and Embodied Scenarios

<div class="grid grid-cols-2 gap-8 mt-6">

<div>

### Dimo-gui

Visual reasoning drives GUI interaction

Understanding the visual-physical structure of a UI → reliably executing action sequences.

### CamReasoner in Embodied Navigation

Camera motion understanding → spatial reasoning about the robot's own motion

Understanding "where am I" and "where am I going".

</div>

<div>

### Multi-source Connection

An embodied agent must integrate:

- Vision (camera)
- Touch (force sensor)
- Motion (IMU, encoder)
- Audio (ambient sound)

Multi-sensor signals must be physically consistent to support reliable decision-making.

</div>

</div>

<div class="mt-6 p-3 bg-blue-50 border-l-4 border-blue-400 text-gray-700">
Conclusion: Physical reasoning is the cognitive foundation of embodied intelligence.
</div>

---

# The Complete Chain: From Signal to Action

<img src="/Image/fig_22.png" class="w-full object-contain max-h-80 mt-3" />


<div class="mt-6 text-center text-gray-500">
This is the complete research framework we have built. Every step practices **Signal is Physics**.
</div>

---

# Part 7 · Underwater Acoustics AI: The Ultimate Test

---

# Why Underwater Acoustics Is the Ultimate Test

<div class="grid grid-cols-2 gap-8 mt-4">

<div>

### Extreme Physical Constraints

- **Multipath reflections**: complex propagation paths in water
- **Temperature gradients**: sound speed changes continuously with depth
- **Limited visual aid**: poor visibility.
- **Extremely high noise**: low SNR, strong background interference

</div>

<div>

### Connecting to Core Themes

**Signal is Physics**: Underwater acoustics is the most extreme embodiment of "signal is physics" — only acoustic signals and physical laws, no other assistance.

**Multi-source**: Every transducer in a sonar array is an independent observation; their consistency is the sole basis for target localization.

</div>

</div>

<div class="mt-4 p-3 bg-red-50 border-l-4 border-red-400 text-gray-700">
Underwater acoustics pushes every assumption of our framework to the limit.
</div>

---

# Applications of Underwater Acoustics AI

<div class="grid grid-cols-3 gap-4 mt-8">

<div class="p-4 border rounded text-center">

### Ocean Exploration

Deep-sea species detection, marine environment monitoring, acoustic tomography.

</div>

<div class="p-4 border rounded text-center">

### Underwater Autonomous Systems

AUV navigation, underwater communication, cooperative operations.

</div>

<div class="p-4 border rounded text-center">

### Seabed Resource Survey

Mineral localization, pipeline inspection, geological structure analysis.

</div>

</div>

<div class="mt-6 p-4 bg-yellow-50 border-l-4 border-yellow-400 text-gray-700">

**Status**: lowest AI penetration, most complex physical modeling, highest application value.

**Opportunity**: precisely because AI has not yet entered this domain, first-mover advantage is enormous.

</div>

---

# Methodology Transfer

| Existing Capability | Underwater Acoustics Mapping |
|--------------------|------------------------------|
| Multi-view spatial reasoning (ViewFusion) | Array localization: inter-transducer time delays → source direction |
| Temporal stability calibration (PAS) | Multipath suppression: separating direct arrivals from reflections |
| Audio reasoning chain (Thinking with Sound) | Underwater feature analysis: from raw IQ signals to target reconstruction |

<div class="mt-8 p-4 bg-green-50 border-l-4 border-green-400 text-gray-700">
Conclusion: We are not starting from scratch — we are entering a new domain with a validated toolbox.
</div>

---

# Part 8 · Conclusion

---

# Our Research Landscape

| Layer | Works |
|-------|-------|
| **Perception Layer** | Spatial Blind Spot · Not in Sync · Visual CoT |
| **Reasoning Layer** | ViewFusion · CamReasoner · PAS · · Thinking with Sound · AudioRouter |
| **Decision Layer** | Dimo-gui · FrameMind |

<div class="mt-8 p-4 bg-gray-100 rounded text-center text-gray-700">

Perception layer reveals the **problems**.

Reasoning layer provides the **methods**.

Decision layer validates the **value**.

</div>

---

# Core Claims

<v-clicks>

<div class="text-3xl font-bold mt-8 text-center">
Signal is Physics
</div>

<div class="text-2xl mt-6 text-center text-gray-700">
Structured Reasoning is the Language of Physical Constraints
</div>

<div class="text-xl mt-6 text-center text-gray-500">
Multi-source Consistency is the Validator of Physical Truth
</div>

</v-clicks>

---
layout: center
---

# Thank You!

Questions and discussion welcome.

<div class="mt-8 text-gray-400 text-sm">
wangyw.evan@gmail.com
</div>

<img src="/Image/uc_yellow.svg" class="absolute top-8 right-8 h-16" />
