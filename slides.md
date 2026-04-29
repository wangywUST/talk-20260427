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
April 2026
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
layout: two-cols
---

# Do Models Really Understand This?

### How Current Models Work

Statistical pattern matching

- Similar input seen before → similar output
- No physical prior
- Systematic failure on out-of-distribution cases

::right::

<div class="mt-14"></div>

### Our Claim

Signals are encodings of physical processes and should be reasoned about as such.

- Each reasoning step maps to a physical operation
- Multi-source signals must be mutually consistent
- Reasoning is interpretable and verifiable

<div class="mt-8 p-4 bg-gray-100 rounded text-center text-gray-700">
Analogy: Memorizing answers vs. understanding the formula
</div>

<div class="mt-4 text-center text-gray-500">
→ This is the problem structured reasoning is built to solve.
</div>

---

# Part 1 · Perception ≠ Understanding

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

<div class="grid grid-cols-3 gap-6 mt-8">

<div class="p-4 border rounded">

### Spatial Constraints

Perspective, occlusion, parallax

The 3D spatial layout of objects leaves deterministic traces in 2D images.

</div>

<div class="p-4 border rounded">

### Temporal Constraints

Motion continuity, causal order

Physical events on the time axis must obey causality — they cannot be reversed.

</div>

<div class="p-4 border rounded">

### Multi-source Constraints

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

<div class="p-4 bg-gray-100 rounded text-gray-700">

```
Sound source →→→→→→→→
              ↓
    🎤 Microphone Array 🎤
     [Time delay = Direction]
              ↓
      Model output: ❓
```

The time delay is discarded; spatial information vanishes.

</div>

</div>

<div class="mt-4 p-3 bg-yellow-50 border-l-4 border-yellow-400 text-gray-700">
Conclusion: The model is listening, but not reasoning about space.
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

<div class="p-4 bg-gray-100 rounded text-gray-700">

```
Ground-truth timeline:  ─────●─────
                              ↑
                         Event occurs

Model perception:        ─────────●─
                                  ↑
                             Event detected
                             [Systematic delay]
```

</div>

</div>

<div class="mt-4 p-3 bg-yellow-50 border-l-4 border-yellow-400 text-gray-700">
Conclusion: The model sees the frames, but loses the physical meaning of temporal order.
</div>

---

# Evidence 3 · Fragile Visual Reasoning

## Visual CoT Makes VLMs Smarter but More Fragile

<div class="grid grid-cols-2 gap-8 mt-6">

<div>

### Key Finding

- Adding visual chain-of-thought improves overall accuracy
- But it simultaneously introduces new, systematic error patterns
- More reasoning steps → certain errors become worse

### Physical Interpretation

The reasoning chain is not anchored to physical constraints, so the longer it runs, the more it drifts.

</div>

<div class="p-4 bg-gray-100 rounded text-gray-700">

```
Step 1: Observe scene       ✓
Step 2: Infer relation      ✓
Step 3: Conclude            ✗  ← Error accumulates

vs. Physics-anchored:
Step 1: Observe scene       ✓
Step 2: Verify consistency  ✓
Step 3: Conclude            ✓
```

</div>

</div>

<div class="mt-4 p-3 bg-yellow-50 border-l-4 border-yellow-400 text-gray-700">
Conclusion: More reasoning steps ≠ better physical understanding.
</div>

---

# Problem Framework

<div class="grid grid-cols-3 gap-4 mt-8">

<div class="p-4 border-2 border-blue-400 rounded text-center">

### Top Layer
Structured Reasoning

</div>

<div class="p-4 border-2 border-green-400 rounded text-center">

### Middle Layer
Multi-source Signals

Audio · Visual · Temporal · Sensor Array

</div>

<div class="p-4 border-2 border-gray-400 rounded text-center">

### Bottom Layer
Physical World

</div>

</div>

<div class="mt-8 p-4 bg-red-50 border-l-4 border-red-400 text-gray-700">

**The problem with current models**: the transition from middle layer to top layer lacks injection of physical priors.

This is where our work begins.

</div>

---

# Part 2 · Structured Reasoning & Multi-source Consistency

---

# Three Forms of Structured Reasoning

| Form | Mechanism | Representative Work |
|------|-----------|-------------------|
| Reasoning Chain | Each step maps to a physical operation | ViewFusion, Thinking with Sound |
| Path Selection | RL learns physically consistent reasoning order | CamReasoner, AudioRouter |
| Structure Injection | Hard-coded physical constraints injected into reasoning | PAS |

<div class="mt-8 p-4 bg-gray-100 rounded text-gray-700">

**What all three share**

The reasoning process is **transparent and interpretable** with respect to physical constraints.

Every step can answer: what physical operation is this step performing?

</div>

---

# What Is Multi-source Consistency?

<div class="mt-4 p-4 bg-blue-50 border-l-4 border-blue-400 text-gray-700">
Core principle: The physical world is singular. Any set of independent observations of it must yield mutually consistent conclusions.
</div>

<div class="mt-6 font-mono text-sm p-4 bg-gray-100 rounded text-gray-700">

```
Visual reasoning chain    ──┐
Audio reasoning chain     ──┤
Microphone array          ──┼──→  Consistency Check  ──→  Physical Truth Confirmed
Multi-view cameras        ──┤              ↑
Underwater transducers    ──┘     Inconsistent → Re-reason
```

</div>

<div class="mt-6 text-center text-gray-500">
Analogy: Multiple independent witnesses in court — consistent testimony is credible; contradiction reveals the flaw.

**Where inconsistency appears is where reasoning went wrong.**
</div>

---

# Part 3 · Spatial Reasoning

---

# The Challenge of Spatial Reasoning

### Why Is Spatial Reasoning Hard?

<div class="grid grid-cols-3 gap-4 mt-6">

<div class="p-4 border rounded text-center">
**Insufficient Single-frame Information**

Depth is lost in projection; a single image cannot determine 3D position.
</div>

<div class="p-4 border rounded text-center">
**Viewpoint Dependence**

The same scene leads to completely different spatial descriptions from different viewpoints.
</div>

<div class="p-4 border rounded text-center">
**Occlusion**

Spatial relations of hidden parts can only be inferred from constraints.
</div>

</div>

<div class="mt-8 p-4 bg-blue-50 border-l-4 border-blue-400 text-gray-700">

**Our approach**: use structured reasoning chains to make spatial relations explicit.

→ This is Signal is Physics instantiated on the visual channel.

</div>

---

# ViewFusion · Multi-view Spatial Reasoning Chain

<div class="grid grid-cols-2 gap-8 mt-4">

<div>

### Task

Spatial relation QA under multi-view settings

### Core Innovation

Structured Spatial Thinking Chain

Each reasoning step maps to a spatial geometric operation and is verifiable.

### Results

Significantly outperforms baselines on multi-view spatial reasoning benchmarks.

</div>

<div class="p-4 bg-gray-100 rounded text-sm text-gray-700">

```
Input: Images from cameras A, B, C
              ↓
Step 1: Establish coordinate frames
              ↓
Step 2: Locate target in each view
              ↓
Step 3: Triangulate to 3D position
              ↓
Step 4: Infer spatial relation
              ↓
Output: Spatial relation answer ✓
```

</div>

</div>

<div class="mt-4 text-gray-500 text-sm">
Multi-source view: multiple cameras = multiple sensors independently sampling the same space.
</div>

---

# ViewFusion · Physical Significance

<div class="grid grid-cols-2 gap-8 mt-8">

<div>

### Reasoning Step → Physical Operation

| Reasoning Step | Physical Operation |
|---------------|-------------------|
| Coordinate alignment | Extrinsic matrix transform |
| Depth estimation | Monocular depth constraint |
| Triangulation | Multi-view geometry |
| Relation inference | 3D spatial computation |

</div>

<div>

### Multi-source Consistency

Conclusions from different viewpoints must be geometrically consistent.

```
View A infers: "target is front-left"
View B infers: "target is back-right"
          ↓
Geometric constraint check: Contradiction!
          ↓
Reasoning chain self-corrects
```

</div>

</div>

<div class="mt-6 p-3 bg-blue-50 border-l-4 border-blue-400 text-gray-700">
Conclusion: The reasoning structure is the linguistic expression of spatial physical constraints.
</div>

---

# CamReasoner · Camera Motion Understanding

<div class="grid grid-cols-2 gap-8 mt-6">

<div>

### Task

Semantic classification of camera motion in video

### Core Innovation

RL-driven structured spatial reasoning

The model learns to select reasoning paths consistent with physical motion laws.

</div>

<div class="p-4 bg-gray-100 rounded text-gray-700">

### Geometric Meaning of Motion Types

| Motion Type | Physical / Geometric Meaning |
|------------|------------------------------|
| Push (Dolly in) | Camera translates forward, focal length fixed |
| Pull (Dolly out) | Camera translates backward, focal length fixed |
| Pan / Tilt | Optical center fixed, optical axis rotates |
| Zoom | Optical center fixed, focal length changes |

</div>

</div>

---

# CamReasoner · Physical Significance

<div class="mt-8">

### Camera Motion Is the Most Direct Visual Carrier of Physical Constraints

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

# PAS · Positional Alignment Stabilizer

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

<div class="p-4 bg-gray-100 rounded text-sm text-gray-700">

```
Without PAS:
Frames:     F1 F2 F3 F4 F5
Perceived:  F1    F3 F4 F5
                ↑
           Temporal gap; bias accumulates

With PAS:
Frames:     F1 F2 F3 F4 F5
Perceived:  F1 F2 F3 F4 F5
Physical constraint injected → stable
```

</div>

</div>

<div class="mt-4 p-3 bg-blue-50 border-l-4 border-blue-400 text-gray-700">
Conclusion: Temporal continuity is the foundational guarantee of physical fidelity.
</div>

---

# FrameMind · Inter-frame Reasoning with RL

<div class="grid grid-cols-2 gap-8 mt-6">

<div>

### Task

Video frame interleaved reasoning

### Core Innovation

RL-driven inter-frame logical reasoning

### Reasoning Path Example

```
Frame t:   Observe state A
Frame t+1: Infer transition A→B
Frame t+2: Verify physical causality ✓
           Predict state C
```

RL rewards reasoning paths that are physically causal.

</div>

<div>

### Multi-source View

Adjacent frames = **temporal samples** of the same physical scene.

Inter-frame reasoning must satisfy causal consistency.

```
Frame n:   Ball in the air
Frame n+1: Ball hits the ground
Frame n+2: Ball bounces up
     ↓
Physical check: trajectory satisfies
                gravity equations ✓
```

If inconsistent → RL penalty → model corrects.

</div>

</div>

---

# The Deeper Meaning of Temporal Reasoning

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

<div class="mt-6 p-4 bg-yellow-50 border-l-4 border-yellow-400 text-gray-700">

**Multi-source connection**

Audio timestamps + video frame timestamps must be aligned.

Misalignment → the root cause of the **Not in Sync** problem.

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

<div class="grid grid-cols-3 gap-4 mt-6">

<div class="p-4 border rounded text-center">
**Extremely High Temporal Resolution**

Sampling rate 44,100 Hz — far exceeding video frame rate — captures very brief physical events.
</div>

<div class="p-4 border rounded text-center">
**Strong Spatial Constraints**

Time delay → direction

Intensity attenuation → distance

Complete spatial geometry is encoded in acoustic signals.
</div>

<div class="p-4 border rounded text-center">
**Unaffected by Lighting or Occlusion**

In darkness, behind obstacles — audio still carries complete physical information.
</div>

</div>

<div class="mt-6 p-4 bg-yellow-50 border-l-4 border-yellow-400 text-gray-700">

Recall: Audio = spatiotemporal encoding of pressure waves, carrying complete spatial geometry.

**Audio is a severely underestimated reasoning channel.**

</div>

---

# Thinking with Sound · Audio Reasoning Chain

<div class="grid grid-cols-2 gap-8 mt-6">

<div>

### Task

Audio chain-of-thought for multimodal reasoning

### Core Innovation

Explicit audio reasoning steps

Each step maps to an acoustic physical operation.

### Significance

Only a complete audio reasoning chain can truly serve as a cross-modal validator.

</div>

<div class="p-4 bg-gray-100 rounded text-sm text-gray-700">

**Reasoning chain example**

```
Input: Binaural audio clip
   ↓
Step 1: Compute inter-microphone time delay
        Δt = t_R - t_L = 0.3 ms
   ↓
Step 2: Infer source direction from Δt
        θ = arcsin(c·Δt / d) = 30°
   ↓
Step 3: Infer distance from intensity decay
        r ≈ 2.4 m
   ↓
Output: Source is front-right at 30°, ~2.4 m away
```

</div>

</div>

<div class="mt-4 p-3 bg-blue-50 border-l-4 border-blue-400 text-gray-700">
Conclusion: Audio is not just a feature — it can carry complete reasoning logic.
</div>

---

# AudioRouter · Multi-source Consistency in Action

<div class="grid grid-cols-2 gap-8 mt-4">

<div>

### Task

Using audio logic to assist video action understanding

### Core Innovation

RL-based dual reasoning pathway

### Consistency Mechanism

```
Video channel  → infers "Action A"
Audio channel  → infers "Sound matches Action B"
         ↓
   A ≠ B: Inconsistency detected!
         ↓
   RL learns to re-weigh,
   rather than blindly trust vision
         ↓
   Corrected output
```

</div>

<div>

### Case: Audio Corrects a Visual Error

**Scene**: video shows "chopping vegetables"

| Channel | Inference |
|---------|-----------|
| Visual | Chopping vegetables ✓ |
| Audio | Sound is a thud, not a slicing sound |

→ Audio inconsistency triggers re-reasoning

→ Corrected: mincing meat, not slicing vegetables

<div class="mt-4 p-3 bg-green-50 border rounded text-gray-700">
Audio's physical logic acts as a validator for visual reasoning.
</div>

</div>

</div>

---

# Multi-source Consistency — Unified View

<div class="font-mono text-sm p-6 bg-gray-100 rounded mt-4 text-gray-700">

```
Visual reasoning chain    ──┐
Audio reasoning chain     ──┤
Microphone array          ──┼──→  Consistency Check  ──→  Physical Truth Confirmed
Multi-view cameras        ──┤              ↑
Underwater transducers    ──┘     Inconsistent → Re-reason
```

</div>

<div class="mt-8 grid grid-cols-3 gap-4 text-sm text-center">

<div class="p-3 border rounded">
ViewFusion represents **cross-sensor** (multi-camera)
</div>

<div class="p-3 border rounded">
AudioRouter represents **cross-modal** (visual + audio)
</div>

<div class="p-3 border rounded">
Underwater acoustics is the **extreme fusion** of both
</div>

</div>

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

### The Leap from Understanding to Acting

<div class="grid grid-cols-2 gap-8 mt-6">

<div>

### FrameMind

Video reasoning → reinforcement learning → decision

Reasoning chain directly translates into action instructions.

### Video-to-BT

Human demonstration → robot behavior tree generation

Physical reasoning understands human intent and generates executable behavior trees.

</div>

<div class="p-4 bg-gray-100 rounded text-sm text-gray-700">

```
Physical signal input
       ↓
Structured reasoning
(understand physical scene)
       ↓
Reasoning chain → action sequence
       ↓
RL optimization → decision output
       ↓
Robot / agent execution
```

</div>

</div>

<div class="mt-6 p-3 bg-green-50 border-l-4 border-green-400 text-gray-700">
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

<div class="mt-8 p-6 bg-gray-100 rounded text-gray-700">

```
Multi-source physical signal input
              ↓
        Spatial Reasoning
    (ViewFusion, CamReasoner)
              ↓
       Temporal Reasoning
         (PAS, FrameMind)
              ↓
  Multi-source Consistency Check
  (AudioRouter, Thinking with Sound)
              ↓
        Decision Output
   (Video-to-BT, Dimo-gui, FrameMind)
```

</div>

<div class="mt-6 text-center text-gray-500">
This is the complete research framework we have built.

Every step practices **Signal is Physics**.
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
- **No visual aid**: purely unimodal — only acoustic signals
- **Extremely high noise**: low SNR, strong background interference

### In One Sentence

If our framework works here, it has truly understood physics.

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

### Existing Capability → Underwater Acoustics Mapping

| Existing Capability | Underwater Acoustics Mapping |
|--------------------|------------------------------|
| Multi-view spatial reasoning (ViewFusion) | Array localization: inter-transducer time delays → source direction |
| Temporal stability calibration (PAS) | Multipath suppression: separating direct arrivals from reflections |
| Cross-modal consistency check (AudioRouter) | Acoustic-image fusion: joint reasoning from acoustic signals and imagery |
| Audio reasoning chain (Thinking with Sound) | Underwater feature analysis: from raw IQ signals to target reconstruction |

<div class="mt-8 p-4 bg-green-50 border-l-4 border-green-400 text-gray-700">
Conclusion: We are not starting from scratch — we are entering a new domain with a validated toolbox.
</div>

---

# Long-term Roadmap and Recruitment

### Three-Phase Plan

<div class="grid grid-cols-3 gap-4 mt-6">

<div class="p-4 border-2 border-green-400 rounded">

### Phase 1 ✅

Consolidate methodology from existing AI work.

Establish the Signal is Physics framework.

</div>

<div class="p-4 border-2 border-blue-400 rounded">

### Phase 2

Image-domain sonar.

UATD / FSOD datasets.

Object detection and recognition.

</div>

<div class="p-4 border-2 border-gray-400 rounded">

### Phase 3

Physical-domain raw IQ signal → image reconstruction.

Validation on real sonar hardware.

</div>

</div>

<div class="mt-6 p-4 bg-blue-50 border-l-4 border-blue-400 text-gray-700">

**Recruitment**

If you are interested in physics-driven AI, underwater acoustic signal processing, or multimodal reasoning — please find me after the talk.

</div>

---

# Part 8 · Conclusion

---

# Our Research Landscape

| Layer | Works |
|-------|-------|
| **Perception Layer** | Spatial Blind Spot · Not in Sync · Visual CoT |
| **Reasoning Layer** | ViewFusion · CamReasoner · PAS · FrameMind · Thinking with Sound · AudioRouter |
| **Decision Layer** | Video-to-BT · Dimo-gui · FrameMind |

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
your@email.com
</div>

<img src="/Image/uc_yellow.svg" class="absolute top-8 right-8 h-16" />
