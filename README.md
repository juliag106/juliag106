## Lucy Liang · 声学大模型 / Acoustic Foundation Models

电子科技大学（UESTC）研究生，本科起就专注**声学大模型**方向。我的研究把声学信号从底层表示一路做到与大语言模型的对接，围绕一条主线展开：

> **统一声学表示 → 事件检测与声源定位 → 声学基础模型接入 LLM**

工程上偏好**可复现、离线优先**的开源实现——核心以 NumPy 编写，装好即用，不依赖 GPU 或重型框架；深度学习部分（PyTorch / transformers）一律作为可选后端，缺失也不影响主链路运行。

![Python](https://img.shields.io/badge/Python-3.9%2B-3776AB?logo=python&logoColor=white)
![NumPy](https://img.shields.io/badge/core-NumPy-013243?logo=numpy&logoColor=white)
![PyTorch](https://img.shields.io/badge/optional-PyTorch-EE4C2C?logo=pytorch&logoColor=white)
![License](https://img.shields.io/badge/license-MIT-green.svg)
![Focus](https://img.shields.io/badge/focus-Acoustic%20Foundation%20Models-6f42c1)

---

### 研究主线上的三个项目

这三个仓库不是孤立的 demo，而是同一条技术路线上前后衔接的三段：表示学习打底，检测/定位处理时空结构，最后把编码器接到语言模型上做理解与生成。

| 阶段 | 项目 | 一句话 |
| :-- | :-- | :-- |
| ① 表示 | [**resona**](https://github.com/juliag106/resona) | 面向语音 / 环境声 / 声场的统一自监督表示学习工具包 |
| ② 检测与定位 | [**sonoloc**](https://github.com/juliag106/sonoloc) | 多通道声学事件检测与声源定位（SELD）工具箱 |
| ③ 接入 LLM | [**sonolingua**](https://github.com/juliag106/sonolingua) | 把统一声学编码器接入大语言模型的声学理解框架 |

---

#### ① [resona](https://github.com/juliag106/resona) — 统一声学自监督表示

把**语音、环境声、声场（多通道）**三类信号统一到同一套特征前端与预训练接口下。一个 `UnifiedFrontend` 按信号域自动选参并输出规整张量，多通道信号会自动拼接 ILD / IPD 等空间线索；预训练提供两条共享同一 Transformer 编码器的路线——**掩码声学建模（MAE 风格重建）**与 **InfoNCE 对比学习**。损失与掩码都保留纯 NumPy 参考实现作为「真值」，便于单测逐值校验。

`self-supervised` · `masked-modeling` · `contrastive-learning` · `audio-representation`

#### ② [sonoloc](https://github.com/juliag106/sonoloc) — 事件检测与声源定位（SELD）

围绕**弱标注**与**鲁棒噪声场景**两个实际难点组织，既给出可解释的经典信号处理基线，也对齐 DCASE 任务三的特征、标签与指标。包含 **SRP-PHAT / MUSIC** 经典 DOA 定位、GCC-PHAT 与 FOA 有源声强特征、注意力等 **MIL 池化**的弱标注检测、单/多轨 **ACCDOA** 标签编解码，以及自由场平面波 + 扩散噪声按目标 SNR 混合的可控评测数据；神经部分为可选的 CRNN + ACCDOA 头。

`seld` · `sound-source-localization` · `direction-of-arrival` · `weakly-supervised`

#### ③ [sonolingua](https://github.com/juliag106/sonolingua) — 声学编码器 × 大语言模型

把「声学前端 → 声学编码器 → 模态桥接 → 语言模型」这条链路封装成一个对象，核心观点是：**音频描述、声学检索、场景标注可以共享同一个声学嵌入空间**。提供纯 NumPy 的对数梅尔前端、可插拔声学编码器、线性投影 + 软提示适配器的模态桥接，一套接口即可完成**零样本场景理解、音频-文本检索、描述生成**三类任务，并内置 Recall@K / mAP 与 BLEU / ROUGE-L / CIDEr 风格评测。路线图上正逐步接入 PANN / BEATs / HTSAT 与 `transformers` 后端。

`large-language-models` · `audio-text-retrieval` · `audio-captioning` · `acoustic-scene-classification`

---

### 设计取向

- **离线优先**：核心算法只依赖 NumPy，无 GPU、无重型框架也能跑通全流程。
- **可复现**：经典信号处理基线可解释、可对拍；关键实现附纯 NumPy 参考版供单测逐值校验。
- **工程基建齐全**：ruff + mypy + pytest，CI 多版本矩阵，pre-commit 钩子。
- **可选而非强制**：深度学习后端一律作为 extra 依赖，按需启用。

### 研究兴趣

声学信号自监督表示 · 声学事件检测与声源定位（SELD） · 统一声学基础模型 · 声学理解与大语言模型的对接 · 可复现的开源声学工具链

<sub>核心 NumPy · 可选 PyTorch / transformers · MIT License</sub>
