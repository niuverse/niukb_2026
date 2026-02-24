# Motion Tracking 最新研究综述 (2024-2025)

> 调研日期: 2026-02-24  
> 调研范围: arXiv、CVPR、ICCV、SIGGRAPH 等顶级会议  
> 重点关注: 2024-2025 年最新论文

---

## 1. 领域概述

Motion Tracking（运动跟踪）是计算机视觉和计算机图形学的核心研究方向，涵盖从**人体姿态估计**、**多目标跟踪**到**点跟踪**等多个子领域。近年来，随着深度学习技术的快速发展，该领域在准确性、实时性和泛化能力方面取得了显著进展。

### 主要应用场景
- **虚拟现实/增强现实 (XR)**: 全身运动捕捉驱动虚拟化身
- **机器人学**: 人机交互、动作模仿学习
- **运动分析**: 体育训练、医疗康复
- **自动驾驶**: 行人轨迹预测
- **内容创作**: 动画制作、游戏开发

### 当前挑战
- **遮挡处理**: 复杂场景中的部分/完全遮挡
- **稀疏输入**: 从有限传感器信号恢复完整运动
- **实时性**: 在边缘设备上实现低延迟跟踪
- **泛化能力**: 跨域、跨场景的鲁棒性

---

## 2. 最新方法分类

### 2.1 基于 Transformer 的方法

**核心思想**: 利用自注意力机制建模长程时序依赖

| 方法 | 会议 | 核心贡献 |
|------|------|----------|
| **ARGTrack** | CVPR 2025 | 自回归生成预训练，通过扩散模型生成未来帧外观 |
| **TokenHMR** | CVPR 2024 | 使用 Token 化姿态表示进行人体网格恢复 |
| **TORE** | ICCV 2023 | Token 缩减策略降低 Transformer 计算复杂度 |
| **MotionGPT** | arXiv 2023 | 将人体运动视为"外语"进行生成建模 |

### 2.2 扩散模型 (Diffusion Models)

**核心思想**: 通过去噪扩散过程生成高质量运动序列

| 方法 | 会议 | 核心贡献 |
|------|------|----------|
| **EMDM** | ECCV 2024 | 高效运动扩散模型，实现快速高质量运动生成 |
| **MotionDiffuse** | TPAMI 2024 | 文本驱动的运动生成 |
| **PMDiff** | ACM MM 2024 | 基于 Mamba 状态空间模型的姿态扩散 |
| **DICE** | ICLR 2025 | 单图像手部-面部交互变形恢复 |

### 2.3 状态空间模型 (State Space Models)

**核心思想**: 使用 Mamba 等线性复杂度序列模型替代 Transformer

| 方法 | 会议 | 核心贡献 |
|------|------|----------|
| **PMDiff** | ACM MM 2024 | 双向 Pose Mamba 去噪器实现序列建模 |
| **STGJMamer** | IMTAS 2025 | 图引导状态空间模型用于 3D 姿态估计 |
| **VMamba** | arXiv 2024 | 视觉状态空间模型用于视觉表示学习 |

### 2.4 稀疏传感器运动捕捉

**核心思想**: 从少量 IMU/视觉传感器恢复全身运动

| 方法 | 会议 | 核心贡献 |
|------|------|----------|
| **Ultra Inertial Poser** | SIGGRAPH 2024 | 结合 UWB 测距约束 IMU 漂移和抖动 |
| **HMD-Poser** | CVPR 2024 | VR 头显上的实时全身运动跟踪 |
| **PIP** | CVPR 2022 | 物理感知实时运动跟踪 |
| **EgoLocate** | TOG 2023 | 稀疏体戴传感器的实时运动捕捉与定位 |

### 2.5 点跟踪 (Point Tracking)

**核心思想**: 跟踪视频中任意点的轨迹

| 方法 | 会议 | 核心贡献 |
|------|------|----------|
| **CoTracker3** | arXiv 2024 | 通过伪标签真实视频简化点跟踪 |
| **TAPIR** | ICCV 2023 | 每帧初始化 + 时序细化的点跟踪 |
| **BootsTAPIR** | ACCV 2024 | 自举训练实现任意点跟踪 |
| **AnthroTAP** | arXiv 2025 | 利用人体运动复杂性自动生成伪标签 |

### 2.6 多目标跟踪 (MOT)

**核心思想**: 同时检测和跟踪多个目标

| 方法 | 会议 | 核心贡献 |
|------|------|----------|
| **MOTIP** | arXiv 2024 | 将 MOT 视为上下文 ID 预测任务 |
| **OmniTrack** | CVPR 2025 | 全景多目标跟踪处理 360° 图像 |
| **MITracker** | CVPR 2025 | 多视图集成用于视觉目标跟踪 |

---

## 3. 重要论文列表

### 3.1 人体姿态估计与运动生成

| 标题 | 作者 | 会议 | 一句话总结 |
|------|------|------|-----------|
| TokenHMR: Advancing Human Mesh Recovery with a Tokenized Pose Representation | Sai Kumar Dwivedi et al. | CVPR 2024 | 使用 Token 化姿态表示提升人体网格恢复精度 |
| Humans in 4D: Reconstructing and Tracking Humans with Transformers | Shubham Goel et al. | ICCV 2023 | 基于 Transformer 的 4D 人体重建与跟踪 |
| EMDM: Efficient Motion Diffusion Model for Fast, High-Quality Human Motion Generation | Wenyang Zhou et al. | ECCV 2024 | 高效运动扩散模型实现快速高质量运动生成 |
| PMDiff: Towards Accurate and Smooth Human Motion Tracking | Dong et al. | ACM MM 2024 | 基于 Mamba 的扩散模型实现准确平滑的运动跟踪 |
| Pose Mamba Diffusion: Realistic Full-Body Motion Generation from Sparse Tracking | Kun Dong et al. | ACM MM 2024 | 从稀疏跟踪信号生成真实全身运动 |

### 3.2 稀疏传感器与实时跟踪

| 标题 | 作者 | 会议 | 一句话总结 |
|------|------|------|-----------|
| Ultra Inertial Poser: Scalable Motion Capture and Tracking | ETH SIPLab | SIGGRAPH 2024 | 结合 UWB 和 IMU 实现可扩展的运动捕捉 |
| HMD-Poser: On-Device Real-time Human Motion Tracking | PICO AI Team | CVPR 2024 | VR 头显端实时全身运动跟踪 |
| Physical Inertial Poser (PIP): Physics-aware Real-time Human Motion Tracking | Xinyu Yi et al. | CVPR 2022 | 物理感知实时运动跟踪 |
| EgoLocate: Real-time Motion Capture, Localization, and Mapping | Xinyu Yi et al. | TOG 2023 | 稀疏传感器的实时运动捕捉与定位建图 |

### 3.3 点跟踪与视觉跟踪

| 标题 | 作者 | 会议 | 一句话总结 |
|------|------|------|-----------|
| CoTracker3: Simpler and Better Point Tracking by Pseudo-labelling Real Videos | Nikita Karaev et al. | arXiv 2024 | 通过伪标签简化并改进点跟踪 |
| Learning to Track Any Points from Human Motion | Inès Hyeonsu Kim et al. | arXiv 2025 | 利用人体运动复杂性训练鲁棒点跟踪器 |
| TAPTR: Tracking Any Point with Transformers as Detection | Hongyang Li et al. | ECCV 2024 | 将点跟踪视为检测任务的 Transformer 方法 |
| LocoTrack: Local All-Pair Correspondence for Point Tracking | Seokju Cho et al. | ECCV 2024 | 局部全对应对应关系实现点跟踪 |

### 3.4 多目标跟踪

| 标题 | 作者 | 会议 | 一句话总结 |
|------|------|------|-----------|
| Multiple Object Tracking as ID Prediction | Ruopeng Gao et al. | arXiv 2024 | 将多目标跟踪重新定义为 ID 预测任务 |
| OmniTrack: Omnidirectional Multi-Object Tracking | CVPR 2025 | CVPR 2025 | 全景图像的多目标跟踪框架 |
| MITracker: Multi-View Integration for Visual Object Tracking | CVPR 2025 | CVPR 2025 | 多视图集成实现稳定目标跟踪 |

### 3.5 3D 姿态估计

| 标题 | 作者 | 会议 | 一句话总结 |
|------|------|------|-----------|
| Semantics-aware Test-time Adaptation for 3D Human Pose Estimation | arXiv 2025 | arXiv 2025 | 语义感知的测试时自适应提升野外视频姿态估计 |
| Language-Driven 3D Human Pose Estimation in Multi-Person Scenes | ACM MM 2025 | ACM MM 2025 | 语言驱动的多人场景 3D 姿态估计 |
| SyncDiffPose: Multi-View 3D Human Pose Estimation with Weakly Synchronized Images | AAAI 2025 | AAAI 2025 | 弱同步图像的多视图姿态估计 |

---

## 4. 主流数据集和评估指标

### 4.1 常用数据集

| 数据集 | 类型 | 规模 | 特点 |
|--------|------|------|------|
| **AMASS** | 运动捕捉 | 40+ 小时 | 统一 SMPL 参数表示的大规模运动数据集 |
| **Human3.6M** | 室内姿态 | 3.6M 帧 | 经典室内 3D 姿态估计基准 |
| **3DPW** | 野外姿态 | 60K 帧 | 真实野外场景，含 IMU 数据 |
| **MPI-INF-3DHP** | 多场景姿态 | 1.3M 帧 | 室内+室外多场景 3D 姿态 |
| **TAP-Vid** | 点跟踪 | 多个子集 | 点跟踪基准测试集 |
| **GORP** | VR 运动 | 14+ 小时 | 首个真实 VR 稀疏输入数据集 |
| **Panoptic-L3D** | 语言-姿态 | 588 视频 | 语言驱动的 3D 姿态估计数据集 |

### 4.2 评估指标

#### 姿态估计指标
- **MPJPE** (Mean Per Joint Position Error): 预测关节与真实关节的欧氏距离
- **PA-MPJPE** (Procrustes-Aligned MPJPE): 经过普氏对齐后的 MPJPE
- **MPVPE** (Mean Per Vertex Position Error): 顶点位置平均误差
- **PCK** (Percentage of Correct Keypoints): 正确关键点百分比
- **AUC** (Area Under Curve): 正确率曲线下面积

#### 点跟踪指标
- **AJ** (Average Jaccard): 平均 Jaccard 相似度
- **OA** (Occlusion Accuracy): 遮挡预测准确率
- **δ_avg**: 平均位置精度

#### 运动生成指标
- **FID** (Fréchet Inception Distance): 特征分布距离
- **Diversity**: 生成运动的多样性
- **Multimodality**: 多模态性
- **Physical Plausibility**: 物理合理性

---

## 5. 趋势和开放问题

### 5.1 当前趋势

1. **扩散模型主导生成任务**
   - 扩散模型在运动生成任务中逐渐取代 VAE 和 GAN
   - 研究重点转向提高采样效率和可控性

2. **状态空间模型兴起**
   - Mamba 等线性复杂度模型开始挑战 Transformer
   - 在长序列建模中展现效率和性能优势

3. **稀疏输入成为主流**
   - 从密集传感器向稀疏 IMU/视觉传感器转变
   - 强调实用性和可穿戴性

4. **多模态融合**
   - 结合文本、音频、空间音频等多种模态
   - 语言驱动的运动生成受到关注

5. **自监督与伪标签**
   - 利用大规模无标注视频数据
   - 减少对手动标注的依赖

### 5.2 开放问题

1. **泛化能力**
   - 如何提高模型在野外场景的泛化能力？
   - 跨域适应和零样本迁移仍是挑战

2. **实时性与精度的平衡**
   - 如何在边缘设备上实现高精度实时跟踪？
   - 模型压缩与加速技术需求迫切

3. **物理合理性**
   - 生成的运动是否符合物理规律？
   - 如何有效集成物理约束

4. **长程一致性**
   - 如何保证长序列运动的时间一致性？
   - 误差累积问题亟待解决

5. **可解释性与可控性**
   - 如何提高模型的可解释性？
   - 细粒度控制运动风格和内容

6. **数据稀缺**
   - 高质量 3D 标注数据获取成本高
   - 需要更有效的数据增强和合成方法

### 5.3 未来方向

- **世界模型 (World Models)**: 结合物理仿真与深度学习
- **神经辐射场 (NeRF) 集成**: 与 3D 场景表示结合
- **大模型范式**: 探索运动领域的基础模型
- **具身智能 (Embodied AI)**: 与机器人控制深度结合
- **高效推理**: 面向移动和边缘设备的轻量级模型

---

## 6. 主要研究团队

| 团队/机构 | 代表工作 | 研究方向 |
|-----------|----------|----------|
| **Max Planck Institute (MPI)** | SMPL, AMASS, VIBE | 人体建模、运动捕捉 |
| **ETH Zurich (CVL/CGL)** | Ultra Inertial Poser | 稀疏传感器、物理仿真 |
| **MIT CSAIL** | Genesis, Human Motion Diffusion | 物理引擎、运动生成 |
| **Stanford (GLAMOR)** | MotionCLIP, T2M | 运动-语言模型 |
| **HKU (CGVU Lab)** | EMDM, TORE, Coverage Axis | 运动生成、几何处理 |
| **Tsinghua (HMM Lab)** | HMD-Poser, EgoLocate | 实时跟踪、XR 应用 |
| **CUHK** | 3D 人体重建、虚拟试衣 | 数字人、服装建模 |
| **Adobe Research** | CoTracker, TAPIR | 点跟踪、视频编辑 |
| **Meta Reality Labs** | Avatars Grow Legs | 虚拟化身、XR 跟踪 |
| **Google Research** | TAP-Vid, Kubric | 点跟踪基准、数据集 |

---

## 参考文献

1. Dwivedi et al. "TokenHMR: Advancing Human Mesh Recovery with a Tokenized Pose Representation." CVPR 2024.
2. Goel et al. "Humans in 4D: Reconstructing and Tracking Humans with Transformers." ICCV 2023.
3. Zhou et al. "EMDM: Efficient Motion Diffusion Model for Fast, High-Quality Human Motion Generation." ECCV 2024.
4. Karaev et al. "CoTracker3: Simpler and Better Point Tracking by Pseudo-labelling Real Videos." arXiv 2024.
5. Kim et al. "Learning to Track Any Points from Human Motion." arXiv 2025.
6. Gao et al. "Multiple Object Tracking as ID Prediction." arXiv 2024.
7. Mahmood et al. "AMASS: Archive of Motion Capture as Surface Shapes." ICCV 2019.
8. Yi et al. "Physical Inertial Poser (PIP): Physics-aware Real-time Human Motion Tracking." CVPR 2022.
9. Yi et al. "EgoLocate: Real-time Motion Capture, Localization, and Mapping." TOG 2023.
10. Tevet et al. "MotionCLIP: Exposing Human Motion Generation to CLIP Space." ECCV 2022.

---

*本文档由 AI 助手自动生成，基于 2024-2025 年最新公开研究成果整理。*
