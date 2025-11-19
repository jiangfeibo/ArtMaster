# ArtMaster
<div align="center">

| <img src="https://github.com/jiangfeibo/Flux.1-dev-lora/blob/main/README.assets/cover_1.png" width="280px"> | <img src="https://github.com/jiangfeibo/Flux.1-dev-lora/blob/main/README.assets/cover_2.png" width="280px"> | <img src="https://github.com/jiangfeibo/Flux.1-dev-lora/blob/main/README.assets/lora_2.png" width="280px"> |
|:---:|:---:|:---:|

</div>

## 项目概述

随着视觉生成模型（如Stable Diffusion、Midjourney、DALL·E等）的快速发展，AI艺术创作已成为大众化的创意工具。然而，当前主流的视觉大模型普遍采用多风格融合训练的方式，模型在生成时往往同时学习了成千上万种艺术风格与构图逻辑。这种泛化式学习虽然提升了模型的多样性，但也带来了两个显著问题：

- 风格一致性缺失：现有模型生成的作品虽具备一定美感，但往往无法稳定复现特定艺术家的独特风格特征，例如笔触走向、色彩构成、构图逻辑、意象符号等。生成结果在细节表现上呈现出“混合风格”的特征，艺术辨识度较低。
  
- 艺术语义漂移：由于大模型在多风格语料中学习的特征过于分散，其输出的语义往往趋向于“平均化”，难以精准体现单一艺术家创作中的精神内核或美学意图。这使得模型更像是“风格的模仿者”，而非“风格的继承者”。
  
基于此，本项目旨在构建首个以单一画家风格为核心的大规模视觉模型ArtMaster。该模型将以湖南山水画大师曾晓浒先生的手稿作品为基础，结合多阶段特征提炼、跨层风格约束与语义引导机制，使生成的每一幅图像在风格、色调、笔触、构图逻辑上均与原艺术家保持高度一致。本项目填补了目前市面上尚无真正以“单一画家风格”为训练核心的大模型的空白。同时，通过模型化的方式保留艺术家的风格基因，推动数字艺术保护与再创作。


## 技术贡献

#### 数据集处理

为了确保模型能够充分学习目标画家的风格特征，同时兼顾图像内容的完整性与分辨率适配性，本项目对原始画集数据进行了系统化的筛选与裁剪处理。首先，收集了曾晓浒老师的所有代表性作品。这些作品覆盖了其主要创作时期与典型题材，保证了画风在色彩、构图、笔触等方面的多样性与代表性。由于不同作品原始尺寸存在显著差异（包括横幅、竖幅及方形构图），因此在数据预处理阶段，对原图进行了统一的尺寸规范化。我们针对挑选出的作品，分别裁剪出了两种规格的样本，分别是512×512和512×768。在裁剪过程中，优先保留画面主体区域，避免破坏主要视觉元素和笔触连续性；对背景或边缘部分进行适度平衡裁剪，以保证风格一致性与训练数据的代表性。

#### 模型微调

本项目我们采用AdaLoRA进行模型微调，LoRA微调作为近年来在大模型领域广泛应用的一种轻量化适配方法，具有显著的灵活性与高效性。相比传统的全参数微调方式，LoRA不需要对原模型的全部权重进行更新，而是通过在特定层中引入低秩矩阵，对模型参数进行有针对性的调整。这种方法不仅极大地降低了训练过程中的显存占用与计算开销，还能在较小的数据集上实现稳定而精准的风格迁移。



## 项目参数

本次训练基于Flux.1-dev基础模型，采用AdaLoRA微调方法。数据集由经过裁剪与处理的画家风格样本构成，分辨率为512×512和512×768。训练使用AdamW优化器，学习率设为2e-4，共进行15个epoch，batch size为1。每张图片在训练中被重复学习10次，总训练步数约为6000步。



## 安装与加载

克隆本项目到本地：https://github.com/jiangfeibo/ArtMaster

git clone

cd ArtMaster



## 模型效果生成展示



<div align="center">

| **原始图画** | **Flux 模型** | **ArtMaster** |
|:---:|:---:|:---:|
| <img src="https://github.com/jiangfeibo/Flux.1-dev-lora/blob/main/README.assets/18.JPG" width="280px"> | <img src="https://github.com/jiangfeibo/Flux.1-dev-lora/blob/main/README.assets/Flux_1.jpg" width="280px"> | <img src="https://github.com/jiangfeibo/Flux.1-dev-lora/blob/main/README.assets/lora_1.png" width="280px"> |
| <img src="https://github.com/jiangfeibo/Flux.1-dev-lora/blob/main/README.assets/03.JPG" width="280px"> | <img src="https://github.com/jiangfeibo/Flux.1-dev-lora/blob/main/README.assets/Flux_2.png" width="280px"> | <img src="https://github.com/jiangfeibo/Flux.1-dev-lora/blob/main/README.assets/lora_2.png" width="280px"> |

</div>


## 曾晓浒简介
曾晓浒（1938-2015）是湖南美术界极具代表性的山水画大家和美术教育家，在湘生活、教学、创作共五十四年，成就了其融贯南北画风、吸收西画光色、表现湖南地域风貌的山水画面貌。他提出的"真山真水真笔墨"的山水画美学观念，体现了崇"真"精神和写生创作方法的统一。他的作品既有岭南画派明丽色彩和强烈光影的运用，又创造性地在深涧幽谷中以纯色点画明亮的乔木，形成个性鲜明的艺术语言。他对翠绿色系和赭黄色系的偏好与创造性运用，形成了其独特的诗意氛围营造方式。曾晓浒被认为是美术史上第一个长期寄寓湖南并以一生努力开拓、发掘、创造湖南山水画资源并形成潇湘山水画派的画家，堪称一代宗师。





## 贡献者

指导老师：
江沸菠，jiangfb@hunnu.edu.cn，唐宏岳，曾进，湖南师范大学


模型设计与编程：
毛磊，202520294367@hunnu.edu.cn，湖南师范大学，在读研究生，
朱万运，湖南师范大学，在读研究生
























