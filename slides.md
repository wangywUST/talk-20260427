---
theme: dracula
title: Signal is Physics
info: |
  组会汇报 · 2026
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

**作者姓名** · University of California, Merced

<div class="pt-4 text-gray-400">
2026年X月X日 · 组会
</div>

<img src="/Image/uc_yellow.svg" class="absolute top-8 right-8 h-16" />

---
layout: center
---

<v-clicks>

<div class="text-3xl font-bold mb-8">多个麦克风，能判断声源在哪个方向吗？</div>

<div class="text-3xl font-bold mb-8">一段视频，AI 能感知摄像机在向前推进还是在旋转吗？</div>

<div class="text-3xl font-bold mb-8">水下声纳阵列，AI 能从多个换能器的信号里重建目标位置吗？</div>

</v-clicks>

<div v-click class="pt-6 text-center text-xl text-gray-500">
这三个问题，本质上是同一个问题
</div>

---
layout: center
---

# Signal is Physics

<v-clicks>

<div class="text-2xl mt-8">音频 　＝　压力波的时空编码</div>

<div class="text-2xl mt-6">图像 　＝　光场的二维投影</div>

<div class="text-2xl mt-6">视频 　＝　时空动力学的连续采样</div>

</v-clicks>

<div v-click class="pt-8 text-center text-lg text-gray-500">
信号的结构，就是物理规律的结构
</div>

---
layout: two-cols
---

# 但模型真的这样理解吗？

### 当前模型的处理方式

统计模式匹配

- 见过类似输入 → 输出类似结果
- 不依赖物理先验
- 在分布外场景系统性失败

::right::

<div class="mt-14"></div>

### 我们的主张

信号 = 物理过程的编码，应被如此推理

- 每一步推理对应一个物理操作
- 多源信号必须相互自洽
- 推理过程可解释、可验证

<div class="mt-8 p-4 bg-gray-100 rounded text-center text-gray-700">
类比：背答案的学生 vs 理解公式的学生
</div>

<div class="mt-4 text-center text-gray-500">
→ 这就是结构化推理要解决的问题
</div>

---

# Part 1 · 感知不等于理解

---

# 当前多模态 AI 的能力边界

### 已有的成就

- 图像识别、图文生成：接近甚至超越人类
- 视频问答、跨模态检索：显著进展
- 语音理解与音频生成：快速突破

<div class="mt-6 p-4 border-l-4 border-red-400 bg-red-50 text-gray-700">

### 但在物理约束推理上，存在系统性缺陷

- 无法感知声源的空间运动方向
- 音视频时间戳系统性不对齐
- 推理链越长反而越容易偏离物理事实

</div>

<div class="mt-4 text-gray-500 text-center">
规模和数据量不能解决物理理解的缺失
</div>

---

# 什么是物理约束？

<div class="grid grid-cols-3 gap-6 mt-8">

<div class="p-4 border rounded">

### 空间约束

透视、遮挡、视差

物体在三维空间中的位置关系在二维图像上留下确定性痕迹

</div>

<div class="p-4 border rounded">

### 时间约束

运动连贯性、因果顺序

物理事件在时间轴上必须满足因果律，不能倒转

</div>

<div class="p-4 border rounded">

### 多源约束

同一物理事件在多个信号源上的观测结论必须自洽

</div>

</div>

<div class="mt-6 text-gray-500 text-sm">
多源约束涵盖：跨模态（视觉＋音频）和跨传感器（多麦克风 / 多摄像机 / 多换能器）
</div>

---

# 证据① · 听觉空间盲区

## Spatial Blind Spot

**Audio LLMs 无法感知声源运动方向**

<div class="grid grid-cols-2 gap-8 mt-6">

<div>

### 核心发现

- 当声源从左向右移动时，模型几乎无法判断方向
- 准确率接近随机猜测水平

### 物理解读

多麦克风的**时延差**里藏着完整的空间信息，但模型完全没有利用

</div>

<div class="p-4 bg-gray-100 rounded text-gray-700">

```
声源 →→→→→→→→
         ↓
  🎤 麦克风阵列 🎤
   [时延差 = 方向信息]
         ↓
   模型输出：❓
```

时延差被丢弃，空间信息消失

</div>

</div>

<div class="mt-4 p-3 bg-yellow-50 border-l-4 border-yellow-400 text-gray-700">
结论：模型在听，但没有在推理空间
</div>

---

# 证据② · 时间不同步

## Not in Sync

**Audio Chat Models 的系统性时间偏差**

<div class="grid grid-cols-2 gap-8 mt-6">

<div>

### 核心发现

- 模型对音频事件的时间定位存在显著系统性偏差
- 偏差不随模型规模改善

### 物理解读

音频和视频描述的是**同一物理事件**，时间上不自洽说明模型丢失了物理因果链

</div>

<div class="p-4 bg-gray-100 rounded text-gray-700">

```
真实时间轴:  ─────●─────
                  ↑
              物理事件发生

模型感知轴:  ─────────●─
                      ↑
                  感知到事件
                  [系统性延迟]
```

</div>

</div>

<div class="mt-4 p-3 bg-yellow-50 border-l-4 border-yellow-400 text-gray-700">
结论：模型看到了帧，但丢失了时序的物理意义
</div>

---

# 证据③ · 视觉推理的脆弱性

## Visual CoT Makes VLMs Smarter but More Fragile

<div class="grid grid-cols-2 gap-8 mt-6">

<div>

### 核心发现

- 加入视觉推理链后，整体准确率提升
- 但同时引入了新的、系统性的错误模式
- 推理步骤越多，某类错误越严重

### 物理解读

推理链没有锚定在物理约束上，所以越推越偏

</div>

<div class="p-4 bg-gray-100 rounded text-gray-700">

```
Step 1: 观察场景 ✓
Step 2: 推断关系 ✓
Step 3: 得出结论 ✗ ← 累积偏差

vs 物理约束锚定:
Step 1: 观察场景 ✓
Step 2: 校验物理一致性 ✓
Step 3: 得出结论 ✓
```

</div>

</div>

<div class="mt-4 p-3 bg-yellow-50 border-l-4 border-yellow-400 text-gray-700">
结论：更多推理步骤 ≠ 更好的物理理解
</div>

---
layout: center
---

# 问题框架定义

<div class="grid grid-cols-3 gap-4 mt-8">

<div class="p-4 border-2 border-blue-400 rounded text-center">

### 上层
结构化推理
Structured Reasoning

</div>

<div class="p-4 border-2 border-green-400 rounded text-center">

### 中层
多源信号
Audio · Visual · Temporal · Sensor Array

</div>

<div class="p-4 border-2 border-gray-400 rounded text-center">

### 底层
物理世界
Physical World

</div>

</div>

<div class="mt-8 p-4 bg-red-50 border-l-4 border-red-400 text-gray-700">

**当前模型的问题**：中层到上层之间，缺乏物理先验的注入

这就是我们工作的起点

</div>

---

# Part 2 · 结构化推理与多源一致性

---

# 结构化推理的三种形式

| 形式 | 机制 | 代表工作 |
|------|------|--------|
| 推理链 | 每步推理对应一个物理操作 | ViewFusion, Thinking with Sound |
| 路径选择 | RL 学习物理一致的推理顺序 | CamReasoner, AudioRouter |
| 结构注入 | 外部物理约束硬编码入推理 | PAS |

<div class="mt-8 p-4 bg-gray-100 rounded text-gray-700">

**三种形式的共同点**

推理过程对物理约束是**透明的、可解释的**

每一步都能回答：这一步在做什么物理操作？

</div>

---
layout: center
---

# Multi-source Consistency 是什么？

<div class="mt-4 p-4 bg-blue-50 border-l-4 border-blue-400 text-gray-700">
核心原则：物理世界是唯一的，任何对它的多次独立观测，结论必须自洽
</div>

<div class="mt-6 font-mono text-sm p-4 bg-gray-100 rounded text-gray-700">

```
视觉推理链     ──┐
音频推理链     ──┤
多麦克风阵列   ──┼──→  一致性校验  ──→  物理真实性确认
多视角摄像机   ──┤          ↑
水声换能器阵列 ──┘     不一致 → 重新推理
```

</div>

<div class="mt-6 text-center text-gray-500">
类比：法庭上的多位独立证人，证词高度吻合才可信

**不一致的地方，就是推理出错的地方**
</div>

---

# Part 3 · 空间推理

---

# 空间推理的挑战

### 为什么空间推理难？

<div class="grid grid-cols-3 gap-4 mt-6">

<div class="p-4 border rounded text-center">
**单帧信息不足**

深度信息在投影中丢失，单张图像无法确定三维位置
</div>

<div class="p-4 border rounded text-center">
**视角依赖**

同一场景，不同视角下空间关系的语言描述完全不同
</div>

<div class="p-4 border rounded text-center">
**遮挡**

物体互相遮挡，不可见部分的空间关系只能从约束推断
</div>

</div>

<div class="mt-8 p-4 bg-blue-50 border-l-4 border-blue-400 text-gray-700">

**我们的思路**：用结构化推理链显式表达空间关系

→ 这是 Signal is Physics 在视觉通道上的具体实现

</div>

---

# ViewFusion · 多视角空间推理链

<div class="grid grid-cols-2 gap-8 mt-4">

<div>

### 任务

多视角下的空间关系问答

### 核心创新

Structured Spatial Thinking Chain

每一步推理对应一个空间几何操作，推理链可验证

### 定量结果

在多视角空间推理基准上显著超越 baseline

</div>

<div class="p-4 bg-gray-100 rounded text-sm text-gray-700">

```
输入：摄像机 A、B、C 的图像
         ↓
Step 1: 确定各视角坐标系
         ↓
Step 2: 识别目标在各视角的位置
         ↓
Step 3: 三角化，确定三维位置
         ↓
Step 4: 推断空间关系
         ↓
输出：空间关系答案 ✓
```

</div>

</div>

<div class="mt-4 text-gray-500 text-sm">
Multi-source 视角：多个摄像机 ＝ 多个传感器对同一空间的独立采样
</div>

---

# ViewFusion 的物理意义

<div class="grid grid-cols-2 gap-8 mt-8">

<div>

### 推理步骤 → 物理操作

| 推理步骤 | 对应物理操作 |
|---------|------------|
| 坐标系对齐 | 外参矩阵变换 |
| 深度估计 | 单目深度约束 |
| 三角化 | 多视角几何 |
| 关系推断 | 三维空间运算 |

</div>

<div>

### 多源一致性的体现

不同视角的推理结论必须几何自洽

```
视角 A 推断："目标在左前方"
视角 B 推断："目标在右后方"
        ↓
几何约束校验：矛盾！
        ↓
推理链重新校正
```

</div>

</div>

<div class="mt-6 p-3 bg-blue-50 border-l-4 border-blue-400 text-gray-700">
结论：推理结构是空间物理约束的语言表达
</div>

---

# CamReasoner · 摄像机运动理解

<div class="grid grid-cols-2 gap-8 mt-6">

<div>

### 任务

视频中的摄像机运动语义分类

### 核心创新

RL 驱动的结构化空间推理

模型学会选择与物理运动规律一致的推理路径

</div>

<div class="p-4 bg-gray-100 rounded text-gray-700">

### 运动类型的几何含义

| 运动类型 | 物理几何含义 |
|--------|------------|
| 推镜 (Push) | 焦距不变，摄像机前移 |
| 拉镜 (Pull) | 焦距不变，摄像机后退 |
| 旋转 (Pan) | 光心不动，光轴旋转 |
| 变焦 (Zoom) | 光心不动，焦距变化 |

</div>

</div>

---

# CamReasoner 的物理意义

<div class="mt-8">

### 摄像机运动是物理约束最直接的视觉载体

摄像机的每一种运动，都对应确定的三维几何变换

视频帧序列必须与这种几何变换在物理上自洽

</div>

<div class="mt-6 grid grid-cols-2 gap-8">

<div class="p-4 border rounded">

### RL 的作用

不是学"什么答案对"，而是学"什么推理路径与物理运动规律一致"

</div>

<div class="p-4 border rounded">

### 收益

错误的推理路径会因为违反物理约束而被惩罚，模型被迫学习物理规律

</div>

</div>

<div class="mt-6 p-3 bg-blue-50 border-l-4 border-blue-400 text-gray-700">
结论：理解摄像机运动，是理解视觉物理的第一步
</div>

---

# 空间推理小结

<div class="grid grid-cols-2 gap-8 mt-6">

<div>

### 在框架中的位置

| 工作 | 解决的问题 |
|------|----------|
| ViewFusion | 多视角几何一致性 |
| CamReasoner | 摄像机运动的物理理解 |

</div>

<div>

### 回扣核心主题

**Signal is Physics**：空间推理在做的事，是从图像信号中还原三维物理空间

**Multi-source**：多视角的几何自洽性，就是空间推理的验证器

</div>

</div>

<div class="mt-8 p-4 bg-green-50 border-l-4 border-green-400 text-gray-700">

空间推理解决了"**在哪里**"

→ 时序推理解决"**什么时候**"

</div>

---

# Part 4 · 时序推理

---

# 时序推理的挑战

### 为什么时间轴上的推理特别难？

<div class="grid grid-cols-2 gap-6 mt-6">

<div class="p-4 border rounded">

**帧采样丢失信息**

视频是连续时间的离散采样，帧间事件不可见

采样率不均匀时，时序关系进一步模糊

</div>

<div class="p-4 border rounded">

**位置编码的系统性偏差**

现有模型的时序位置编码存在已知偏差，导致对事件发生时间的感知系统性偏移

</div>

</div>

<div class="mt-8 p-4 bg-blue-50 border-l-4 border-blue-400 text-gray-700">

**我们的思路**：在不重训练的前提下，校准时序感知

→ 时间连贯性是视频信号最基本的物理约束

</div>

---

# PAS · 时序稳定性校准

<div class="grid grid-cols-2 gap-8 mt-6">

<div>

### 任务

Video LLMs 的 temporal encoding 偏差问题

### 核心创新

Training-free 稳定器

无需重新训练，直接在推理阶段注入时序物理约束

### 效果

显著减少时序感知偏差，提升时序问答准确率

</div>

<div class="p-4 bg-gray-100 rounded text-sm text-gray-700">

```
无 PAS:
帧序列: F1 F2 F3 F4 F5
感知:   F1    F3 F4 F5
           ↑
        时序空洞，偏差累积

有 PAS:
帧序列: F1 F2 F3 F4 F5
感知:   F1 F2 F3 F4 F5
物理约束注入 → 时序稳定
```

</div>

</div>

<div class="mt-4 p-3 bg-blue-50 border-l-4 border-blue-400 text-gray-700">
结论：时间连贯性是物理真实性的基础保障
</div>

---

# FrameMind · 帧间推理与强化学习

<div class="grid grid-cols-2 gap-8 mt-6">

<div>

### 任务

视频帧交织推理

### 核心创新

RL 驱动的帧间逻辑推理

### 推理路径示例

```
帧 t:   观察状态 A
帧 t+1: 推断变化 A→B
帧 t+2: 验证物理因果 ✓
        预测状态 C
```

RL 奖励物理因果一致的推理路径

</div>

<div>

### Multi-source 视角

相邻帧 = 对同一物理场景的**时序采样**

帧间推理必须满足因果自洽

```
帧 n:   球在空中
帧 n+1: 球落地
帧 n+2: 球弹起
   ↓
物理校验: 轨迹满足重力方程 ✓
```

若不自洽 → RL 惩罚 → 模型纠正

</div>

</div>

---

# 时序推理的更深含义

<div class="mt-6 text-center text-xl">
时间轴上的推理 = 对**物理因果链**的建模
</div>

<div class="mt-8 p-4 bg-gray-100 rounded text-gray-700">

**直觉例子**：打碎一个杯子

时序推理能告诉我们：
- 撞击力的大小（由声音强度和破碎程度推断）
- 材质属性（由碎裂方式推断）
- 运动轨迹（由帧序列推断）

</div>

<div class="mt-6 p-4 bg-yellow-50 border-l-4 border-yellow-400 text-gray-700">

**Multi-source 体现**

音频时间戳 ＋ 视频帧时间戳必须对齐

不对齐 → 就是 **Not in Sync** 问题的根源

</div>

<div class="mt-4 text-center text-gray-500">
因果顺序是物理世界最基本的约束之一
</div>

---

# 时序推理小结

<div class="grid grid-cols-2 gap-8 mt-6">

<div>

### 在框架中的位置

| 工作 | 解决的问题 |
|------|----------|
| PAS | 时序位置编码偏差的校准 |
| FrameMind | 帧间因果推理与决策 |

</div>

<div>

### 回扣核心主题

**Signal is Physics**：时序推理在做的事，是从视频信号中还原物理因果链

**Multi-source**：音视频时间戳的对齐，就是时序推理的验证器

</div>

</div>

<div class="mt-8 p-4 bg-green-50 border-l-4 border-green-400 text-gray-700">

空间和时间都解决了

→ 现在让多个信号源**彼此验证**

</div>

---

# Part 5 · 多源一致性的实现

---

# 从单源推理到多源校验

<div class="grid grid-cols-2 gap-8 mt-8">

<div>

### 回顾

空间推理和时序推理都是**单通道内**的结构化推理

- ViewFusion：在视觉通道内推理空间
- PAS / FrameMind：在时间维度内推理因果

</div>

<div>

### 新问题

不同信号源之间，如何相互验证？

**物理基础**：同一物理事件在多个信号源上留下**冗余但一致**的痕迹

这种冗余是天然的验证资源

</div>

</div>

<div class="mt-8 p-4 bg-blue-50 border-l-4 border-blue-400 text-gray-700">
同一声音，被多个麦克风记录；同一场景，被多个摄像机拍摄。
它们描述的是同一个物理真相。
</div>

---

# 音频作为独立推理通道

### 音频的独特物理属性

<div class="grid grid-cols-3 gap-4 mt-6">

<div class="p-4 border rounded text-center">
**时间分辨率极高**

采样率 44100Hz，远超视频帧率，能捕捉极短暂的物理事件
</div>

<div class="p-4 border rounded text-center">
**空间约束强**

时延差 → 方向

强度衰减 → 距离

完整的空间几何信息藏在声学信号中
</div>

<div class="p-4 border rounded text-center">
**不受光照遮挡影响**

黑暗中、障碍物后，音频信号依然携带完整的物理信息
</div>

</div>

<div class="mt-6 p-4 bg-yellow-50 border-l-4 border-yellow-400 text-gray-700">

回扣：音频 = 压力波的时空编码，里面藏着完整的空间几何信息

**音频是被严重低估的推理通道**

</div>

---

# Thinking with Sound · 音频推理链

<div class="grid grid-cols-2 gap-8 mt-6">

<div>

### 任务

Audio Chain-of-Thought for multimodal reasoning

### 核心创新

显式音频推理步骤

每一步推理对应一个声学物理操作

### 意义

音频推理链足够完整，才能真正充当跨模态验证器

</div>

<div class="p-4 bg-gray-100 rounded text-sm text-gray-700">

**推理链展开示例**

```
输入：双麦克风录音片段
   ↓
Step 1: 计算两麦克风的时延差
        Δt = t_R - t_L = 0.3ms
   ↓
Step 2: 由时延差推断声源方向
        θ = arcsin(c·Δt / d) = 30°
   ↓
Step 3: 由强度衰减推断距离
        r ≈ 2.4m
   ↓
输出：声源在右前方 30°，距离约 2.4m
```

</div>

</div>

<div class="mt-4 p-3 bg-blue-50 border-l-4 border-blue-400 text-gray-700">
结论：音频不只是特征，它可以承载完整的推理逻辑
</div>

---

# AudioRouter · 多源一致性校验的实现

<div class="grid grid-cols-2 gap-8 mt-4">

<div>

### 任务

用音频逻辑辅助视频动作理解

### 核心创新

RL-based 双推理路径

### 一致性校验机制

```
视频通道 → 推断"动作 A"
音频通道 → 推断"声音对应动作 B"
       ↓
  A ≠ B，不一致！
       ↓
  RL 学会重新权衡
  而不是盲目信任视觉
       ↓
  修正输出
```

</div>

<div>

### 案例：音频修正视频误判

**场景**：视频显示"正在切菜"

| 通道 | 推断 |
|------|------|
| 视觉 | 正在切菜 ✓ |
| 音频 | 听到的是敲击声，不是切割声 |

→ 音频不一致，触发重新推理

→ 修正：正在剁肉，而非切菜

<div class="mt-4 p-3 bg-green-50 border rounded text-gray-700">
音频的物理逻辑充当了视觉推理的验证器
</div>

</div>

</div>

---
layout: center
---

# 多源一致性的统一视角

<div class="font-mono text-sm p-6 bg-gray-100 rounded mt-4 text-gray-700">

```
视觉推理链     ──┐
音频推理链     ──┤
多麦克风阵列   ──┼──→  一致性校验  ──→  物理真实性确认
多视角摄像机   ──┤          ↑
水声换能器阵列 ──┘     不一致 → 重新推理
```

</div>

<div class="mt-8 grid grid-cols-3 gap-4 text-sm text-center">

<div class="p-3 border rounded">
ViewFusion 体现**跨传感器**（多摄像机）
</div>

<div class="p-3 border rounded">
AudioRouter 体现**跨模态**（视觉＋音频）
</div>

<div class="p-3 border rounded">
水声阵列是**两者的极端融合**
</div>

</div>

---

# 多源推理小结

<div class="mt-6 p-4 bg-blue-50 border-l-4 border-blue-400 text-gray-700">

**Signal is Physics**：多源一致性推理在做的事，是验证多个独立观测是否描述了同一个物理真相

</div>

<div class="mt-6 p-6 border-2 border-blue-400 rounded text-center">

### 核心主张正式确立

**Multi-source Consistency is the Validator of Physical Truth**

</div>

<div class="mt-6 text-center text-gray-500 text-xl">
这套框架能用在哪里？
</div>

---

# Part 6 · 落点：向上延伸

---

# 推理驱动决策

### 从理解到行动的跨越

<div class="grid grid-cols-2 gap-8 mt-6">

<div>

### FrameMind

视频推理 → 强化学习决策

推理链直接转化为动作指令

### Video-to-BT

人类示范 → 机器人行为树生成

物理推理理解人类意图，生成可执行行为树

</div>

<div class="p-4 bg-gray-100 rounded text-sm text-gray-700">

```
物理信号输入
     ↓
结构化推理（理解物理场景）
     ↓
推理链 → 动作序列
     ↓
RL 优化 → 决策输出
     ↓
机器人 / 智能体执行
```

</div>

</div>

<div class="mt-6 p-3 bg-green-50 border-l-4 border-green-400 text-gray-700">
结论：物理推理的终点是可靠的行动
</div>

---

# GUI 与具身场景

<div class="grid grid-cols-2 gap-8 mt-6">

<div>

### Dimo-gui

视觉推理驱动 GUI 交互

理解界面的视觉物理结构 → 可靠地执行操作序列

### CamReasoner 在具身导航中的潜力

摄像机运动理解 → 机器人自身运动的空间推理

理解"我在哪里、我在往哪里走"

</div>

<div>

### Multi-source 体现

具身智能体需要同时整合：

- 视觉（摄像机）
- 触觉（力传感器）
- 运动（IMU、编码器）
- 音频（环境声）

多传感器的信号必须在物理上自洽，才能支持可靠决策

</div>

</div>

<div class="mt-6 p-3 bg-blue-50 border-l-4 border-blue-400 text-gray-700">
结论：物理推理是具身智能的认知基础
</div>

---
layout: center
---

# 从信号到行动的完整链路

<div class="mt-8 p-6 bg-gray-100 rounded text-gray-700">

```
多源物理信号输入
        ↓
   空间推理
 (ViewFusion, CamReasoner)
        ↓
   时序推理
 (PAS, FrameMind)
        ↓
  多源一致性校验
 (AudioRouter, Thinking with Sound)
        ↓
    决策输出
 (Video-to-BT, Dimo-gui, FrameMind)
```

</div>

<div class="mt-6 text-center text-gray-500">
这就是我们构建的完整研究框架

每一步都在践行 **Signal is Physics**
</div>

---

# Part 7 · 水声 AI：终极考场

---

# 为什么水声是终极考场？

<div class="grid grid-cols-2 gap-8 mt-4">

<div>

### 极端物理约束

- **多径反射**：声波在水中的复杂传播路径
- **温度梯度**：声速随深度持续变化
- **无视觉辅助**：纯单模态，只有声学信号
- **极高噪声**：背景噪声强，信噪比极低

### 一句话

如果我们的框架在这里有效，它就是真正理解了物理

</div>

<div>

### 回扣核心主题

**Signal is Physics**：水声是"信号即物理"最极端的体现——只有声学信号和物理规律，没有任何其他辅助

**Multi-source**：水声阵列的每一个换能器都是独立观测，它们的一致性就是目标定位的唯一依据

</div>

</div>

<div class="mt-4 p-3 bg-red-50 border-l-4 border-red-400 text-gray-700">
水声：把我们框架的每一个假设都推到极限
</div>

---

# 水声 AI 的应用前景

<div class="grid grid-cols-3 gap-4 mt-8">

<div class="p-4 border rounded text-center">

### 海洋探测

深海生物探测、海洋环境监测、声学断层成像

</div>

<div class="p-4 border rounded text-center">

### 水下无人系统

AUV 自主导航、水下通信、协同作业

</div>

<div class="p-4 border rounded text-center">

### 海底资源勘探

矿产资源定位、管道检测、地质结构分析

</div>

</div>

<div class="mt-6 p-4 bg-yellow-50 border-l-4 border-yellow-400 text-gray-700">

**现状**：AI 渗透最浅、物理建模最复杂、应用价值最大

**时机**：正是因为 AI 还没有真正进入这个领域，先行者的优势极大

</div>

---

# 我们的方法论迁移

### 已有能力 → 水声任务映射

| 已有能力 | 水声任务映射 |
|---------|-----------|
| 多视角空间推理（ViewFusion） | 阵列定向：多换能器时延差 → 声源方向 |
| 时序稳定性校准（PAS） | 多径抑制：区分直达波与反射波 |
| 跨模态一致性校验（AudioRouter） | 声图融合：声学信号与图像的联合推理 |
| 音频推理链（Thinking with Sound） | 水声特征解析：从原始 IQ 信号到目标重建 |

<div class="mt-8 p-4 bg-green-50 border-l-4 border-green-400 text-gray-700">
结论：我们不是从零开始，我们带着验证过的工具箱进入新场景
</div>

---

# 长期布局与招募

### 三阶段路线图

<div class="grid grid-cols-3 gap-4 mt-6">

<div class="p-4 border-2 border-green-400 rounded">

### Phase 1 ✅

已有 AI 工作的方法论沉淀

Signal is Physics 框架建立

</div>

<div class="p-4 border-2 border-blue-400 rounded">

### Phase 2

图像层声纳

UATD / FSOD 数据集

目标检测与识别

</div>

<div class="p-4 border-2 border-gray-400 rounded">

### Phase 3

物理层原始 IQ 信号

→ 图像重建

真实声纳设备验证

</div>

</div>

<div class="mt-6 p-4 bg-blue-50 border-l-4 border-blue-400 text-gray-700">

**招募信号**

对物理驱动 AI、水声信号处理、多模态推理感兴趣的同学，欢迎课后交流

</div>

---

# Part 8 · 收尾

---

# 我们的研究版图

| 层次 | 工作 |
|------|------|
| **感知层** | Spatial Blind Spot · Not in Sync · Visual CoT |
| **推理层** | ViewFusion · CamReasoner · PAS · FrameMind · Thinking with Sound · AudioRouter |
| **决策层** | Video-to-BT · Dimo-gui · FrameMind |

<div class="mt-8 p-4 bg-gray-100 rounded text-center text-gray-700">

感知层揭示**问题**

推理层提供**方法**

决策层验证**价值**

</div>

---
layout: center
---

# 核心观点汇总

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

# 谢谢！

欢迎提问与讨论

<div class="mt-8 text-gray-400 text-sm">
your@email.com
</div>

<img src="/Image/uc_yellow.svg" class="absolute top-8 right-8 h-16" />
