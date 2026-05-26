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

① **Multi-microphone localization** asks whether we can infer where a sound comes from.

② **Camera-motion understanding** asks whether AI can tell pushing forward from rotating.

③ **Sonar-array reconstruction** asks whether multi-transducer signals can recover a target position.

→ These three questions are, fundamentally, the same question.

![Figure](/Image/fig_1.png)

---

# Signal is Physics

**Audio** is a spatiotemporal encoding of pressure waves; **image** is a 2D projection of a light field; **video** is continuous sampling of physical dynamics. The structure of a signal is the structure of physical law.

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

Current models are strong at **image recognition and generation**, improving quickly in **video QA and cross-modal retrieval**, and advancing rapidly in **speech understanding and audio generation**.

### But There Are Systematic Failures in Physical Constraint Reasoning

Yet they still fail on **sound-source motion**, show **audio-video temporal misalignment**, and can drift further from physical truth as reasoning chains become longer.

Scale and data alone cannot fix a missing understanding of physics.

---

# What Are Physical Constraints?

**Spatial constraints** include perspective, occlusion, and parallax: 3D layout leaves deterministic traces in 2D images.

**Temporal constraints** include motion continuity and causal order: physical events cannot be reversed on the time axis.

**Multi-source constraints** require independent observations of the same event to stay mutually consistent, across **modalities** such as visual + audio and across **sensors** such as microphones, cameras, or transducers.

![Figure](/Image/fig_30.png)

---

# Evidence 1 · Spatial Blind Spot

### Key Finding

Audio LLMs Cannot Perceive Sound Source Direction. When a sound source moves **left to right**, the model can barely determine the direction, and accuracy approaches **random chance**.

**Conclusion**: The model is listening, but not reasoning about space.

![Figure](/Image/fig_4.png)

<footer>Spatial Blind Spot: Auditory Motion Perception Deficits in Audio LLMs. Zhe Sun, Yujun Cai, Jiayu Yao, Yiwei Wang. 2025</footer>

---

# Evidence 2 · Not in Sync

## Systematic Temporal Bias in Audio Chat Models

### Key Finding

Models show a **systematic temporal bias** when localizing audio events, and this bias does not improve with **model scale**.

### Physical Interpretation
Audio and video describe **the same physical event** — temporal inconsistency means the model has lost the physical causal chain.

Conclusion: The model sees the frames, but loses the physical meaning of temporal order.

![Figure](/Image/fig_6.png)

<footer>Not in Sync: Unveiling Temporal Bias in Audio Chat Models · J Yao, S Liu, Y Wang, R Cheng, L Mei, B Bi, Z Xiong, X Cheng</footer>

---

# Evidence 3 · Fragile Visual Reasoning

### Key Finding

Visual CoT Makes VLMs Smarter but More Fragile: Visual chain-of-thought introduces **new systematic errors**, and for some cases **more reasoning steps** make the errors worse.

### Physical Interpretation

The reasoning chain is not anchored to physical constraints, so the longer it runs, the more it drifts.

**Conclusion**: More reasoning steps ≠ better physical understanding.

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

**Analogy**: Multiple independent witnesses in court — consistent testimony is credible; contradiction reveals the flaw.

![Figure](/Image/fig_31.png)

---

# Part 3 · Spatial Reasoning

![Figure](/Image/fig_25.png)

---

# The Challenge of Spatial Reasoning

### Why Is Spatial Reasoning Hard?

**Single-frame ambiguity** loses depth in projection, so one image cannot determine 3D position.

**Viewpoint dependence** makes the same scene produce different spatial descriptions from different cameras.

**Occlusion** hides object parts, so their spatial relations can only be inferred through constraints.

**Our approach**: use structured reasoning chains to make spatial relations explicit.

→ This is Signal is Physics instantiated on the visual channel.

---

# ViewFusion · Multi-view Spatial Reasoning Chain

**Task**: spatial relation QA under multi-view settings. **Core innovation**: a Structured Spatial Thinking Chain whose steps map to verifiable geometric operations. **Result**: stronger performance on multi-view spatial reasoning benchmarks.

![Figure](/Image/fig_9.png)

<footer>ViewFusion: Structured Spatial Thinking Chains for Multi-View Reasoning. Xingjian Tao, Yiwei Wang, Yujun Cai, Yifan Song, Jing Tang. 2026</footer>

---

# ViewFusion · Physical Significance

Each **reasoning step** corresponds to a physical operation, and conclusions from different viewpoints must remain **geometrically consistent**. The reasoning structure is the linguistic expression of spatial physical constraints.

| Reasoning Step | Physical Operation |
|------------|------------------------------|
| Coordinate alignment | Extrinsic matrix transform |
| Triangulation | Multi-view geometry |
| Relation inference | 3D spatial computation |

<footer>ViewFusion: Structured Spatial Thinking Chains for Multi-View Reasoning. Xingjian Tao, Yiwei Wang, Yujun Cai, Yifan Song, Jing Tang. 2026</footer>

---

# CamReasoner · Camera Motion Understanding

![Figure](/Image/fig_11.png)

<footer>CamReasoner: Reinforcing Camera Movement Understanding via Structured Spatial Reasoning. Hang Wu, Yujun Cai, Zehao Li, Haonan Ge, Bowen Sun, Junsong Yuan, Yiwei Wang. 2026</footer>

---

# CamReasoner · Physical Significance

**Camera motion** directly carries physical constraints: every motion corresponds to a deterministic 3D geometric transformation, and the frame sequence must stay consistent with it.

**RL** learns which reasoning path follows physical motion laws, not merely which final answer is correct.

Reasoning paths that violate constraints are penalized, forcing the model to internalize **visual physics**.

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

**Frame sampling** discretizes continuous time, so events between frames disappear and non-uniform sampling further blurs temporal relations.

**Positional encoding bias** creates systematic offsets in perceived event timing.

**Our approach**: calibrate temporal perception without retraining.

→ Temporal continuity is the most fundamental physical constraint on video signals.

---

# PAS · Phase Aggregated Smoothing

**Task**: temporal encoding bias in Video LLMs. **Core innovation**: a training-free stabilizer that injects temporal physical constraints at inference time. **Result**: lower temporal perception bias and higher temporal QA accuracy.

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

Temporal reasoning can infer **impact force** from sound intensity and fracture patterns, **material properties** from fracture mode, and **motion trajectory** from the frame sequence.

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

**ViewFusion** handles spatial reasoning inside the visual channel, while **PAS** and **FrameMind** handle causal reasoning along the time dimension.

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

**Dimo-gui** uses visual reasoning to understand the visual-physical structure of a UI and execute action sequences reliably.

**CamReasoner** turns camera motion understanding into spatial reasoning about the robot's own motion: "where am I" and "where am I going".

### Multi-source Connection

An embodied agent must integrate **vision** from cameras, **touch** from force sensors, **motion** from IMU and encoders, and **audio** from ambient sound.

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

Underwater acoustics combines **multipath reflections**, **temperature-dependent sound speed**, **limited visual aid**, and **extremely high noise** into one tightly constrained physical setting.

### Connecting to Core Themes

**Signal is Physics**: Underwater acoustics is the most extreme embodiment of "signal is physics" — only acoustic signals and physical laws, no other assistance.

**Multi-source**: Every transducer in a sonar array is an independent observation; their consistency is the sole basis for target localization.

Underwater acoustics pushes every assumption of our framework to the limit.

---

# Applications of Underwater Acoustics AI

**Ocean exploration** covers deep-sea species detection, marine monitoring, and acoustic tomography.

**Underwater autonomy** covers AUV navigation, communication, and cooperative operations.

**Seabed surveys** cover mineral localization, pipeline inspection, and geological structure analysis.

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

**Signal is Physics**

**Structured Reasoning** is the Language of Physical Constraints

**Multi-source Consistency** is the Validator of Physical Truth

---

# Thank You!

<span class="closing-slide-marker"></span>

Questions and discussion welcome.

[wangyw.evan@gmail.com](mailto:wangyw.evan@gmail.com)

![UC Merced](/Image/uc_yellow.svg)