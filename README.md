# Paddle_GPEN
[飞桨论文复现挑战赛第五期](https://github.com/PaddlePaddle/Paddle/issues/37401)  复现论文《[GAN Prior Embedded Network for Blind Face Restoration in the Wild](https://paperswithcode.com/paper/gan-prior-embedded-network-for-blind-face)》(GPEN)

## 1. 简介
目前大多数深度学习修复方法在解决人脸修复问题时往往预先假设特定的退化模型，例如双线性下采样、高斯噪声、运动模糊、JPEG压缩等，然后依据这个提前定义好的退化模型人工生成“高—低”质量图像对，再采用深度CNN来学习低质量图像到高质量图像的映射。这种方法可以方便的生成大量的训练数据，因此，学习得到的算法模型修复效果显著。但是很明显，这种方法有个很大的缺陷，即只能修复特定退化模式的图像，而在真实应用中，受损的人脸图像其退化过程往往是未知的，我们无法准确估计其退化模型，因此，这类方法针对盲人脸修复(Blind Face Restoration, BFR)任务效果一般。

本次复现的论文提出了一种基于GAN先验的盲人脸图像修复方法。该方法首先学习一个用于生成高分辨率人脸图像的StyleGAN2模型，并将其嵌入到U形DNN中作为先验解码器，然后用一组合成的低质量人脸图像对网络模型进行微调。GPEN算法从DNN的深层和浅层特征分别生成GAN的潜码和噪声输入，控制重建图像的全局人脸结构、局部人脸细节和背景。GPEN算法模型结构如下图所示：

<div align="center">
<img src=./figures/model.png  width="100%"> 
</div>

总体来看，GPEN的思想是建立在[StyleGAN2](https://github.com/NVlabs/stylegan2)基础上的。StyleGAN2是专门用来生成高清人脸图像的算法，其生成的人脸图像更加真实、更加清晰。由于StyleGAN2的输入是一个随机隐向量和噪声，因此如果能替代掉这个随机隐向量和噪声，或者用另一个模型来生成这个隐向量和噪声，那么就可以控制待生成的人像面部特征，GPEN就采用了这样的方法。

## 2. 复现精度
| NetWork | epochs | opt | image_size | batch_size | dataset | PSNR | FID | LPIPS |
| --- | --- | --- | --- | --- | --- | --- | --- |--- |
| GPEN |  |  | 512X512 |  | CelebA-HQ | 待完成 |待完成 |待完成 |

## 3. 数据集
* 待完成；

## 4. 环境依赖
* 待完成；

## 5. 快速开始

### 5.1 训练

### 5.2 验证

### 5.3 推理


## 6. 代码结构和详细说明


## 7. 模型信息

| 信息 | 描述 |
| --- | --- |
|模型名称| GPEN |
|框架版本| PaddlePaddle==2.2.0|
|应用场景| 人像修复 |