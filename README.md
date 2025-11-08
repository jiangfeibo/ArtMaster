# Flux.1-dev-lora

<div align="center">
  <img src="https://github.com/jiangfeibo/Flux.1-dev-lora/blob/main/README.assets/FLux.jpg" alt="image text" width="500px">
</div>

## 项目简介

FLUX.1系列模型于2024年由Black Forest Labs（BFL）发布，是该实验室迄今为止最具代表性的文本生成图像（Text-to-Image）模型家族。作为新一代生成式AI系统，FLUX.1在图像生成质量、文本指令理解能力以及视觉一致性等方面，均达到了业界领先水平，被广泛认为是继Stable Diffusion之后，开源图像生成领域的又一次重大突破。FLUX.1模型采用创新性的Flow Matching Transformer架构，将扩散模型的稳定性与Transformer的高效表示能力相结合，在图像细节呈现、语义理解、风格多样性和生成速度等多个维度实现了全面提升。BFL团队在开发过程中，针对图像清晰度、提示词遵从度（Prompt Adherence）以及复杂场景生成等关键问题进行了系统优化，使模型能够精准地理解文本语义，并生成符合创作者预期的高保真图像。

然而，对于具有独特笔墨语汇与审美规范的中国传统山水画，通用模型仍存在明显的“域间差距”。

为此，本项目以FLUX.1-dev为基础，引入LoRA（Low-Rank Adaptation） 的轻量化微调方案，定向迁移至“曾晓浒风格山水” 的笔墨体系与审美范式。我们围绕曾晓浒作品的核心要素——如代表性皴法的运用与节奏、墨色层次与破/积墨关系、留白比例与典型构图法、题跋/印章的常用位置与尺度，建立高质量图文对并完成数据清洗与风格标签标准化；在不改动基座权重的前提下，仅对关键层注入低秩适配器，实现最小侵入式适配，并配合风格提示约束与推理阶段的提示重写策略提升稳定性与可控性。实验表明，相较未微调的基线模型，微调后的 FLUX.1 在“笔触质感保真度”“墨韵层次与氛围”“留白与构图一致性”以及“曾氏气韵复现度”等维度取得显著提升，能够稳定生成符合目标风格范式的高质量山水图像。项目将提供曾晓浒风格LoRA适配器与推理示例，便于与原始FLUX.1权重组合，在本地或云端快速复现与二次创作。


#### 特点

- 基于开源的FLUX.1-dev模型，FLUX.1-dev在prompt遵从、细节刻画等方面表现优异，接近闭源最先进模型。

- Lora微调无需改动原始权重，从而大幅度降低训练参数量与显存消耗。

- 获得较小的最终结果，易于共享和下载。



## 安装与加载

克隆本项目到本地：https://github.com/jiangfeibo/Flux.1-dev-lora

git clone

cd Flux.1-dev-lora



## 模型测试

在同样prompt的前提下，基础模型、Lora模型的生成效果如下：

| <img src="https://github.com/jiangfeibo/Flux.1-dev-lora/blob/main/README.assets/Flux_1.jpg" width="250px"> | <img src="https://github.com/jiangfeibo/Flux.1-dev-lora/blob/main/README.assets/Flux_2.png" width="250px"> | <img src="https://github.com/jiangfeibo/Flux.1-dev-lora/blob/main/README.assets/lora_1.png" width="250px"> | <img src="https://github.com/jiangfeibo/Flux.1-dev-lora/blob/main/README.assets/lora_2.png" width="250px"> |
|:---------------------------------:|:---------------------------------:|:---------------------------------:|:---------------------------------:|
| 图 1：Flux | 图 2：Flux | 图 3：Lora | 图 4：Lora |

其中，左边两幅图为Flux.1生成的图片，而右边两幅图则是在相同的prompt下加入Lora后生成的图片，由此可见Lora加入后效果明显。



## 数据集

本项目采用了曾晓浒大师的20幅作品作为数据集，为了更好的训练Lora，我们将20幅作品作为两组，并对作品进行裁剪，裁剪成了512×512和512×768。每种尺寸的图片各20张，为了让模型更好的学习到特征，训练时每张照片模型会学习10次。

数据集链接：

- https://github.com/jiangfeibo/Flux.1-dev-lora/tree/main/datasets/512%C3%97512

- https://github.com/jiangfeibo/Flux.1-dev-lora/tree/main/datasets/512%C3%97768



## 贡献者

江沸菠，jiangfb@hunnu.edu.cn，湖南师范大学，副教授

毛磊，2547219103@qq.com，湖南师范大学，在读研究生

朱万运，湖南师范大学，在读研究生
























