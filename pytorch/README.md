# Pytorch_GPEN
[飞桨论文复现挑战赛第五期](https://github.com/PaddlePaddle/Paddle/issues/37401)  复现论文《[GAN Prior Embedded Network for Blind Face Restoration in the Wild](https://paperswithcode.com/paper/gan-prior-embedded-network-for-blind-face)》(GPEN)

*注：本次论文复现首先跑通Pytorch版代码，本工程对参考代码进行了大量调整，在不影响精度的前提下使整个推理模型更加简单，依赖更少，也更容易理解，具体见第2部分。*

## 1. 环境准备
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
wget https://public-vigen-video.oss-cn-shanghai.aliyuncs.com/robin/models/GPEN-512.pth
cd ..
```

## 2. 推理
将待测试的图片放置在./testphoto/in文件夹中，运行下面的命令即可开始批量修复：

``` bash
python main.py
```

修复后的图片位于./testphoto/out文件夹中。部分修复样例如下图所示：

<div align="center">
<img src=../figures/demo_pytorch.jpg  width="100%"> 
</div>