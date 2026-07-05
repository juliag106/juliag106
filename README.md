## Lucy Liang · 梁露西

> 电子科技大学 · 从本科一路做声学大模型 —— 让机器「听懂」声音：从表示、定位，到理解。

一条从本科延续到研究生的研究线，三个开源项目把它串起来：

**2020 – 2022 · 打地基**
[resona](https://github.com/juliag106/resona) —— 统一声学自监督表示学习。语音 / 环境声 / 声场信号的掩码建模与对比预训练，作为后续一切工作的声学底座。

**2022 – 2024 · 学会定位**
[sonoloc](https://github.com/juliag106/sonoloc) —— 声学事件检测与声源定位（SELD）。多通道 SRP-PHAT / MUSIC 定位 + 弱标注 MIL 检测，鲁棒于噪声场景。

**2024 – 2026 · 走向理解**
[sonolingua](https://github.com/juliag106/sonolingua) —— 把统一声学编码器接入大语言模型，做声学场景理解、音频–文本检索与描述生成。

---

**一以贯之**：纯 NumPy 内核、`import` 不拉深度学习框架，无 GPU / 无网络也能跑核心与单测；需要训练时再接可选 PyTorch 后端。离线优先，CI 全绿。

<sub>UESTC · 声学大模型 · 表示 → 定位 → 理解 · she/her</sub>
