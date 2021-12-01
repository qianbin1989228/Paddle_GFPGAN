# Paddle_GPEN
[飞桨论文复现挑战赛第五期](https://github.com/PaddlePaddle/Paddle/issues/37401)  复现论文《[GAN Prior Embedded Network for Blind Face Restoration in the Wild](https://paperswithcode.com/paper/gan-prior-embedded-network-for-blind-face)》(GPEN)

本文首先跑通Pytorch版GPEN推理代码，然后使用飞桨PaddlePaddle复现该论文。

## 1. 基于Pytorch的GPEN算法推理
###  1.1 算法简介
老照片作为时光记忆的载体，是过去美好时光的传承者，尤其对于人物照片而言，更是每个人的情结和怀念的寄托。随着时间的流逝,许多人物老照片都因为自然或人为原因，受到了侵蚀损坏，画面模糊、褪色，照片磨损严重。因此，对这些照片进行处理使其在一定程度上得到修复，这已经成为了当前一项热门的技术。进入数字化时代以来，更多的人开始采用PS软件来对受损的人物照片进行修复，但是单纯依赖手工PS修复的方式效率低、学习曲线长，不适合批量修复任务。目前，人工智能正推动着传统照片修复技术往更高效、更简洁的方向发展，基于人工智能算法的照片批量自动修复逐渐成为可能，而这一切都要归功于近些年深度学习技术在数字图像处理领域的高速发展。

目前大多数深度学习修复方法在解决人脸修复问题时往往预先假设特定的退化模型，例如双线性下采样、高斯噪声、运动模糊、JPEG压缩等，然后依据这个提前定义好的退化模型人工生成“高—低”质量图像对，再采用深度CNN来学习低质量图像到高质量图像的映射。这种方法可以方便的生成大量的训练数据，因此，学习得到的算法模型修复效果显著。但是很明显，这种方法有个很大的缺陷，即只能修复特定退化模式的图像，而在真实应用中，受损的人脸图像其退化过程往往是未知的（盲人脸），我们无法准确估计其退化模型，因此，这类方法针对盲人脸图像的修复效果一般。

本次复现的论文提出了一种基于GAN先验的盲人脸图像修复方法。该方法首先学习一个用于生成高分辨率人脸图像的StyleGANV2模型，并将其嵌入到U形 DNN中作为先验解码器，然后用一组合成的低质量人脸图像对先验嵌入的GAN进行微调。GPEN算法从DNN的深层和浅层特征分别生成GAN的潜码和噪声输入，控制重建图像的全局人脸结构、局部人脸细节和背景。GPEN算法易于实现，修复效果惊艳。GPEN算法模型结构如下图所示：

<div align="center">
<img src=./figures/model.png  width="90%"> 
</div>

总体来看，这篇论文的思想是建立在[StyleGANv2](https://github.com/NVlabs/stylegan2)基础上的。StyleGANv2是专门用来生成高清逼真人脸图像的算法，通过FFHQ共7万张不同真实的人脸图像训练，可以非常真实的进行“人脸幻想”，幻想出来的人脸真实度高、细节丰富。由于StyleGANv2的输入是一个随机向量，因此如果我们能替代掉这个向量，或者用另一个模型来生成这个向量，那么就可以级联StyleGANv2模型，获得这种高质量的“幻想”性能。引申到图像修复任务中，如果我们用待修复的低质量图像预先生成这个隐向量，然后作为StyleGANv2的输入，那么通过级联训练，最终就可以实现基于“人脸幻想”的惊艳的修复效果。这就是这篇论文GPEN的根本思路。

### 1.2 环境准备
* 下载工程
``` bash
git clone https://github.com/qianbin1989228/Paddle_GPEN.git
```

然后进入到pytorch目录中：
``` bash
cd Paddle_GPEN/pytorch
```

* 安装Pytorch依赖包
``` bash
pip install -r requirement.txt 
```

* 下载模型文件到model_zoo文件夹中
``` bash
cd ./model_zoo
wget https://public-vigen-video.oss-cn-shanghai.aliyuncs.com/robin/models/RetinaFace-R50.pth
wget https://public-vigen-video.oss-cn-shanghai.aliyuncs.com/robin/models/GPEN-512.pth
cd ..
```

### 1.3 推理
将待测试的图片放置在./testphoto/in文件夹中，运行下面的命令即可开始批量修复：

``` bash
python main.py
```

修复后的图片位于./testphoto/out文件夹中。部分修复样例如下图所示：

<div align="center">
<img src=./figures/demo_pytorch.jpg  width="100%"> 
</div>

## 2. PaddlePaddle论文复现

### 2.1 训练StyleGanV2
* 待完成；

### 2.2 级联训练GPEN模型

*注：待完成*

### 2.3 预测
* 待完成；


## 3. 工程部署
待完成。

