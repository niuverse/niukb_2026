# World Model 综述 (2024-2025)

> 调研日期: 2026-02-26  
> 调研范围: arXiv、CVPR、ICCV、ICML、NeurIPS、RSS、CoRL 等顶级会议  
> 重点关注: 2024-2025 年最新进展，特别是机器人/具身智能应用

---

## 1. 领域概述

**World Model（世界模型）** 是具身智能的核心组件，旨在让智能体能够预测其动作对环境的影响，从而在"想象"中进行规划和学习。世界模型模拟环境动态，支持前向推演和反事实推理，是连接感知、预测与决策的关键桥梁。

### 核心思想
- **预测未来**: 给定当前状态和动作，预测未来状态
- **想象学习**: 在模拟环境中进行策略训练，减少真实交互
- **物理理解**: 学习物理规律，支持因果推理

### 发展时间线

| 时间 | 里程碑 | 关键贡献 |
|------|--------|----------|
| 2018 | World Models (Ha & Schmidhuber) | VAE + RNN + Controller 框架 |
| 2019 | PlaNet | RSSM 循环状态空间模型 |
| 2020 | Dreamer | 潜在想象中的策略学习 |
| 2021 | DreamerV2 | 离散世界模型，Atari SOTA |
| 2023 | DreamerV3 | 跨域泛化，Nature 发表 |
| 2024 | Sora | 视频生成作为世界模拟器 |
| 2024 | Genie 2 | 可交互 3D 世界生成 |
| 2025 | Dreamer 4 | 扩散世界模型，纯离线 Minecraft 钻石获取 |
| 2025 | Genie 3 | 实时交互世界模型，24fps 生成 |
| 2025 | Cosmos | NVIDIA 物理 AI 世界基础模型平台 |

### 主要应用场景
- **机器人操作**: 预测物体交互、抓取规划
- **自动驾驶**: 场景预测、轨迹规划
- **游戏 AI**: 环境模拟、策略训练
- **科学仿真**: 分子动力学、气候预测

### 当前挑战
- **长期一致性**: 长时程视频预测的时序漂移
- **物理准确性**: 复杂物理现象（流体、形变）的建模
- **计算效率**: 实时推理与高质量生成的平衡
- **泛化能力**: 跨场景、跨任务的迁移

---

## 2. 技术路线分类

### 2.1 基于 RSSM 的潜在世界模型

**核心思想**: 使用循环状态空间模型 (Recurrent State Space Model) 在紧凑潜在空间建模动态

| 方法 | 会议 | 核心贡献 |
|------|------|----------|
| **DreamerV3** | Nature 2025 | 统一算法解决多样化任务，超人类表现 |
| **Dreamer 4** | arXiv 2025 | 扩散世界模型，纯离线学习 Minecraft 钻石获取 |
| **PlaNet** | ICML 2019 | 连续控制任务的潜在动力学规划 |
| **TD-MPC2** | ICLR 2024 | 可扩展、鲁棒的世界模型 |
| **DayDreamer** | CoRL 2022 | 真实机器人上的世界模型学习 |

**Dreamer 4 关键创新** (2025):
- **扩散世界模型**: 使用扩散模型替代传统 RSSM，更准确预测复杂环境中的物体交互
- **Shortcut Forcing**: 实时交互推理目标函数，单 GPU 实现实时交互
- **高效 Transformer 架构**: 优化计算效率，支持长序列建模
- **纯离线学习**: 首次实现仅通过离线数据在 Minecraft 中获取钻石，无需环境交互

**优势**:
- 计算高效，适合实时控制
- 潜在空间压缩，减少维度灾难

**局限**:
- 视觉重建质量有限
- 难以捕捉复杂几何和物理

### 2.2 基于视频扩散的世界模型

**核心思想**: 利用视频扩散模型生成未来帧，隐式编码物理规律

| 方法 | 会议 | 核心贡献 |
|------|------|----------|
| **Sora** | OpenAI 2024 | 大规模视频生成，物理世界模拟 |
| **V-JEPA 2** | Meta 2025 | 自监督视频预训练，支持规划，零样本机器人控制 |
| **Cosmos** | NVIDIA 2025 | 物理 AI 世界基础模型平台，9000 万亿 token 训练 |
| **Ctrl-World** | arXiv 2025 | 可控多视角世界模型，支持 VLA 评估和改进 |
| **Video Prediction Policy** | ICML 2025 | 视频预测策略，隐式逆动力学 |
| **Genie 3** | DeepMind 2025 | 实时交互，24fps，720p，文本驱动世界生成 |

**V-JEPA 2 关键创新** (2025):
- **联合嵌入预测架构**: 在表示空间而非像素空间进行预测
- **百万小时视频预训练**: 结合互联网规模视频与少量交互数据
- **零样本机器人控制**: 在 Franka 机械臂上实现零样本抓取和放置
- **动作条件世界模型**: V-JEPA 2-AC 使用少于 62 小时机器人视频进行后训练

**Cosmos 关键创新** (2025):
- **世界基础模型平台**: 包含视频筛选流水线、预训练模型、后训练示例和视频 tokenizer
- **开源开放权重**:  permissive license，支持物理 AI 开发者定制
- **多模态支持**: 支持机器人和自动驾驶等多种物理 AI 应用

**Ctrl-World 关键创新** (2025):
- **姿态条件记忆检索**: 保持长时程一致性
- **帧级动作条件**: 实现精确动作控制
- **多视角预测**: 支持现代通用机器人策略评估
- **策略性能提升**: 通过想象合成成功轨迹，策略成功率提升 44.7%

**Genie 3 关键创新** (2025):
- **实时交互**: 24fps，720p 实时生成
- **长时程一致性**: 视觉记忆延伸至一分钟前
- **可提示世界事件**: 文本驱动的环境干预
- **涌现一致性**: 无需显式 3D 表示即可保持环境一致性

**优势**:
- 高质量视觉生成
- 利用大规模视频预训练

**局限**:
- 推理速度慢
- 动作可控性有限

### 2.3 基于 3D Gaussian Splatting 的世界模型

**核心思想**: 使用 3D 高斯原语显式建模场景几何和动态

| 方法 | 会议 | 核心贡献 |
|------|------|----------|
| **GWM** | ICCV 2025 | 可扩展高斯世界模型，机器人操作 |
| **GAF** | arXiv 2025 | 高斯动作场，4D 表示动作推理 |
| **PIN-WM** | RSS 2025 | 物理驱动世界模型，可微物理仿真 |
| **ManiGaussian** | ECCV 2024 | 多任务操作的高斯动态预测 |
| **Physically Embodied Gaussians** | CoRL 2024 | 粒子-高斯双表示，物理感知 |
| **4D LangSplat** | CVPR 2025 | 4D 语言高斯 splatting，开放词汇查询 |

**GAF (Gaussian Action Field) 关键创新** (2025):
- **V-4D-A 框架**: Vision-to-4D-to-Action，直接动作推理
- **可学习运动属性**: 扩展 3DGS 实现 4D 动态场景建模
- **动作-视觉对齐去噪**: 统一表示结合动作和高斯感知
- **性能提升**: PSNR +11.5dB，机器人操作成功率 +7.3%

**PIN-WM 关键创新** (2025):
- **物理驱动**: 结合可微物理和可微渲染
- **端到端辨识**: 从视觉观测直接辨识 3D 刚体动力学
- **少量任务无关数据**: 仅需少量交互轨迹
- **数字表亲 (Digital Cousins)**: 物理感知随机化弥合 Sim2Real 差距

**优势**:
- 显式 3D 几何，支持精确空间推理
- 实时渲染，适合闭环控制

**局限**:
- 动态场景重建挑战
- 物理属性建模有限

### 2.4 基于 Transformer 的自回归世界模型

**核心思想**: 将世界建模为序列预测问题，使用 Transformer 建模时序依赖

| 方法 | 会议 | 核心贡献 |
|------|------|----------|
| **Genie 2** | DeepMind 2024 | 大规模基础世界模型，可交互 3D 环境 |
| **Genie 3** | DeepMind 2025 | 实时交互，24fps 生成，文本驱动 |
| **iVideoGPT** | NeurIPS 2024 | 可扩展交互视频世界模型 |
| **Pandora** | arXiv 2024 | 语言动作 + 视频状态的世界模型 |
| **WorldVLA** | arXiv 2025 | 自回归动作世界模型 |

**优势**:
- 利用 LLM 的推理能力
- 支持语言条件生成

**局限**:
- 计算资源需求大
- 长序列一致性挑战

### 2.5 基于 State Space Models (Mamba) 的世界模型

**核心思想**: 使用 Mamba 状态空间模型替代 Transformer/RNN，线性复杂度建模长序列

| 方法 | 会议 | 核心贡献 |
|------|------|----------|
| **DRAMA** | ICLR 2025 | Mamba-2 世界模型，Atari100k SOTA，7M 参数 |
| **GLAM** | AAAI 2025 | 全局-局部感知 Mamba 世界模型 |
| **Dyn-O** | arXiv 2025 | 对象中心状态空间模型 |
| **StateSpaceDiffuser** | arXiv 2025 | Mamba + 扩散，长上下文世界模型 |

**DRAMA 关键创新** (2025):
- **线性复杂度**: O(n) 内存和计算复杂度
- **参数高效**: 仅 7M 参数达到 SOTA
- **样本高效**: 优于 RNN 和 Transformer 基线

**GLAM 关键创新** (2025):
- **全局-局部变化感知**: 改进世界模型推理质量
- **变化预测**: 感知和预测轨迹间的变化

**优势**:
- 线性复杂度，适合长序列
- 硬件高效，推理速度快

**局限**:
- 表达能力 vs 效率的权衡
- 生态系统相对不成熟

---

## 3. 重要模型详细对比

### 3.1 Dreamer 系列演进

```
Dreamer (2020) → DreamerV2 (2021) → DreamerV3 (2023) → Dreamer 4 (2025)
```

| 特性 | Dreamer | DreamerV2 | DreamerV3 | Dreamer 4 |
|------|---------|-----------|-----------|-----------|
| 状态表示 | 连续潜在变量 | 离散潜在变量 | 离散潜在变量 | 扩散模型 |
| 策略学习 | 价值函数 | 价值函数 + 策略梯度 | 策略梯度 | 想象训练 |
| 鲁棒性 | 基础 | 改进 | 跨域泛化 | 复杂交互预测 |
| 参数规模 | 小型 | 中型 | 可扩展 | 可扩展 |
| 典型应用 | 连续控制 | Atari 游戏 | 多样化任务 | Minecraft 钻石获取 |

**Dreamer 4 核心突破**:
- **纯离线学习**: 无需环境交互，仅从离线数据学习
- **复杂任务**: 需要选择超过 20,000 个鼠标和键盘动作序列
- **实时推理**: 单 GPU 实现实时交互推理

### 3.2 视频生成世界模型对比

| 模型 | 机构 | 规模 | 特点 | 应用场景 |
|------|------|------|------|----------|
| **Sora** | OpenAI | 大规模 | 文本/图像到视频，物理模拟 | 内容创作、仿真 |
| **Genie 3** | DeepMind | 基础模型 | 实时 24fps，720p，文本驱动 | 游戏、智能体训练 |
| **Cosmos** | NVIDIA | 开源 | 9000 万亿 token，物理 AI 平台 | 机器人、自动驾驶 |
| **V-JEPA 2** | Meta | 大规模 | 自监督预训练，零样本控制 | 视觉理解、规划 |
| **Ctrl-World** | Stanford/Tsinghua | 中等 | 多视角，细粒度动作控制 | VLA 评估和改进 |
| **Wan** | 阿里巴巴 | 开源 | 中文优化，物理一致性检测 | 视频生成 |

### 3.3 3D Gaussian 世界模型对比

| 模型 | 表示 | 动态建模 | 动作条件 | 应用 |
|------|------|----------|----------|------|
| **GWM** | 3DGS + Latent DiT | 高斯参数传播 | ✓ | 机器人操作 |
| **GAF** | 3DGS + 运动属性 | 高斯动作场 | ✓ | 动作推理 |
| **PIN-WM** | 3DGS + 可微物理 | 物理仿真 | ✓ | 非抓取操作 |
| **ManiGaussian** | 3DGS | 逐点变化预测 | ✓ | 多任务操作 |
| **DriveDreamer4D** | 4DGS | 轨迹条件生成 | ✓ | 自动驾驶 |

---

## 4. 2025 年重要工作详解

### 4.1 生成式世界模型

| 标题 | 作者/机构 | 会议 | 一句话总结 |
|------|-----------|------|------------|
| **Dreamer 4: Training Agents Inside of Scalable World Models** | Danijar Hafner et al. | arXiv 2025 | 扩散世界模型实现纯离线 Minecraft 钻石获取 |
| **Ctrl-World: A Controllable Generative World Model for Robot Manipulation** | Stanford/Tsinghua | arXiv 2025 | 多视角、细粒度动作控制，VLA 策略提升 44.7% |
| **Genie 3: A New Frontier for World Models** | DeepMind | 2025 | 实时 24fps 交互，720p，文本驱动世界生成 |
| **Cosmos: World Foundation Model Platform for Physical AI** | NVIDIA | 2025 | 物理 AI 世界基础模型平台，开源开放权重 |
| **V-JEPA 2: Self-Supervised Video Models Enable Understanding, Prediction and Planning** | Meta | 2025 | 零样本机器人控制，62 小时机器人视频后训练 |
| **GAF: Gaussian Action Field as a 4D Representation** | Tsinghua | arXiv 2025 | 高斯动作场 4D 表示，操作成功率 +7.3% |

### 4.2 物理感知世界模型

| 标题 | 作者/机构 | 会议 | 一句话总结 |
|------|-----------|------|------------|
| **PIN-WM: Learning Physics-INformed World Models for Non-Prehensile Manipulation** | NUDT/Shenzhen/Wuhan | RSS 2025 | 可微物理驱动，端到端 3D 刚体动力学辨识 |
| **PhysWorld: From Real Videos to World Models of Deformable Objects** | - | arXiv 2025 | 物理感知演示合成，学习高效世界模型 |
| **WISA: World Simulator Assistant for Physics-Aware Text-to-Video** | - | NeurIPS 2025 | 提升 T2V 模型与真实物理的对齐 |

### 4.3 世界模型与 VLA 结合

| 标题 | 作者/机构 | 会议 | 一句话总结 |
|------|-----------|------|------------|
| **Video Prediction Policy: A Generalist Robot Policy with Predictive Visual Representations** | Tsinghua/UCB | ICML 2025 | 利用视频扩散模型预测特征学习通用策略 |
| **GigaBrain-0: A World Model-Powered Vision-Language-Action Model** | - | arXiv 2025 | 世界模型生成数据增强 VLA 泛化能力 |
| **WorldVLA: Towards Autoregressive Action World Model** | DAMO | arXiv 2025 | 自回归动作世界模型 |
| **EnerVerse: Envisioning Embodied Future Space for Robotics Manipulation** | Shanghai AI Lab | arXiv 2025 | 4D 潜在动态，支持机器人操作 |

### 4.4 状态空间模型世界模型

| 标题 | 作者/机构 | 会议 | 一句话总结 |
|------|-----------|------|------------|
| **DRAMA: Mamba-Enabled Model-Based Reinforcement Learning** | Trinity College | ICLR 2025 | 首个基于 Mamba-2 的世界模型，7M 参数 SOTA |
| **GLAM: Global-Local Variation Awareness in Mamba-Based World Model** | - | AAAI 2025 | 全局-局部感知的 Mamba 世界模型 |
| **StateSpaceDiffuser: Bringing Long Context to Diffusion World Models** | - | arXiv 2025 | Mamba + 扩散模型，解决长上下文记忆丢失 |

### 4.5 自动驾驶世界模型

| 标题 | 作者/机构 | 会议 | 一句话总结 |
|------|-----------|------|------------|
| **A Survey of World Models for Autonomous Driving** | - | arXiv 2025 | 三层分类：物理世界生成、行为规划、预测-规划交互 |
| **Drive-OccWorld: Vision-Centric 4D Occupancy Forecasting** | ZJU | AAAI 2025 | 4D 占用预测和规划世界模型 |
| **DIO: Decomposable Implicit 4D Occupancy-Flow World Model** | - | CVPR 2025 | 可分解隐式 4D 占用流世界模型 |
| **Epona: Autoregressive Diffusion World Model for Autonomous Driving** | - | ICCV 2025 | 自回归扩散驾驶世界模型 |
| **Policy World Model for Collaborative State-Action Prediction** | - | ICLR 2025 | 集成世界建模和轨迹生成的驾驶范式 |

---

## 5. 数据集与基准

### 5.1 机器人操作数据集

| 数据集 | 规模 | 特点 | 适用任务 |
|--------|------|------|----------|
| **Open X-Embodiment (OXE)** | 1M+ 轨迹 | 22 种机器人形态，527 技能 | 跨形态预训练 |
| **DROID** | 95k 轨迹 | 564 场景，真实机器人数据 | 世界模型训练 |
| **RT-1 数据集** | 130k 演示 | 700+ 任务，13 个月收集 | VLA 训练 |
| **RoboCasa** | 大规模 | 厨房场景，多样化任务 | 家庭机器人 |
| **Meta-World** | 50 任务 | 多任务操作基准 | 元学习 |
| **RLBench** | 100 任务 | 稀疏奖励，多模态观测 | 复杂技能学习 |

### 5.2 自动驾驶数据集

| 数据集 | 规模 | 特点 | 适用任务 |
|--------|------|------|----------|
| **nuScenes** | 1000 场景 | 360° 传感器，3D 标注 | 感知、预测 |
| **Waymo Open** | 1150 场景 | 高质量 LiDAR | 轨迹预测 |
| **OpenDV** | 2000+ 小时 | 视频-文本对 | 视频预训练 |
| **Occ3D** | 40k 帧 | 3D 占用标注 | 占用预测 |

### 5.3 评估基准

| 基准 | 任务 | 指标 | 说明 |
|------|------|------|------|
| **WorldScore** | 世界生成 | 可控性、质量、动态 | ICCV 2025，首个统一世界生成基准 |
| **DMC** | 连续控制 | Episode Return | DeepMind Control Suite |
| **Atari100k** | 离散控制 | 归一化分数 | 100k 步限制 |
| **RLBench** | 机器人操作 | 成功率 | 100 个任务 |
| **nuScenes 视频生成** | 驾驶场景 | FID, FVD | 视频质量评估 |
| **Occ3D 4D 占用** | 场景理解 | mIoU | 3D 占用预测 |
| **VBench** | 视频质量 | 多维度评估 | 视频生成评估 |

**WorldScore 关键特性** (2025):
- **统一评估**: 支持 3D、4D、I2V、T2V 模型
- **3000 测试样本**: 涵盖静态/动态、室内/室外、真实/风格化
- **三维度评估**: 可控性 (Controllability)、质量 (Quality)、动态 (Dynamics)
- **19 个代表性模型**: 包括开源和闭源模型

---

## 6. 应用场景

### 6.1 机器人操作

**核心需求**: 预测物体交互、接触动力学、抓取规划

**代表性工作**:
- **Dreamer 4**: 扩散世界模型预测复杂交互
- **GWM**: 3D 高斯预测接触动态，支持模型预测控制
- **GAF**: 4D 高斯动作场实现动作推理
- **PIN-WM**: 物理驱动世界模型，Sim2Real 迁移
- **Ctrl-World**: 评估和改进 VLA 策略
- **V-JEPA 2**: 零样本机器人控制

### 6.2 自动驾驶

**核心需求**: 场景预测、轨迹规划、安全评估

**代表性工作**:
- **Drive-OccWorld**: 4D 占用预测和规划
- **Epona**: 自回归扩散驾驶世界模型
- **GaussianWorld**: 3D 占用预测
- **Cosmos**: 物理 AI 平台支持自动驾驶

### 6.3 智能体训练

**核心需求**: 无限环境生成、策略评估、安全测试

**代表性工作**:
- **Genie 3**: 实时可交互 3D 环境生成
- **Cosmos**: 物理 AI 仿真平台
- **Dreamer 4**: 想象训练环境
- **WorldGym**: 世界模型作为策略评估环境

### 6.4 内容创作

**核心需求**: 高质量视频生成、物理一致性

**代表性工作**:
- **Sora**: 文本/图像到视频生成
- **Veo 3**: 高质量视频生成
- **Genie 3**: 文本驱动世界生成
- **Marble (World Labs)**: 3D 场景生成

---

## 7. 趋势与挑战

### 7.1 当前趋势

1. **从 2D 到 3D/4D 表示**
   - 3D Gaussian Splatting 成为显式几何建模的主流
   - 4D 动态建模（3D + 时间）成为热点
   - 结合 NeRF 和 3DGS 的混合表示

2. **视频生成与世界模型的融合**
   - Sora、Genie、Cosmos 等模型模糊了两者的界限
   - 视频预训练 + 动作微调的范式
   - 物理一致性优先于像素保真度

3. **实时交互能力**
   - Genie 3 实现 24fps 实时生成
   - Dreamer 4 单 GPU 实时推理
   - 从"生成"到"交互"的范式转变

4. **与 VLA 的深度结合**
   - 世界模型作为 VLA 的评估器和改进器
   - Ctrl-World 实现策略性能提升 44.7%
   - 统一感知-预测-决策框架

5. **物理感知建模**
   - PIN-WM 引入可微物理
   - 物理信息约束的生成模型
   - 从数据驱动到物理驱动

6. **状态空间模型的崛起**
   - Mamba 作为 Transformer 的高效替代
   - DRAMA 实现线性复杂度和参数效率
   - 适合长序列建模

7. **大规模预训练 + 高效微调**
   - Cosmos 9000 万亿 token 预训练
   - V-JEPA 2 百万小时视频预训练
   - 少量机器人数据的高效适应

### 7.2 开放挑战

1. **长期一致性**
   - 长时程视频预测的误差累积
   - Genie 3 支持几分钟交互，但扩展至小时级仍有挑战
   - 需要更好的时序建模机制

2. **物理准确性**
   - 复杂物理现象（流体、形变、断裂）的建模
   - 物理先验与数据驱动学习的结合
   - 物理一致性评估标准

3. **实时推理**
   - 高质量生成与实时控制的权衡
   - 模型蒸馏和加速技术
   - 边缘设备部署

4. **跨域泛化**
   - 从仿真到真实的迁移
   - 跨场景、跨任务的通用世界模型
   - 领域自适应技术

5. **可解释性与安全性**
   - 世界模型预测的可解释性
   - 安全关键应用中的可靠性保证
   - 对抗攻击鲁棒性

6. **多智能体交互**
   - 复杂多智能体环境的建模
   - 社会行为预测
   - 协作与竞争动态

### 7.3 未来方向

1. **统一的世界模型架构**
   - 结合 RSSM、扩散模型、3DGS 的混合架构
   - 多模态（视觉、语言、动作）统一建模
   - 端到端可微仿真

2. **世界模型与 LLM 的融合**
   - 利用 LLM 的推理能力指导世界模型
   - 世界模型提供物理 grounding
   - 统一的世界知识表示

3. **世界模型即服务 (WMaaS)**
   - 云原生世界模型平台
   - 按需生成仿真环境
   - 多租户安全隔离

4. **硬件-算法协同设计**
   - 针对边缘设备的轻量化世界模型
   - 专用加速器支持
   - 神经渲染硬件优化

5. **开放世界建模**
   - 无限场景生成
   - 程序化内容生成
   - 用户自定义世界

---

## 8. 参考资源

### 8.1 综述论文

1. **A Comprehensive Survey on World Models for Embodied AI** (2025)
   - 三轴分类法：功能、时间、空间
   - 覆盖机器人、自动驾驶、通用视频

2. **Understanding World or Predicting Future? A Comprehensive Survey of World Models** (2025)
   - ACM Computing Surveys
   - 世界模型 vs 未来预测的分类

3. **A Survey of Embodied World Models** (2025)
   - 清华 FIB Lab
   - 架构、训练范式、应用、基准

4. **A Survey of World Models for Autonomous Driving** (2025)
   - 三层分类：物理世界生成、行为规划、预测-规划交互

### 8.2 开源代码

| 项目 | 链接 | 描述 |
|------|------|------|
| **Dreamer 4** | https://github.com/danijar/dreamerv4 | 扩散世界模型 |
| **GWM** | https://github.com/Gaussian-World-Model/gaussianwm | 高斯世界模型 |
| **DreamerV3** | https://github.com/danijar/dreamerv3 | 官方实现 |
| **V-JEPA 2** | https://github.com/facebookresearch/vjepa2 | Meta 官方 |
| **Cosmos** | https://github.com/NVIDIA/Cosmos | NVIDIA 物理 AI |
| **Ctrl-World** | https://ctrl-world.github.io | 可控世界模型 |
| **DRAMA** | https://github.com/realwenlongwang/drama | Mamba 世界模型 |
| **WorldScore** | https://github.com/haoyi-duan/WorldScore | 世界生成评估 |
| **PIN-WM** | https://pinwm.github.io | 物理驱动世界模型 |
| **GAF** | https://github.com/ | 高斯动作场 |

### 8.3 重要博客与演讲

- **World Models Race 2026** (Introl Blog): 世界模型竞争格局分析
- **World Models Reading List** (Medium): 从入门到精通的论文列表
- **NVIDIA GTC 2025**: Jensen Huang 关于物理 AI 和世界模型的演讲
- **Yann LeCun's AMI Labs**: 世界模型与自主机器智能
- **DeepMind Genie 3 Blog**: 实时交互世界模型的技术突破

---

## 9. 总结

World Model 是具身智能的核心使能技术，2024-2025 年见证了该领域的爆发式发展。主要突破包括：

1. **Dreamer 4** (2025): 扩散世界模型实现纯离线复杂任务学习，首次在 Minecraft 中仅通过离线数据获取钻石

2. **Genie 3** (2025): 首个实时交互世界模型，24fps、720p 生成，支持文本驱动的世界事件

3. **Cosmos** (2025): NVIDIA 开源物理 AI 世界基础模型平台，9000 万亿 token 预训练

4. **V-JEPA 2** (2025): 零样本机器人控制，结合百万小时视频预训练和少量机器人数据

5. **Ctrl-World** (2025): 可控世界模型显著提升 VLA 策略性能 (+44.7%)

6. **PIN-WM** (2025): 物理驱动世界模型，端到端辨识 3D 刚体动力学

7. **WorldScore** (2025): 首个统一世界生成评估基准

主要趋势包括：
- **技术路线多元化**: RSSM、扩散模型、3DGS、Mamba 等多种架构并存
- **实时交互成为标配**: 从"生成"到"交互"的范式转变
- **物理一致性重视**: 从追求视觉质量转向物理准确性
- **与 VLA 深度融合**: 世界模型成为 VLA 系统的关键组件
- **开源生态繁荣**: Cosmos、WorldScore 等开源项目推动社区发展

未来，统一、可扩展、物理一致、实时交互的世界模型将是实现通用具身智能的关键路径。

---

*最后更新: 2026-02-26*
