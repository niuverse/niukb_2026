# World Model 综述 (2024-2025)

> 调研日期: 2026-02-24  
> 调研范围: arXiv、CVPR、ICCV、ICML、NeurIPS、Nature 等顶级会议  
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
| 2025 | GWM | 3D Gaussian Splatting 世界模型 |

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
| **PlaNet** | ICML 2019 | 连续控制任务的潜在动力学规划 |
| **TD-MPC2** | ICLR 2024 | 可扩展、鲁棒的世界模型 |
| **DayDreamer** | CoRL 2022 | 真实机器人上的世界模型学习 |

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
| **V-JEPA 2** | Meta 2025 | 自监督视频预训练，支持规划 |
| **Cosmos** | NVIDIA 2025 | 物理 AI 世界基础模型平台 |
| **Ctrl-World** | arXiv 2025 | 可控多视角世界模型，支持 VLA 评估 |
| **Video Prediction Policy** | ICML 2025 | 视频预测策略，隐式逆动力学 |

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
| **ManiGaussian** | ECCV 2024 | 多任务操作的高斯动态预测 |
| **GAF** | arXiv 2025 | 高斯动作场，4D 表示动作推理 |
| **Physically Embodied Gaussians** | CoRL 2024 | 粒子-高斯双表示，物理感知 |

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
| **Genie 3** | DeepMind 2025 | 实时交互，24fps 生成 |
| **iVideoGPT** | NeurIPS 2024 | 可扩展交互视频世界模型 |
| **Pandora** | arXiv 2024 | 语言动作 + 视频状态的世界模型 |

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
| **DRAMA** | arXiv 2024 | Mamba-2 世界模型，Atari100k SOTA |
| **GLAM** | AAAI 2025 | 全局-局部感知 Mamba 世界模型 |
| **Dyn-O** | arXiv 2025 | 对象中心状态空间模型 |
| **StateSpaceDiffuser** | arXiv 2025 | Mamba + 扩散，长上下文世界模型 |

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
Dreamer (2020) → DreamerV2 (2021) → DreamerV3 (2025)
```

| 特性 | Dreamer | DreamerV2 | DreamerV3 |
|------|---------|-----------|-----------|
| 状态表示 | 连续潜在变量 | 离散潜在变量 | 离散潜在变量 |
| 策略学习 | 价值函数 | 价值函数 + 策略梯度 | 策略梯度 |
| 鲁棒性 | 基础 | 改进 | 跨域泛化 |
| 参数规模 | 小型 | 中型 | 可扩展 |
| 典型应用 | 连续控制 | Atari 游戏 | 多样化任务 |

**DreamerV3 关键创新**:
- **Symlog 预测**: 对称对数变换处理多尺度奖励
- **KL 平衡**: 自适应 KL 散度权重，防止后验坍塌
- **归一化**: 输入归一化提高跨域泛化

### 3.2 视频生成世界模型对比

| 模型 | 机构 | 规模 | 特点 | 应用场景 |
|------|------|------|------|----------|
| **Sora** | OpenAI | 大规模 | 文本/图像到视频，物理模拟 | 内容创作、仿真 |
| **Genie 2** | DeepMind | 基础模型 | 可交互 3D 环境，动作可控 | 游戏、智能体训练 |
| **Cosmos** | NVIDIA | 开源 | 物理 AI 平台，多模态 | 机器人、自动驾驶 |
| **V-JEPA 2** | Meta | 大规模 | 自监督预训练，特征预测 | 视觉理解、规划 |
| **Wan** | 阿里巴巴 | 开源 | 中文优化，物理一致性检测 | 视频生成 |

### 3.3 3D Gaussian 世界模型对比

| 模型 | 表示 | 动态建模 | 动作条件 | 应用 |
|------|------|----------|----------|------|
| **GWM** | 3DGS + Latent DiT | 高斯参数传播 | ✓ | 机器人操作 |
| **ManiGaussian** | 3DGS | 逐点变化预测 | ✓ | 多任务操作 |
| **GAF** | 3DGS + 运动属性 | 高斯动作场 | ✓ | 动作推理 |
| **DriveDreamer4D** | 4DGS | 轨迹条件生成 | ✓ | 自动驾驶 |

---

## 4. 2024-2025 年重要工作

### 4.1 生成式世界模型

| 标题 | 作者/机构 | 会议 | 一句话总结 |
|------|-----------|------|------------|
| **Ctrl-World: A Controllable Generative World Model for Robot Manipulation** | Stanford/Tsinghua | arXiv 2025 | 多视角、细粒度动作控制的世界模型，支持 VLA 策略评估和改进 |
| **GWM: Towards Scalable Gaussian World Models for Robotic Manipulation** | BIGAI | ICCV 2025 | 基于 3D Gaussian Splatting 和 Latent DiT 的可扩展世界模型 |
| **Genie 2: A Large-Scale Foundation World Model** | DeepMind | 2024 | 单图生成无限可交互 3D 环境，支持智能体训练 |
| **Cosmos: World Foundation Model Platform for Physical AI** | NVIDIA | 2025 | 物理 AI 世界基础模型平台，支持机器人、自动驾驶 |
| **V-JEPA 2: Self-Supervised Video Models Enable Understanding, Prediction and Planning** | Meta | 2025 | 自监督视频预训练，支持机器人规划 |

### 4.2 世界模型与 VLA 结合

| 标题 | 作者/机构 | 会议 | 一句话总结 |
|------|-----------|------|------------|
| **Video Prediction Policy: A Generalist Robot Policy with Predictive Visual Representations** | Tsinghua/UCB | ICML 2025 | 利用视频扩散模型的预测特征学习通用机器人策略 |
| **FLARE: Robot Learning with Implicit World Modeling** | Google | RSS 2025 | 隐式世界建模的机器人学习 |
| **WorldVLA: Towards Autoregressive Action World Model** | DAMO | arXiv 2025 | 自回归动作世界模型 |
| **EnerVerse: Envisioning Embodied Future Space for Robotics Manipulation** | Shanghai AI Lab | arXiv 2025 | 4D 潜在动态，支持机器人操作 |

### 4.3 状态空间模型世界模型

| 标题 | 作者/机构 | 会议 | 一句话总结 |
|------|-----------|------|------------|
| **DRAMA: Mamba-Enabled Model-Based Reinforcement Learning** | Trinity College | arXiv 2024 | 首个基于 Mamba-2 的世界模型，7M 参数达到 SOTA |
| **GLAM: Global-Local Variation Awareness in Mamba-Based World Model** | - | AAAI 2025 | 全局-局部感知的 Mamba 世界模型 |
| **StateSpaceDiffuser: Bringing Long Context to Diffusion World Models** | - | arXiv 2025 | Mamba + 扩散模型，解决长上下文记忆丢失 |

### 4.4 自动驾驶世界模型

| 标题 | 作者/机构 | 会议 | 一句话总结 |
|------|-----------|------|------------|
| **DriveWorld: 4D Pre-trained Scene Understanding via World Models** | - | CVPR 2024 | 4D 预训练场景理解 |
| **Vista: A Generalizable Driving World Model** | Shanghai AI Lab | NeurIPS 2024 | 可泛化驾驶世界模型 |
| **GaussianWorld: Gaussian World Model for Streaming 3D Occupancy Prediction** | - | CVPR 2025 | 高斯世界模型用于 3D 占用预测 |
| **OccWorld: Learning a 3D Occupancy World Model** | - | ECCV 2024 | 3D 占用世界模型 |

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

| 基准 | 任务 | 指标 |
|------|------|------|
| **DMC** | 连续控制 | Episode Return |
| **Atari100k** | 离散控制 | 归一化分数 |
| **RLBench** | 机器人操作 | 成功率 |
| **nuScenes 视频生成** | 驾驶场景 | FID, FVD |
| **Occ3D 4D 占用** | 场景理解 | mIoU |
| **VBench** | 视频质量 | 多维度评估 |

---

## 6. 应用场景

### 6.1 机器人操作

**核心需求**: 预测物体交互、接触动力学、抓取规划

**代表性工作**:
- **GWM**: 3D 高斯预测接触动态，支持模型预测控制
- **ManiGaussian**: 多任务操作的高斯世界模型
- **Ctrl-World**: 评估和改进 VLA 策略

### 6.2 自动驾驶

**核心需求**: 场景预测、轨迹规划、安全评估

**代表性工作**:
- **DriveWorld**: 4D 预训练场景理解
- **Vista**: 可泛化驾驶世界模型
- **GaussianWorld**: 3D 占用预测

### 6.3 智能体训练

**核心需求**: 无限环境生成、策略评估、安全测试

**代表性工作**:
- **Genie 2/3**: 可交互 3D 环境生成
- **Cosmos**: 物理 AI 仿真平台
- **WorldGym**: 世界模型作为策略评估环境

### 6.4 内容创作

**核心需求**: 高质量视频生成、物理一致性

**代表性工作**:
- **Sora**: 文本/图像到视频生成
- **Veo 3**: 高质量视频生成
- **Marble (World Labs)**: 3D 场景生成

---

## 7. 趋势与挑战

### 7.1 当前趋势

1. **从 2D 到 3D 表示**
   - 3D Gaussian Splatting 成为显式几何建模的主流
   - 结合 NeRF 和 3DGS 的混合表示

2. **视频生成与世界模型的融合**
   - Sora、Genie 等模型模糊了两者的界限
   - 视频预训练 + 动作微调的范式

3. **与 VLA 的深度结合**
   - 世界模型作为 VLA 的评估器和改进器
   - 统一感知-预测-决策框架

4. **状态空间模型的崛起**
   - Mamba 作为 Transformer 的高效替代
   - 线性复杂度适合长序列建模

5. **物理一致性优先**
   - 从像素保真度转向物理准确性
   - 物理信息约束的生成模型

### 7.2 开放挑战

1. **长期一致性**
   - 长时程视频预测的误差累积
   - 需要更好的时序建模机制

2. **物理准确性**
   - 复杂物理现象（流体、形变、断裂）的建模
   - 物理先验与数据驱动学习的结合

3. **实时推理**
   - 高质量生成与实时控制的权衡
   - 模型蒸馏和加速技术

4. **跨域泛化**
   - 从仿真到真实的迁移
   - 跨场景、跨任务的通用世界模型

5. **可解释性与安全性**
   - 世界模型预测的可解释性
   - 安全关键应用中的可靠性保证

### 7.3 未来方向

1. **统一的世界模型架构**
   - 结合 RSSM、扩散模型、3DGS 的混合架构
   - 多模态（视觉、语言、动作）统一建模

2. **世界模型与 LLM 的融合**
   - 利用 LLM 的推理能力指导世界模型
   - 世界模型提供物理 grounding

3. **大规模预训练 + 高效微调**
   - 互联网规模视频预训练
   - 少量机器人数据的高效适应

4. **硬件-算法协同设计**
   - 针对边缘设备的轻量化世界模型
   - 专用加速器支持

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

### 8.2 开源代码

| 项目 | 链接 | 描述 |
|------|------|------|
| **GWM** | https://github.com/Gaussian-World-Model/gaussianwm | 高斯世界模型 |
| **DreamerV3** | https://github.com/danijar/dreamerv3 | 官方实现 |
| **V-JEPA 2** | https://github.com/facebookresearch/vjepa | Meta 官方 |
| **Cosmos** | https://github.com/NVIDIA/Cosmos | NVIDIA 物理 AI |
| **Ctrl-World** | https://ctrl-world.github.io | 可控世界模型 |
| **DRAMA** | https://github.com/realwenlongwang/drama | Mamba 世界模型 |

### 8.3 重要博客与演讲

- **World Models Race 2026** (Introl Blog): 世界模型竞争格局分析
- **World Models Reading List** (Medium): 从入门到精通的论文列表
- **NVIDIA GTC 2025**: Jensen Huang 关于物理 AI 和世界模型的演讲
- **Yann LeCun's AMI Labs**: 世界模型与自主机器智能

---

## 9. 总结

World Model 是具身智能的核心使能技术，2024-2025 年见证了该领域的快速发展。主要趋势包括：

1. **技术路线多元化**: RSSM、视频扩散、3DGS、Mamba 等多种架构并存
2. **应用场景扩展**: 从游戏到机器人、自动驾驶、科学仿真
3. **与 VLA 深度融合**: 世界模型成为 VLA 系统的关键组件
4. **物理一致性重视**: 从追求视觉质量转向物理准确性
5. **开源生态繁荣**: Cosmos、GWM 等开源项目推动社区发展

未来，统一、可扩展、物理一致的世界模型将是实现通用具身智能的关键路径。

---

*最后更新: 2026-02-24*
