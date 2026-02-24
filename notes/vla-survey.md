# VLA (Vision-Language-Action) 模型综述

> 涵盖 RT-1 到 OpenVLA 的技术演进、代表性工作对比及最新进展

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

---

## 2. 技术路线分类

### 2.1 基于 VLM 微调的 VLA

**核心方法**：冻结或微调预训练 VLM，添加动作预测头

| 模型 | 机构 | 参数 | 特点 |
|------|------|------|------|
| **RT-2** | Google DeepMind | 55B | PaLI-X 骨干，端到端训练 |
| **OpenVLA** | Stanford/UC Berkeley | 7B | 最大开源模型，970k 演示数据 |
| **CogACT** | Microsoft | 7B | CogVLM + 动作预测 |

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
| **Octo** | Berkeley/Stanford | 93M | 开源通用机器人策略 |
| **π0** | Physical Intelligence | - | 流匹配，实时推理 |

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

---

## 3. 重要模型详细对比

### 3.1 Google RT 系列

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

### 3.2 开源模型对比

| 模型 | 参数 | 骨干 | 开源数据 | 推理速度 | 特点 |
|------|------|------|----------|----------|------|
| **OpenVLA** | 7B | Llama 2 + DINOv2 | 970k | ~5-15 Hz | 最大开源 |
| **Octo** | 93M | Transformer | 800k | ~5-15 Hz | 轻量高效 |
| **RDT-1B** | 1B | Diffusion Transformer | 1M+ | ~5-10 Hz | 双臂操作 |
| **π0** | - | Flow Matching | - | ~5-15 Hz | 实时推理 |

---

## 4. 主流数据集

### 4.1 大规模机器人数据集

| 数据集 | 规模 | 机器人 | 特点 |
|--------|------|--------|------|
| **Open X-Embodiment** | 1M+ | 22 种 | 跨机器人、跨任务 |
| **BridgeData V2** | 60k | WidowX | 单臂操作 |
| **ALOHA** | 500+ | ALOHA | 双臂精细操作 |
| **RH20T** | 110k | 多种 | 人类演示视频 |
| **DROID** | 76k | Franka | 多样化场景 |

### 4.2 数据收集策略

1. **人类遥操作**：ALOHA, RH20T
2. **脚本生成**：SURREAL, RLBench
3. **视频学习**：Something-Something, EPIC-Kitchens
4. **仿真到真实**：Isaac Gym, SAPIEN

---

## 5. 应用场景

### 5.1 机器人操作
- 抓取与放置
- 工具使用
- 抽屉/柜门开关
- 双臂协调操作

### 5.2 导航
- 视觉语言导航 (VLN)
- 目标导向导航
- 开放词汇导航

### 5.3 人机交互
- 跟随自然语言指令
- 问答式任务澄清
- 多轮对话

---

## 6. 挑战与开放问题

### 6.1 当前挑战

| 挑战 | 具体问题 |
|------|----------|
| **推理速度** | 大模型推理慢 (~1Hz)，难以实时控制 |
| **数据稀缺** | 高质量机器人数据收集成本高 |
| **泛化局限** | 跨环境、跨机器人泛化仍困难 |
| **安全性** | 真实部署的安全保障 |
| **长程任务** | 多步骤任务的规划与执行 |

### 6.2 未来方向

1. **高效推理**：模型蒸馏、量化、投机解码
2. **数据扩展**：仿真数据、视频预训练、跨机器人学习
3. **世界模型**：结合预测模型进行规划
4. **多模态融合**：触觉、力觉、听觉融合
5. **持续学习**：在线适应新任务和环境

---

## 7. 重要论文列表

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

### 综述论文

| 论文 | 作者 | 会议 | 年份 | 链接 |
|------|------|------|------|------|
| Vision-Language-Action Models for Robotics: A Review | Kawaharazuka et al. | IEEE Access | 2025 | [vla-survey.github.io](https://vla-survey.github.io/) |
| A Survey on VLA Models for Embodied AI | Ma et al. | arXiv | 2024 | [arXiv:2405.14093](https://arxiv.org/abs/2405.14093) |

---

## 8. 主要研究团队

| 团队 | 机构 | 代表工作 |
|------|------|----------|
| Robotics at Google | Google DeepMind | RT 系列, PaLM-E |
| SVL | Stanford | OpenVLA, VoxPoser |
| RAIL | UC Berkeley | Octo, BridgeData |
| HMM Lab | 清华 | RDT-1B, RoboTwin |
| Physical Intelligence | - | π0 |
| Microsoft Research | Microsoft | CogACT, ChatGPT for Robotics |

---

## 9. 资源链接

- **OpenVLA**: https://openvla.github.io/
- **Octo**: https://octo-models.github.io/
- **RDT-1B**: https://github.com/thu-ml/RoboticsDiffusionTransformer
- **Open X-Embodiment**: https://openxembodiment.org/
- **VLA Survey**: https://vla-survey.github.io/
- **Embodied AI Paper List**: https://github.com/HCPLab-SYSU/Embodied_AI_Paper_List

---

*最后更新: 2025-02-24*
