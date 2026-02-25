# Motion Tracking 最新研究综述 (2024-2025)

> 调研日期: 2026-02-26  
> 调研范围: arXiv、CVPR 2025、ICCV 2025、SIGGRAPH 2025 等顶级会议  
> 重点关注: 2024-2025 年最新论文，特别是 2025 年新发表工作

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

| 方法 | 会议 | 核心贡献 | 代码/链接 |
|------|------|----------|-----------|
| **HiPART** | CVPR 2025 | 分层姿态自回归Transformer，解决遮挡3D姿态估计 | arXiv:2503.23331 |
| **ARGTrack** | CVPR 2025 | 自回归生成预训练，通过扩散模型生成未来帧外观 | - |
| **TokenHMR** | CVPR 2024 | 使用 Token 化姿态表示进行人体网格恢复 | - |
| **TORE** | ICCV 2023 | Token 缩减策略降低 Transformer 计算复杂度 | - |
| **MotionGPT** | arXiv 2023 | 将人体运动视为"外语"进行生成建模 | - |
| **PromptHMR** | CVPR 2025 | 可提示的人体网格恢复，支持空间和语义提示 | [GitHub](https://github.com/yufu-wang/PromptHMR) |

**HiPART (CVPR 2025)**  
- **论文**: https://arxiv.org/abs/2503.23331  
- **核心创新**: 提出分层姿态自回归Transformer，通过生成式稠密化方法从稀疏2D姿态生成分层2D稠密姿态，解决遮挡场景下的3D人体姿态估计问题  
- **优势**: 单帧方法性能超越多帧方法，参数量和计算复杂度更低

**PromptHMR (CVPR 2025)**  
- **论文**: https://arxiv.org/abs/2504.06397  
- **项目页**: https://yufu-wang.github.io/phmr-page/  
- **核心创新**: 首个可提示的人体姿态和形状(HPS)估计方法，支持边界框、掩码、语言描述等多种提示模态  
- **优势**: 在拥挤场景、人物交互等挑战性场景下表现鲁棒，达到SOTA性能

### 2.2 扩散模型 (Diffusion Models)

**核心思想**: 通过去噪扩散过程生成高质量运动序列

| 方法 | 会议 | 核心贡献 | 代码/链接 |
|------|------|----------|-----------|
| **EMDM** | ECCV 2024 | 高效运动扩散模型，实现快速高质量运动生成 | - |
| **MotionDiffuse** | TPAMI 2024 | 文本驱动的运动生成 | - |
| **PMDiff** | ACM MM 2024 | 基于 Mamba 状态空间模型的姿态扩散 | - |
| **DICE** | ICLR 2025 | 单图像手部-面部交互变形恢复 | - |
| **GaIP** | IJCAI 2025 | 服装感知扩散模型，从松散稀疏IMU传感器捕捉运动 | arXiv:2506.15290 |
| **Back to Basics** | arXiv 2025 | 系统研究运动表示对扩散模型的影响 | arXiv:2512.04499 |

**GaIP - Garment Inertial Poser (IJCAI 2025)**  
- **论文**: https://arxiv.org/abs/2506.15290  
- **项目页**: https://siplab.org/projects/GarmentInertialPoser  
- **核心创新**: 首个处理松散附着IMU传感器的运动捕捉方法，使用服装感知扩散模型  
- **优势**: 突破传统方法对传感器紧密附着的假设，更适用于真实世界场景

**Back to Basics (arXiv 2025)**  
- **论文**: https://arxiv.org/abs/2512.04499  
- **核心贡献**: 系统比较6种常见运动表示在扩散模型中的性能，提出v-loss预测目标  
- **发现**: 运动表示的选择对生成质量和多样性有显著影响

### 2.3 状态空间模型 (State Space Models / Mamba)

**核心思想**: 使用 Mamba 等线性复杂度序列模型替代 Transformer

| 方法 | 会议 | 核心贡献 | 代码/链接 |
|------|------|----------|-----------|
| **PMDiff** | ACM MM 2024 | 双向 Pose Mamba 去噪器实现序列建模 | - |
| **STGJMamer** | IMTAS 2025 | 图引导状态空间模型用于 3D 姿态估计 | - |
| **VMamba** | arXiv 2024 | 视觉状态空间模型用于视觉表示学习 | - |
| **PoseMamba** | AAAI 2025 | 纯SSM方法用于单目视频3D人体姿态估计 | arXiv:2408.03540 |
| **MeshMamba** | ICCV 2025 | 用于关节3D网格生成和重建的状态空间模型 | arXiv:2507.15212 |
| **PS-Mamba** | ICCV 2025 | 时空图Mamba用于姿态序列精修 | - |
| **SasMamba** | arXiv 2025 | 轻量级结构感知步长状态空间模型 | arXiv:2511.08872 |

**MeshMamba (ICCV 2025)**  
- **论文**: https://arxiv.org/abs/2507.15212  
- **核心创新**: 将Mamba状态空间模型应用于关节3D网格学习和生成  
- **优势**: 线性复杂度，适合处理长序列网格数据

**PoseMamba (AAAI 2025)**  
- **论文**: https://arxiv.org/abs/2408.03540  
- **核心创新**: 纯SSM-based方法，线性复杂度处理单目视频3D姿态估计  
- **优势**: 在保持性能的同时显著降低计算成本

### 2.4 稀疏传感器运动捕捉

**核心思想**: 从少量 IMU/视觉传感器恢复全身运动

| 方法 | 会议 | 核心贡献 | 代码/链接 |
|------|------|----------|-----------|
| **Ultra Inertial Poser** | SIGGRAPH 2024 | 结合 UWB 测距约束 IMU 漂移和抖动 | - |
| **HMD-Poser** | CVPR 2024 | VR 头显上的实时全身运动跟踪 | - |
| **PIP** | CVPR 2022 | 物理感知实时运动跟踪 | - |
| **EgoLocate** | TOG 2023 | 稀疏体戴传感器的实时运动捕捉与定位 | - |
| **GaIP** | IJCAI 2025 | 服装感知扩散模型处理松散IMU传感器 | arXiv:2506.15290 |
| **MagShield** | arXV 2025 | 磁场干扰下的鲁棒稀疏惯性运动捕捉 | arXiv:2506.22907 |

**GaIP (IJCAI 2025)**  
- **论文**: https://arxiv.org/abs/2506.15290  
- **核心创新**: 提出新的任务设定——使用稀疏、松散附着的IMU传感器进行全身姿态估计  
- **技术路线**: 模拟服装感知人体运动数据集生成IMU记录，使用Transformer-based扩散模型合成松散IMU数据并估计姿态

### 2.5 点跟踪 (Point Tracking)

**核心思想**: 跟踪视频中任意点的轨迹

| 方法 | 会议 | 核心贡献 | 代码/链接 |
|------|------|----------|-----------|
| **CoTracker3** | arXiv 2024 | 通过伪标签真实视频简化点跟踪 | - |
| **TAPIR** | ICCV 2023 | 每帧初始化 + 时序细化的点跟踪 | - |
| **BootsTAPIR** | ACCV 2024 | 自举训练实现任意点跟踪 | - |
| **AnthroTAP** | arXiv 2025 | 利用人体运动复杂性自动生成伪标签 | arXiv:2507.06233 |
| **AllTracker** | ICCV 2025 | 高分辨率高效稠密点跟踪 | arXiv:2506.07310 |
| **SpatialTrackerV2** | ICCV 2025 | 前馈3D点跟踪，统一场景几何、相机运动和像素运动 | arXiv:2507.12462 |
| **ProTracker** | arXiv 2025 | 概率集成实现鲁棒长程稠密跟踪 | - |
| **Chrono** | CVPR 2025 | 时间感知特征骨干网络用于点跟踪 | - |

**AnthroTAP (arXiv 2025)**  
- **论文**: https://arxiv.org/abs/2507.06233  
- **核心创新**: 自动化流水线从真实人体运动视频生成大规模伪标签点跟踪数据  
- **技术路线**: 拟合SMPL模型，投影网格顶点到图像平面，通过光线投射解决遮挡，使用光流一致性过滤不可靠轨迹  
- **性能**: 在TAP-Vid基准上达到SOTA，仅需4 GPU训练一天

**AllTracker (ICCV 2025)**  
- **论文**: https://arxiv.org/abs/2506.07310  
- **代码**: https://github.com/aharley/alltracker  
- **核心创新**: 通过估计查询帧与所有其他帧之间的流场来实现长程点跟踪  
- **优势**: 比其他类似模型更快更准确，同时在高分辨率下产生稠密输出

**SpatialTrackerV2 (ICCV 2025)**  
- **论文**: https://arxiv.org/abs/2507.12462  
- **代码**: https://github.com/henry123-boy/SpaTrackerV2  
- **Demo**: https://huggingface.co/spaces/henry123boy/SpaTracker  
- **核心创新**: 统一点跟踪、单目深度和相机姿态估计的内在联系，分解世界空间3D运动为场景几何、相机自运动和像素级物体运动  
- **性能**: 比现有3D跟踪方法提升30%，与领先的动态3D重建方法精度相当但速度快50倍

### 2.6 多目标跟踪 (MOT)

**核心思想**: 同时检测和跟踪多个目标

| 方法 | 会议 | 核心贡献 | 代码/链接 |
|------|------|----------|-----------|
| **MOTIP** | CVPR 2025 | 将 MOT 视为上下文 ID 预测任务 | arXiv:2403.16848 |
| **OmniTrack** | CVPR 2025 | 全景多目标跟踪处理 360° 图像 | - |
| **MITracker** | CVPR 2025 | 多视图集成用于视觉目标跟踪 | - |
| **CO-MOT** | ICLR 2025 | 端到端Transformer MOT的协同优化 | - |
| **FastTrackTr** | arXiv 2024 | 实时Transformer多目标跟踪 | arXiv:2411.15811 |
| **VeTrack** | Nature 2025 | 基于Transformer外观特征的车辆MOT | - |

**MOTIP (CVPR 2025)**  
- **论文**: https://arxiv.org/abs/2403.16848  
- **代码**: https://github.com/MCG-NJU/MOTIP  
- **核心创新**: 创新性地将多目标跟踪中的目标关联任务看作上下文ID预测问题  
- **优势**: 避免传统方法中人工设计的启发式规则，更适应复杂场景

**OmniTrack (CVPR 2025)**  
- **论文**: http://openaccess.thecvf.com/content/CVPR2025/papers/Luo_Omnidirectional_Multi-Object_Tracking_CVPR_2025_paper.pdf  
- **核心创新**: 首个全景图像多目标跟踪框架，处理360°视野  
- **数据集**: 提出QuadTrack数据集，包含复杂运动动态

### 2.7 3D 人体网格恢复 (HMR)

| 方法 | 会议 | 核心贡献 | 代码/链接 |
|------|------|----------|-----------|
| **TokenHMR** | CVPR 2024 | Token化姿态表示进行人体网格恢复 | - |
| **PromptHMR** | CVPR 2025 | 可提示的人体网格恢复 | arXiv:2504.06397 |
| **BLADE** | CVPR 2025 | 通过精确深度估计的单视图人体网格估计 | - |
| **MEGA** | CVPR 2025 | 掩码生成自编码器用于人体网格恢复 | - |
| **Biomech-HMR** | CVPR 2025 | 使用生物力学精确骨骼模型重建人体 | - |
| **Age-Inclusive HMR** | arXiv 2025 | 面向全年龄段的动作识别人体网格恢复 | arXiv:2512.05259 |

**BLADE (CVPR 2025)**  
- **论文**: https://openaccess.thecvf.com/content/CVPR2025/papers/Wang_BLADE_Single-view_Body_Mesh_Estimation_through_Accurate_Depth_Estimation_CVPR_2025_paper.pdf  
- **核心创新**: 通过精确深度估计解决单图像人体网格恢复的病态问题  
- **技术路线**: 同时估计身体形状、姿态和相机参数

**MEGA (CVPR 2025)**  
- **论文**: https://openaccess.thecvf.com/content/CVPR2025/papers/Oh_Masked_Generative_Autoencoder_for_Human_Mesh_Recovery_CVPR_2025_paper.pdf  
- **核心创新**: 掩码生成自编码器，从图像和部分人体网格token序列恢复人体网格

### 2.8 手部跟踪与重建

| 方法 | 会议 | 核心贡献 | 代码/链接 |
|------|------|----------|-----------|
| **WiLoR** | CVPR 2025 | 端到端3D手部定位和重建 | arXiv:2409.12259 |
| **HandOS** | CVPR 2025 | 单阶段3D手部重建 | - |
| **HaWoR** | CVPR 2025 | 从第一人称视频重建世界空间手部运动 | arXiv:2501.02973 |
| **Dyn-HaMR** | CVPR 2025 | 从动态相机恢复4D交互手部运动 | - |
| **MagicHOI** | ICCV 2025 | 利用3D先验实现短序列手物重建 | - |

**WiLoR (CVPR 2025)**  
- **论文**: https://arxiv.org/abs/2409.12259  
- **项目页**: https://rolpotamias.github.io/WiLoR/  
- **核心创新**: 野外多手重建的数据驱动流水线，包含实时检测定位和重建两个组件  
- **优势**: 高效的多手重建，适用于野外场景

**HaWoR (CVPR 2025 Highlight)**  
- **论文**: https://arxiv.org/abs/2501.02973  
- **代码**: https://github.com/ThunderVVV/HaWoR  
- **核心创新**: 高保真地从第一人称视频重建世界坐标系中的手部运动  
- **技术路线**: 解耦相机运动对手部运动估计的影响

### 2.9 高斯溅射 (Gaussian Splatting) 在运动跟踪中的应用

| 方法 | 会议 | 核心贡献 | 代码/链接 |
|------|------|----------|-----------|
| **GST** | CVPR 2025 Workshop | 结合3D人体姿态估计与3D高斯溅射 | arXiv:2409.04196 |
| **GEM** | CVPR 2025 | 高斯特征模型用于头部化身 | arXiv:2407.04545 |
| **EventSplat** | CVPR 2025 | 从事件相机数据进行高斯溅射 | - |
| **RGBAvatar** | CVPR 2025 | 简化高斯Blendshapes实现在线头部化身 | - |
| **Humangaussian** | CVPR 2024 | 文本驱动的3D人体生成与高斯溅射 | - |

**GEM - Gaussian Eigen Models (CVPR 2025)**  
- **论文**: https://arxiv.org/abs/2407.04545  
- **核心创新**: 将3D高斯头部化身表示为无网络形式的特征基集合  
- **优势**: 高质量、轻量级、易于控制的头部化身

### 2.10 基础模型 (Foundation Models) 用于姿态估计

| 方法 | 会议 | 核心贡献 | 代码/链接 |
|------|------|----------|-----------|
| **OPFormer** | arXiv 2025 | 利用基础模型进行物体姿态估计 | arXiv:2511.12614 |
| **FoundationStereo** | arXiv 2025 | 立体匹配基础模型 | arXiv:2501.09898 |
| **FEEPE** | arXiv 2025 | 基础特征驱动的在线末端执行器姿态估计 | arXiv:2503.14051 |
| **Geo6DPose** | arXiv 2025 | 快速零样本6D物体姿态估计 | arXiv:2512.10674 |
| **Depth-Anything V3** | 2025 | 字节跳动发布的深度估计基础模型 | [GitHub](https://github.com/ByteDance-Seed/Depth-Anything-3) |

### 2.11 通用运动模型 (Generalist Models)

**GENMO (ICCV 2025)**  
- **论文**: https://arxiv.org/abs/2505.01425  
- **项目页**: https://research.nvidia.com/labs/dair/genmo/  
- **代码**: https://github.com/NVlabs/GENMO  
- **核心创新**: NVIDIA提出的统一通用人体运动模型，在单一框架中桥接运动估计和生成  
- **支持条件**: 视频、关键点、文本、音乐等多种输入模态  
- **优势**: 一个模型处理多种运动任务，包括运动生成、估计、补全、编辑等

---

## 3. 重要论文列表 (2025年最新)

### 3.1 人体姿态估计与运动生成

| 标题 | 作者 | 会议 | 一句话总结 | 链接 |
|------|------|------|-----------|------|
| HiPART: Hierarchical Pose AutoRegressive Transformer for Occluded 3D Human Pose Estimation | Zheng et al. | CVPR 2025 | 分层姿态自回归Transformer解决遮挡3D姿态估计 | arXiv:2503.23331 |
| PromptHMR: Promptable Human Mesh Recovery | Wang et al. | CVPR 2025 | 可提示的人体网格恢复，支持多种提示模态 | arXiv:2504.06397 |
| Back to Basics: Motion Representation Matters for Human Motion Generation Using Diffusion Model | Jin et al. | arXiv 2025 | 系统研究运动表示对扩散模型的影响 | arXiv:2512.04499 |
| GENMO: A GENeralist Model for Human MOtion | Li et al. | ICCV 2025 | 统一通用人体运动模型，支持多种任务和条件 | arXiv:2505.01425 |
| EMDM: Efficient Motion Diffusion Model for Fast, High-Quality Human Motion Generation | Zhou et al. | ECCV 2024 | 高效运动扩散模型实现快速高质量运动生成 | - |
| PMDiff: Towards Accurate and Smooth Human Motion Tracking | Dong et al. | ACM MM 2024 | 基于Mamba的扩散模型实现准确平滑的运动跟踪 | - |

### 3.2 稀疏传感器与实时跟踪

| 标题 | 作者 | 会议 | 一句话总结 | 链接 |
|------|------|------|-----------|------|
| Human Motion Capture from Loose and Sparse Inertial Sensors with Garment-aware Diffusion Models | Ilic et al. | IJCAI 2025 | 服装感知扩散模型处理松散稀疏IMU传感器 | arXiv:2506.15290 |
| Improving Sparse IMU-based Motion Capture with Motion Label Smoothing | - | arXiv 2025 | 运动标签平滑改进稀疏IMU运动捕捉 | arXiv:2511.22288 |
| MagShield: Towards Better Robustness in Sparse Inertial Motion Capture Under Magnetic Disturbances | - | arXiv 2025 | 磁场干扰下的鲁棒稀疏惯性运动捕捉 | arXiv:2506.22907 |
| Ultra Inertial Poser: Scalable Motion Capture and Tracking | ETH SIPLab | SIGGRAPH 2024 | 结合UWB和IMU实现可扩展的运动捕捉 | - |
| HMD-Poser: On-Device Real-time Human Motion Tracking | PICO AI Team | CVPR 2024 | VR头显端实时全身运动跟踪 | - |

### 3.3 点跟踪与视觉跟踪

| 标题 | 作者 | 会议 | 一句话总结 | 链接 |
|------|------|------|-----------|------|
| AnthroTAP: Learning Point Tracking with Real-World Motion | Kim et al. | arXiv 2025 | 利用人体运动复杂性训练鲁棒点跟踪器 | arXiv:2507.06233 |
| AllTracker: Efficient Dense Point Tracking at High Resolution | Harley et al. | ICCV 2025 | 高分辨率高效稠密点跟踪 | arXiv:2506.07310 |
| SpatialTrackerV2: 3D Point Tracking Made Easy | Xiao et al. | ICCV 2025 | 前馈3D点跟踪，统一几何和运动估计 | arXiv:2507.12462 |
| CoTracker3: Simpler and Better Point Tracking by Pseudo-labelling Real Videos | Karaev et al. | arXiv 2024 | 通过伪标签简化并改进点跟踪 | - |
| TAPTR: Tracking Any Point with Transformers as Detection | Li et al. | ECCV 2024 | 将点跟踪视为检测任务的Transformer方法 | - |
| LocoTrack: Local All-Pair Correspondence for Point Tracking | Cho et al. | ECCV 2024 | 局部全对应对应关系实现点跟踪 | - |
| ProTracker: Probabilistic Integration for Robust and Accurate Long-term Dense Tracking | - | arXiv 2025 | 概率集成实现鲁棒长程稠密跟踪 | - |
| Chrono: Exploring Temporally-Aware Features for Point Tracking | - | CVPR 2025 | 时间感知特征骨干网络用于点跟踪 | - |

### 3.4 多目标跟踪

| 标题 | 作者 | 会议 | 一句话总结 | 链接 |
|------|------|------|-----------|------|
| Multiple Object Tracking as ID Prediction | Gao et al. | CVPR 2025 | 将多目标跟踪重新定义为ID预测任务 | arXiv:2403.16848 |
| OmniTrack: Omnidirectional Multi-Object Tracking | Luo et al. | CVPR 2025 | 全景图像的多目标跟踪框架 | - |
| MITracker: Multi-View Integration for Visual Object Tracking | - | CVPR 2025 | 多视图集成实现稳定目标跟踪 | - |
| CO-MOT: Boosting End-to-End Transformer Multi-Object Tracking | - | ICLR 2025 | 端到端Transformer MOT的协同优化 | - |
| FastTrackTr: Real-time Multi-Object Tracking with Transformer | - | arXiv 2024 | 实时Transformer多目标跟踪 | arXiv:2411.15811 |

### 3.5 3D 姿态估计与网格恢复

| 标题 | 作者 | 会议 | 一句话总结 | 链接 |
|------|------|------|-----------|------|
| BLADE: Single-view Body Mesh Estimation through Accurate Depth Estimation | Wang et al. | CVPR 2025 | 通过精确深度估计的单视图人体网格估计 | - |
| MEGA: Masked Generative Autoencoder for Human Mesh Recovery | Oh et al. | CVPR 2025 | 掩码生成自编码器用于人体网格恢复 | - |
| Reconstructing Humans with a Biomechanically Accurate Skeleton Model | - | CVPR 2025 | 使用生物力学精确骨骼模型重建人体 | - |
| A Neural Optimizer for Multiview Human Mesh Recovery | - | CVPR 2025 | 用于多视图人体网格恢复的神经优化器 | - |
| Age-Inclusive 3D Human Mesh Recovery for Action Recognition | - | arXiv 2025 | 面向全年龄段的动作识别人体网格恢复 | arXiv:2512.05259 |
| Semantics-aware Test-time Adaptation for 3D Human Pose Estimation | - | arXiv 2025 | 语义感知的测试时自适应提升野外视频姿态估计 | - |
| SyncDiffPose: Multi-View 3D Human Pose Estimation with Weakly Synchronized Images | - | AAAI 2025 | 弱同步图像的多视图姿态估计 | - |

### 3.6 手部跟踪

| 标题 | 作者 | 会议 | 一句话总结 | 链接 |
|------|------|------|-----------|------|
| WiLoR: End-to-end 3D Hand Localization and Reconstruction in the Wild | Potamias et al. | CVPR 2025 | 野外端到端3D手部定位和重建 | arXiv:2409.12259 |
| HaWoR: World-Space Hand Motion Reconstruction from Egocentric Videos | Zhang et al. | CVPR 2025 | 从第一人称视频重建世界空间手部运动 | arXiv:2501.02973 |
| HandOS: 3D Hand Reconstruction in One Stage | Chen et al. | CVPR 2025 | 单阶段3D手部重建 | - |
| Dyn-HaMR: Recovering 4D Interacting Hand Motion from a Dynamic Camera | - | CVPR 2025 | 从动态相机恢复4D交互手部运动 | - |
| How Do I Do That? Synthesizing 3D Hand Motion and Contact Maps | - | CVPR 2025 | 合成3D手部运动和接触图 | - |
| Hand-held Object Reconstruction from RGB Video | - | CVPR 2025 | 从RGB视频重建手持物体 | - |
| MagicHOI: Leveraging 3D Priors for Accurate Hand-object Reconstruction | Wang et al. | ICCV 2025 | 利用3D先验实现手物重建 | - |

### 3.7 状态空间模型 (Mamba)

| 标题 | 作者 | 会议 | 一句话总结 | 链接 |
|------|------|------|-----------|------|
| MeshMamba: State Space Models for Articulated 3D Mesh Generation and Reconstruction | Yoshiyasu et al. | ICCV 2025 | 用于关节3D网格生成和重建的状态空间模型 | arXiv:2507.15212 |
| PS-Mamba: Spatial-Temporal Graph Mamba for Pose Sequence Refinement | Dong et al. | ICCV 2025 | 时空图Mamba用于姿态序列精修 | - |
| PoseMamba: Monocular 3D Human Pose Estimation with Bidirectional Global-Local Mamba | - | AAAI 2025 | 双向全局-局部Mamba用于单目3D姿态估计 | arXiv:2408.03540 |
| SasMamba: A Lightweight Structure-Aware Stride State Space Model for 3D Human Pose Estimation | - | arXiv 2025 | 轻量级结构感知步长状态空间模型 | arXiv:2511.08872 |
| Mamba-Driven Topology Fusion for Monocular 3D Human Pose Estimation | - | arXiv 2025 | Mamba驱动的拓扑融合用于单目3D姿态估计 | arXiv:2505.20611 |

### 3.8 高斯溅射

| 标题 | 作者 | 会议 | 一句话总结 | 链接 |
|------|------|------|-----------|------|
| Gaussian Eigen Models for Human Heads | Zielonka et al. | CVPR 2025 | 高斯特征模型用于头部化身 | arXiv:2407.04545 |
| GST: Precise 3D Human Body from a Single Image with Gaussian Splatting | - | CVPR 2025 Workshop | 结合3D人体姿态估计与高斯溅射 | arXiv:2409.04196 |
| RGBAvatar: Reduced Gaussian Blendshapes for Online Head Avatar | - | CVPR 2025 | 简化高斯Blendshapes实现在线头部化身 | - |
| EventSplat: 3D Gaussian Splatting from Moving Event Cameras | - | CVPR 2025 | 从事件相机进行高斯溅射 | - |

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
| **QuadTrack** | 全景MOT | - | CVPR 2025提出的全景多目标跟踪数据集 |

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

### 5.1 2025年关键趋势

1. **扩散模型主导生成任务**
   - 扩散模型在运动生成任务中逐渐取代 VAE 和 GAN
   - 研究重点转向提高采样效率和可控性
   - **新进展**: GaIP将扩散模型应用于稀疏传感器运动捕捉，Back to Basics系统研究运动表示的影响

2. **状态空间模型 (Mamba) 兴起**
   - Mamba 等线性复杂度模型开始挑战 Transformer
   - 在长序列建模中展现效率和性能优势
   - **新进展**: MeshMamba(ICCV 2025)、PS-Mamba(ICCV 2025)、PoseMamba(AAAI 2025)等多个工作将Mamba应用于姿态估计和网格重建

3. **稀疏输入成为主流**
   - 从密集传感器向稀疏 IMU/视觉传感器转变
   - 强调实用性和可穿戴性
   - **新进展**: GaIP(IJCAI 2025)首次处理松散附着的IMU传感器，MagShield处理磁场干扰

4. **多模态融合**
   - 结合文本、音频、空间音频等多种模态
   - 语言驱动的运动生成受到关注
   - **新进展**: GENMO(ICCV 2025)统一处理视频、关键点、文本、音乐等多种输入；PromptHMR(CVPR 2025)支持空间和语义提示

5. **自监督与伪标签**
   - 利用大规模无标注视频数据
   - 减少对手动标注的依赖
   - **新进展**: AnthroTAP(arXiv 2025)利用人体运动自动生成点跟踪伪标签

6. **通用/基础模型趋势**
   - 从专用模型向通用模型转变
   - **新进展**: GENMO(ICCV 2025)作为首个通用人体运动模型，统一处理多种任务

7. **3D点跟踪突破**
   - 从2D点跟踪向3D点跟踪发展
   - **新进展**: SpatialTrackerV2(ICCV 2025)统一场景几何、相机运动和像素运动，速度提升50倍

8. **高斯溅射与人体建模结合**
   - 3D Gaussian Splatting在头部/人体化身中的应用
   - **新进展**: GEM(CVPR 2025)高斯特征模型用于头部化身

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

7. **松散传感器配置**
   - 真实场景中传感器往往无法紧密附着
   - 服装、皮肤滑动等因素影响精度

### 5.3 未来方向

- **世界模型 (World Models)**: 结合物理仿真与深度学习
- **神经辐射场 (NeRF) 集成**: 与 3D 场景表示结合
- **大模型范式**: 探索运动领域的基础模型 (如GENMO)
- **具身智能 (Embodied AI)**: 与机器人控制深度结合
- **高效推理**: 面向移动和边缘设备的轻量级模型
- **多模态统一**: 统一处理视觉、语言、音频等多种模态
- **3D高斯溅射**: 在动态人体建模和跟踪中的更广泛应用

---

## 6. 主要研究团队

| 团队/机构 | 代表工作 | 研究方向 |
|-----------|----------|----------|
| **Max Planck Institute (MPI)** | SMPL, AMASS, VIBE, PromptHMR | 人体建模、运动捕捉 |
| **ETH Zurich (CVL/CGL)** | Ultra Inertial Poser, GaIP | 稀疏传感器、物理仿真 |
| **MIT CSAIL** | Genesis, Human Motion Diffusion | 物理引擎、运动生成 |
| **Stanford (GLAMOR)** | MotionCLIP, T2M | 运动-语言模型 |
| **HKU (CGVU Lab)** | EMDM, TORE, Coverage Axis | 运动生成、几何处理 |
| **Tsinghua (HMM Lab)** | HMD-Poser, EgoLocate | 实时跟踪、XR 应用 |
| **CUHK** | 3D 人体重建、虚拟试衣 | 数字人、服装建模 |
| **Adobe Research** | CoTracker, TAPIR | 点跟踪、视频编辑 |
| **Meta Reality Labs** | Avatars Grow Legs | 虚拟化身、XR 跟踪 |
| **Google Research** | TAP-Vid, Kubric | 点跟踪基准、数据集 |
| **NVIDIA Research** | GENMO | 通用运动模型 |
| **SJTU** | HiPART, MOTIP | 姿态估计、多目标跟踪 |
| **Zhejiang University** | SpatialTrackerV2 | 3D点跟踪 |

---

## 7. 代码仓库汇总

| 项目 | 链接 | 描述 |
|------|------|------|
| PromptHMR | https://github.com/yufu-wang/PromptHMR | 可提示的人体网格恢复 |
| GENMO | https://github.com/NVlabs/GENMO | NVIDIA通用人体运动模型 |
| MOTIP | https://github.com/MCG-NJU/MOTIP | 多目标跟踪作为ID预测 |
| SpatialTrackerV2 | https://github.com/henry123-boy/SpaTrackerV2 | 3D点跟踪 |
| HaWoR | https://github.com/ThunderVVV/HaWoR | 世界空间手部运动重建 |
| AllTracker | https://github.com/aharley/alltracker | 高分辨率稠密点跟踪 |
| WiLoR | https://github.com/rolpotamias/WiLoR | 野外3D手部重建 |
| Depth-Anything V3 | https://github.com/ByteDance-Seed/Depth-Anything-3 | 字节跳动深度估计基础模型 |

---

## 参考文献

1. Zheng et al. "HiPART: Hierarchical Pose AutoRegressive Transformer for Occluded 3D Human Pose Estimation." CVPR 2025.
2. Wang et al. "PromptHMR: Promptable Human Mesh Recovery." CVPR 2025.
3. Kim et al. "AnthroTAP: Learning Point Tracking with Real-World Motion." arXiv 2025.
4. Xiao et al. "SpatialTrackerV2: 3D Point Tracking Made Easy." ICCV 2025.
5. Harley et al. "AllTracker: Efficient Dense Point Tracking at High Resolution." ICCV 2025.
6. Li et al. "GENMO: A GENeralist Model for Human MOtion." ICCV 2025.
7. Ilic et al. "Human Motion Capture from Loose and Sparse Inertial Sensors with Garment-aware Diffusion Models." IJCAI 2025.
8. Gao et al. "Multiple Object Tracking as ID Prediction." CVPR 2025.
9. Jin et al. "Back to Basics: Motion Representation Matters for Human Motion Generation Using Diffusion Model." arXiv 2025.
10. Yoshiyasu et al. "MeshMamba: State Space Models for Articulated 3D Mesh Generation and Reconstruction." ICCV 2025.
11. Zhang et al. "HaWoR: World-Space Hand Motion Reconstruction from Egocentric Videos." CVPR 2025.
12. Zielonka et al. "Gaussian Eigen Models for Human Heads." CVPR 2025.
13. Dwivedi et al. "TokenHMR: Advancing Human Mesh Recovery with a Tokenized Pose Representation." CVPR 2024.
14. Zhou et al. "EMDM: Efficient Motion Diffusion Model for Fast, High-Quality Human Motion Generation." ECCV 2024.
15. Karaev et al. "CoTracker3: Simpler and Better Point Tracking by Pseudo-labelling Real Videos." arXiv 2024.

---

*本文档由 AI 助手自动生成，基于 2024-2025 年最新公开研究成果整理。更新时间: 2026-02-26*
