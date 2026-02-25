# VLA (Vision-Language-Action) 模型综述 (2025 最新版)

> 涵盖 RT-1 到 OpenVLA、π0、GR00T N1 等最新模型的技术演进、代表性工作对比及 2025 年最新进展

---

## 1. 领域概述

**Vision-Language-Action (VLA)** 模型是具身智能领域的核心方向，旨在将视觉感知、语言理解和机器人动作控制统一到一个端到端框架中。

### 核心思想
- 利用大规模视觉-语言模型 (VLM) 的预训练知识
- 通过机器人动作数据微调，实现语言条件的机器人控制
- 目标是让机器人能够理解自然语言指令并在真实环境中执行

### 发展时间线

| 时间 | 里程碑 | 关键贡献 |
|------|--------|----------|
| 2022.12 | RT-1 | 首个大规模机器人 Transformer |
| 2023.07 | RT-2 | 引入 VLM 作为骨干网络 |
| 2023.10 | RT-X | 跨机器人平台的泛化 |
| 2024.06 | OpenVLA | 最大规模开源 VLA (7B) |
| 2024.08 | RDT-1B | 扩散模型 + 双臂操作 |
| 2024.10 | π0 | 流匹配 + 高效推理 |
| **2025.03** | **GR00T N1** | **NVIDIA 开源人形机器人基础模型** |
| **2025.06** | **BitVLA** | **首个 1-bit 量化 VLA** |
| **2025.07** | **Spec-VLA** | **投机解码加速 VLA 推理** |
| **2025.09** | **LLaDA-VLA** | **首个扩散 VLM 的 VLA** |
| **2025.09** | **RDT-2** | **零样本跨本体泛化** |

---

## 2. 技术路线分类

### 2.1 基于 VLM 微调的 VLA

**核心方法**：冻结或微调预训练 VLM，添加动作预测头

| 模型 | 机构 | 参数 | 特点 |
|------|------|------|------|
| **RT-2** | Google DeepMind | 55B | PaLI-X 骨干，端到端训练 |
| **OpenVLA** | Stanford/UC Berkeley | 7B | 最大开源模型，970k 演示数据 |
| **CogACT** | Microsoft | 7B | CogVLM + 动作预测 |
| **GR00T N1** | NVIDIA | 2B-3B | 双系统架构 (VLM + DiT)，人形机器人专用 |

**优势**：
- 充分利用 VLM 的语义理解能力
- 零样本泛化到新任务

**局限**：
- 推理速度慢 (~1 Hz)
- 计算资源需求大

### 2.2 基于扩散模型的 VLA

**核心方法**：将动作生成建模为去噪扩散过程

| 模型 | 机构 | 参数 | 特点 |
|------|------|------|------|
| **RDT-1B** | 清华 | 1B | 双臂操作，百万级数据预训练 |
| **RDT-2** | 清华 | 1B+ | **零样本跨本体泛化**，残差 VQ 动作 token |
| **Octo** | Berkeley/Stanford | 93M | 开源通用机器人策略 |
| **π0** | Physical Intelligence | - | 流匹配，实时推理，50Hz 高频控制 |
| **LLaDA-VLA** | 中科大/南大 | - | **首个基于扩散 VLM 的 VLA** |

**优势**：
- 多模态动作分布建模
- 支持复杂接触交互

**局限**：
- 采样步数影响推理速度
- 训练稳定性挑战

### 2.3 基于 Transformer 的端到端控制

**核心方法**：纯 Transformer 架构，直接映射视觉+语言→动作

| 模型 | 机构 | 特点 |
|------|------|------|
| **RT-1** | Google DeepMind | FiLM 条件化，高效推理 |
| **RT-1-X** | Google DeepMind | RT-X 系列，跨机器人数据 |
| **Gato** | DeepMind | 通用多任务代理 |

### 2.4 分层任务规划 + 底层控制

**核心方法**：高层 VLM 规划子任务，低层 VLA 执行

| 模型 | 特点 |
|------|------|
| **SayCan** | LLM 规划 + 可执行性评分 |
| **Inner Monologue** | 闭环重规划 |
| **VoxPoser** | 从语言生成 3D 价值图 |
| **GR00T N1** | System 2 (VLM) + System 1 (DiT) 双系统 |

---

## 3. 2025 年重要新模型详解

### 3.1 NVIDIA GR00T N1 (2025.03)

**首个开源人形机器人基础模型**，采用双系统架构：

- **System 2 (视觉-语言模块)**：基于 Eagle-2.5 VLM，负责环境理解和推理
- **System 1 (扩散 Transformer)**：基于流匹配 (Flow Matching) 的 DiT，实时生成动作

**技术亮点**：
- 端到端联合训练
- 异构数据混合训练：真实机器人轨迹 + 人类视频 + 合成数据
- 在 Fourier GR-1 人形机器人上部署验证

**性能**：
- 在标准仿真基准上超越 SOTA 模仿学习方法
- 高数据效率的语言条件双臂操作

### 3.2 BitVLA (2025.06)

**首个 1-bit 量化 VLA 模型**，针对资源受限的边缘设备：

- 三值参数 {-1, 0, 1}
- 蒸馏感知训练策略，将全精度视觉编码器压缩至 1.58-bit
- 在 LIBERO 基准上达到与 OpenVLA-OFT (4-bit 量化) 相当的性能

**效率提升**：
- 内存占用仅为 OpenVLA-OFT 的 **29.8%**
- 适合边缘设备部署

### 3.3 Spec-VLA (2025.07)

**首个针对 VLA 的投机解码框架**：

- 利用动作 token 的相对距离设计放松接受机制
- 增强接受长度 **44%**
- 相比 OpenVLA 基线实现 **1.42 倍加速**，不降低成功率

**技术贡献**：
- 将 LLM 投机解码技术成功应用于 VLA
- 为 VLA 推理加速开辟新方向

### 3.4 LLaDA-VLA (2025.09)

**首个基于扩散视觉-语言模型 (d-VLM) 的 VLA**：

- 基于 LLaDA (大语言扩散模型) 构建
- 局部特殊 token 分类策略替代全词汇分类
- 分层动作结构化解码策略

**性能**：
- 在仿真和真实机器人上显著超越 SOTA VLA
- 展示了扩散模型在机器人策略学习中的潜力

### 3.5 RDT-2 (2025.09)

**RDT-1B 的继任者，首个实现零样本跨本体泛化的基础模型**：

- 残差 VQ (Residual VQ) 动作 token 化
- 仅需 5 步扩散去噪即可生成连续动作
- 在未见本体上实现简单开放词汇任务的零样本部署

**版本**：
- **RDT2-VQ**：自回归 VLA 模型
- **RDT2-FM**：基于流匹配的动作专家模型

---

## 4. 重要模型详细对比

### 4.1 Google RT 系列

```
RT-1 (2022) → RT-2 (2023) → RT-X (2023) → RT-H (2024)
```

| 特性 | RT-1 | RT-2 | RT-X |
|------|------|------|------|
| 骨干网络 | EfficientNet-B3 | PaLI-X (55B) | RT-1 / RT-2 |
| 语言编码 | Universal Sentence Encoder | 内置 VLM | 内置 VLM |
| 训练数据 | 130k 演示 | 同 RT-1 + Web 数据 | 跨 22 种机器人 |
| 推理速度 | ~3 Hz | ~1 Hz | ~1-3 Hz |
| 泛化能力 | 有限 | 强（语义+视觉） | 跨机器人 |

**RT-2 关键创新**：
- 将机器人动作表示为文本 token（如 "pos_x pos_y pos_z rot_x rot_y rot_z gripper"）
- 联合训练 Web 数据和机器人数据
- 涌现能力：符号理解、推理、人类识别

### 4.2 2025 年开源模型对比

| 模型 | 参数 | 骨干 | 开源数据 | 推理速度 | 特点 |
|------|------|------|----------|----------|------|
| **OpenVLA** | 7B | Llama 2 + DINOv2 | 970k | ~5-15 Hz | 最大开源 |
| **Octo** | 93M | Transformer | 800k | ~5-15 Hz | 轻量高效 |
| **RDT-1B** | 1B | Diffusion Transformer | 1M+ | ~5-10 Hz | 双臂操作 |
| **RDT-2** | 1B+ | Diffusion Transformer | 1M+ | ~5-10 Hz | 零样本跨本体 |
| **π0** | - | Flow Matching | - | ~50 Hz | 高频实时 |
| **GR00T N1** | 2B-3B | VLM + DiT | 混合 | ~10-20 Hz | 人形专用 |
| **BitVLA** | 7B (1-bit) | Llama 2 + DINOv2 | 970k | ~10-20 Hz | 极致压缩 |
| **LLaDA-VLA** | - | d-VLM | - | ~5-10 Hz | 扩散 VLM |

---

## 5. 高效 VLA 技术 (2025 综述)

根据 2025 年 10 月发表的《A Survey on Efficient Vision-Language-Action Models》，高效 VLA 技术可分为三大支柱：

### 5.1 高效模型设计

| 技术方向 | 代表工作 | 核心思想 |
|----------|----------|----------|
| **架构优化** | Long-VLA | 将二次 Transformer 转换为线性注意力 |
| **模型压缩** | BitVLA | 1-bit/三值量化 |
| **超网络** | HyperVLA | 使用超网络生成权重，减少推理成本 |
| **小型 VLA** | TinyVLA | 紧凑模型设计，快速推理 |

### 5.2 高效训练

| 技术方向 | 代表工作 | 核心思想 |
|----------|----------|----------|
| **数据蒸馏** | FT-NCFM | 影响感知数据蒸馏 |
| **课程学习** | - | 渐进式难度训练 |
| **多任务学习** | - | 共享表示，减少重复训练 |

### 5.3 高效推理

| 技术方向 | 代表工作 | 加速比 | 特点 |
|----------|----------|--------|------|
| **投机解码** | Spec-VLA | 1.42x | 放松接受机制 |
| **量化推理** | BitVLA | 3.35x 内存节省 | 1-bit 权重 |
| **Token 复用** | - | - | 缓存重复动作 token |

---

## 6. 安全与可靠性 (2025 新进展)

### 6.1 SafeVLA (NeurIPS 2025 Spotlight)

**首个系统性的 VLA 安全对齐框架**：

- **集成安全方法 (ISA)**：系统建模安全需求
- **主动诱发不安全行为**：识别潜在风险
- **安全强化学习约束**：通过 CMDP 优化
- **严格安全评估**：针对长尾风险

**效果**：
- 安全违规累计成本降低 **83.58%**
- 任务成功率提升 **3.85%**
- 对分布外扰动具有鲁棒性

### 6.2 SAFE (NeurIPS 2025)

**多任务故障检测器**：

- 分析 VLA 特征空间
- 发现 VLA 具有足够的内部信息用于故障检测
- 可检测未见任务的故障

### 6.3 FPC-VLA

**故障预测与纠正框架**：

- 双模型架构：VLA + 监督器
- 预测潜在故障并主动纠正

---

## 7. 移动操作与长程任务 (2025 新进展)

### 7.1 MoManipVLA (CVPR 2025)

**通用移动操作 VLA 迁移框架**：

- 将固定基座操作 VLA 迁移到移动操作
- 紧密集成导航与操作
- 跨任务和环境的强泛化能力

### 7.2 EchoVLA

**面向长程移动操作的记忆感知 VLA**：

- **双重声明式记忆机制**：
  - 旁海马皮层 (PHC)：处理空间结构（场景记忆）
  - 海马体：处理情景经历（情景记忆）
- 赋予机器人"连续的意识"

### 7.3 AuxVLA

**辅助任务学习 + 多模态提示**：

- 成功将现有 VLA 迁移到移动操作
- 使用辅助任务增强表示学习

---

## 8. 主流数据集与数据扩展趋势

### 8.1 大规模机器人数据集

| 数据集 | 规模 | 机器人 | 特点 |
|--------|------|--------|------|
| **Open X-Embodiment** | 1M+ | 22 种 | 跨机器人、跨任务 |
| **BridgeData V2** | 60k | WidowX | 单臂操作 |
| **ALOHA** | 500+ | ALOHA | 双臂精细操作 |
| **RH20T** | 110k | 多种 | 人类演示视频 |
| **DROID** | 76k | Franka | 多样化场景 |
| **GR00T N1 训练集** | 混合 | 人形 | 真实 + 视频 + 合成 |

### 8.2 2025 数据扩展趋势

1. **异构数据融合**：真实机器人轨迹 + 人类视频 + 合成数据
2. **跨本体数据共享**：统一动作空间表示
3. **视频预训练**：利用互联网视频学习物理常识
4. **仿真到真实**：大规模仿真数据 + 域随机化

---

## 9. 应用场景与商业部署

### 9.1 应用场景

| 场景 | 代表工作 | 进展 |
|------|----------|------|
| **双臂操作** | RDT-1B/2, ALOHA | 精细协调操作 |
| **人形机器人** | GR00T N1, Figure AI, Tesla Optimus | 2025 年进入量产阶段 |
| **移动操作** | MoManipVLA, EchoVLA | 长程任务规划 |
| **工业部署** | Ambi PRIME-1, RLWRLD | 仓库自动化 |
| **服务机器人** | Pudu Robotics | 出货量超 12 万台 |

### 9.2 商业部署里程碑 (2025)

- **NVIDIA GR00T N1**：开源人形机器人基础模型，与 Google DeepMind、Disney 合作
- **Figure AI**：人形机器人进入商业生产
- **Tesla Optimus**：从舞台道具转变为服务工作者
- **Ambi Robotics PRIME-1**：首个面向仓库运营的 AI 基础模型
- **RLWRLD**：获得 Nebius 机器人物理 AI 奖基础模型类别
- **Pudu Robotics**：2025 年出货量超 12 万台，收入增长 100%+

---

## 10. 挑战与开放问题

### 10.1 当前挑战

| 挑战 | 具体问题 | 2025 进展 |
|------|----------|-----------|
| **推理速度** | 大模型推理慢 (~1Hz)，难以实时控制 | Spec-VLA (1.42x), π0 (50Hz) |
| **数据稀缺** | 高质量机器人数据收集成本高 | 异构数据融合、视频预训练 |
| **泛化局限** | 跨环境、跨机器人泛化仍困难 | RDT-2 零样本跨本体 |
| **安全性** | 真实部署的安全保障 | SafeVLA (83.58% 安全提升) |
| **长程任务** | 多步骤任务的规划与执行 | EchoVLA 双重记忆 |
| **计算资源** | 大模型部署成本高 | BitVLA (29.8% 内存) |

### 10.2 开放问题

1. **世界模型集成**：如何将预测模型与 VLA 结合进行规划
2. **多模态感知**：触觉、力觉、听觉的有效融合
3. **持续学习**：在线适应新任务和环境
4. **人机协作**：安全、自然的人机交互
5. **可解释性**：理解 VLA 的决策过程
6. **标准化评估**：统一的基准和评估协议

---

## 11. 重要论文列表 (2025 更新)

### 基础工作

| 论文 | 作者 | 会议 | 年份 | 一句话总结 |
|------|------|------|------|------------|
| RT-1: Robotics Transformer for Real-World Control at Scale | Google DeepMind | arXiv | 2022 | 首个大规模机器人 Transformer |
| RT-2: Vision-Language-Action Models | Google DeepMind | arXiv | 2023 | VLM 骨干 + 端到端训练 |
| RT-X: Robotic Transformer X | Google DeepMind | arXiv | 2023 | 跨机器人平台泛化 |

### 开源模型

| 论文 | 作者 | 会议 | 年份 | 一句话总结 |
|------|------|------|------|------------|
| OpenVLA: An Open-Source VLA Model | Stanford | arXiv | 2024 | 7B 参数最大开源 VLA |
| Octo: An Open-Source Generalist Robot Policy | Berkeley | arXiv | 2024 | 轻量级开源策略 |
| RDT-1B: Diffusion Foundation Model | 清华 | arXiv | 2024 | 双臂操作扩散模型 |
| **GR00T N1: Open Foundation Model for Humanoid Robots** | **NVIDIA** | **arXiv** | **2025** | **首个开源人形机器人基础模型** |
| **RDT-2: Zero-Shot Cross-Embodiment Generalization** | **清华** | **arXiv** | **2025** | **零样本跨本体泛化** |

### 高效 VLA

| 论文 | 作者 | 会议 | 年份 | 一句话总结 |
|------|------|------|------|------------|
| **A Survey on Efficient Vision-Language-Action Models** | **Yu et al.** | **arXiv** | **2025** | **高效 VLA 全面综述** |
| **BitVLA: 1-bit VLA Models** | **Wang et al.** | **arXiv** | **2025** | **首个 1-bit 量化 VLA** |
| **Spec-VLA: Speculative Decoding for VLA** | **Wang et al.** | **EMNLP** | **2025** | **投机解码加速推理** |
| **HyperVLA: Efficient Inference via Hypernetworks** | - | **OpenReview** | **2025** | **超网络高效推理** |
| TinyVLA: Fast, Data-Efficient VLA | Wen et al. | IEEE RA-L | 2025 | 紧凑高效 VLA |

### 扩散/流匹配 VLA

| 论文 | 作者 | 会议 | 年份 | 一句话总结 |
|------|------|------|------|------------|
| π0: A Vision-Language-Action Flow Model | Physical Intelligence | arXiv | 2024 | 流匹配实时控制 |
| **LLaDA-VLA: Vision Language Diffusion Action Models** | **Wen et al.** | **arXiv** | **2025** | **首个扩散 VLM 的 VLA** |
| Diffusion-VLA: Generalizable Robot Policies | - | arXiv | 2025 | 自回归+扩散统一 |

### 安全与可靠性

| 论文 | 作者 | 会议 | 年份 | 一句话总结 |
|------|------|------|------|------------|
| **SafeVLA: Safety Alignment via Constrained Learning** | **Zhang et al.** | **NeurIPS** | **2025** | **系统性安全对齐框架** |
| **SAFE: Multitask Failure Detection for VLA** | - | **NeurIPS** | **2025** | **多任务故障检测** |
| FPC-VLA: Failure Prediction and Correction | - | Expert Systems | 2026 | 故障预测纠正 |

### 移动操作

| 论文 | 作者 | 会议 | 年份 | 一句话总结 |
|------|------|------|------|------------|
| **MoManipVLA: Transferring VLA for Mobile Manipulation** | **Wu et al.** | **CVPR** | **2025** | **通用移动操作迁移** |
| **EchoVLA: Memory-Aware VLA for Long-Horizon** | - | **arXiv** | **2025** | **双重记忆长程任务** |
| AuxVLA: Auxiliary Task Learning for Mobile Manipulation | - | OpenReview | 2025 | 辅助任务增强 |

### 综述论文

| 论文 | 作者 | 会议 | 年份 | 链接 |
|------|------|------|------|------|
| Vision-Language-Action Models for Robotics: A Review | Kawaharazuka et al. | IEEE Access | 2025 | [vla-survey.github.io](https://vla-survey.github.io/) |
| A Survey on VLA Models for Embodied AI | Ma et al. | arXiv | 2024 | [arXiv:2405.14093](https://arxiv.org/abs/2405.14093) |
| **A Survey on Efficient Vision-Language-Action Models** | **Yu et al.** | **arXiv** | **2025** | **[arXiv:2510.24795](https://arxiv.org/abs/2510.24795)** |
| Large VLM-based VLA Models: A Survey | - | arXiv | 2025 | [arXiv:2508.13073](https://arxiv.org/abs/2508.13073) |

---

## 12. 主要研究团队

| 团队 | 机构 | 代表工作 |
|------|------|----------|
| Robotics at Google | Google DeepMind | RT 系列, PaLM-E |
| SVL | Stanford | OpenVLA, VoxPoser |
| RAIL | UC Berkeley | Octo, BridgeData |
| HMM Lab | 清华 | RDT-1B, RDT-2, RoboTwin |
| Physical Intelligence | - | π0 |
| **NVIDIA** | **NVIDIA** | **GR00T N1, Isaac Sim** |
| Microsoft Research | Microsoft | CogACT, ChatGPT for Robotics |
| **中科大/南大** | **USTC/NJU** | **LLaDA-VLA** |

---

## 13. 资源链接

### 模型与代码
- **OpenVLA**: https://openvla.github.io/
- **Octo**: https://octo-models.github.io/
- **RDT-1B/2**: https://github.com/thu-ml/RoboticsDiffusionTransformer
- **GR00T N1**: https://github.com/NVIDIA/Isaac-GR00T
- **π0**: https://www.pi.website/blog/pi0
- **LLaDA-VLA**: https://arxiv.org/abs/2509.06932

### 数据集
- **Open X-Embodiment**: https://openxembodiment.org/
- **BridgeData**: https://rail.eecs.berkeley.edu/datasets/bridge_data/

### 综述与跟踪
- **VLA Survey**: https://vla-survey.github.io/
- **Awesome-VLA**: https://github.com/KwanWaiPang/Awesome-VLA
- **Embodied AI Paper List**: https://github.com/HCPLab-SYSU/Embodied_AI_Paper_List

---

## 14. 关键趋势总结 (2025)

### 14.1 技术趋势

1. **架构多样化**：从单一 VLM 微调到扩散、流匹配、双系统等多种架构并存
2. **效率优先**：量化、蒸馏、投机解码等技术快速发展，推动 VLA 边缘部署
3. **跨本体泛化**：RDT-2 实现零样本跨本体，打破机器人形态壁垒
4. **安全对齐**：SafeVLA 等系统性安全框架成为部署刚需
5. **记忆机制**：EchoVLA 等引入显式记忆，支持长程任务

### 14.2 应用趋势

1. **人形机器人爆发**：GR00T N1、Figure AI、Tesla Optimus 推动人形机器人实用化
2. **商业部署加速**：从研究走向仓库、服务、制造等真实场景
3. **开源生态繁荣**：NVIDIA、Stanford、清华等持续开源模型和数据

### 14.3 挑战与机遇

| 挑战 | 机遇 |
|------|------|
| 推理速度 | 边缘 AI 芯片、模型压缩技术 |
| 数据稀缺 | 视频学习、仿真到真实、跨本体共享 |
| 安全性 | 安全对齐、故障检测、人机协作 |
| 泛化能力 | 世界模型、持续学习、多模态融合 |

---

*最后更新: 2025-02-26*
*更新内容: 新增 2025 年 10+ 篇重要论文，涵盖 GR00T N1、BitVLA、Spec-VLA、LLaDA-VLA、RDT-2、SafeVLA、MoManipVLA、EchoVLA 等最新进展*
