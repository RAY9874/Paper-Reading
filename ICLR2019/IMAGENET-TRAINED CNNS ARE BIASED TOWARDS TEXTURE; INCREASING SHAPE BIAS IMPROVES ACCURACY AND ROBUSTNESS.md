#### IMAGENET-TRAINED CNNS ARE BIASED TOWARDS TEXTURE; INCREASING SHAPE BIAS IMPROVES ACCURACY AND ROBUSTNESS

### 猜想

作者猜想CNN是按照纹理（texture）特征进行识别的，而不是形状（shape）

> we believe that it is time to consider a second explanation, which we term the texture hypothesis: in contrast to the common assumption, object textures are more important than global object shapes for CNN object recognition. 

### 实验

作者选取了ImageNet的子集，16种物体，进行了4中变换（灰度、轮廓、边缘、纹理），对多个神经网络模型（AlexNet,GoogLeNet,VGG-16,Resnet-50）与人类识别进行比较。特殊说明了

1. SIN数据集
2. 人类识别的方式

#### Stylized-ImageNet数据集

作者将原ImageNet数据集（IN）的纹理不变，用AdaIN 风格对图像进行了变换-SIN

> Starting from ImageNet we constructed a new data set (termed Stylized-ImageNet or SIN) by stripping every single image of its original texture and replacing it with the style of a randomly selected painting through AdaIN style transfer

#### 心理物理实验：

他们在邀请人（97个人看了48560张图）来进行区分图片的时候考虑到了如人的神经反射、记忆力等等不同于CNN的部分并对这些情况采取了相应的办法保证实验的公平性。

### 实验结果

1. 在原图、灰度图和纹理图上，CNN和人类都取得了接近全对的准确率。
2. 在轮廓图、边缘图上，CNN取得了较低的准确率。

进而，他们使用SIN的数据，令机器和人类分别判断，发现人类主要依靠“形状”作为依据，而CNN使用“纹理”作为依据

#### 鲁棒性

他们认为使用SIN变换后的数据训练模型能够提升模型的鲁棒性

> Shape-ResNet surpasses the vanilla ResNet in terms of top-1 and top5 ImageNet validation accuracy as reported in Table 2. This indicates that SIN may be a useful data augmentation on ImageNet that can improve model performance without any architectural changes.

他们也尝试了在目标检测中使用这种数据增强方式，并在Faster-RCNN 上获得了约5个点的mAP提升

> We tested the representations of each model as backbone features for Faster-RCNN (Renetal.,2017) on Pascal VOC 2007 and MS COCO. Incorporating SIN in the training data  substantially improves object detection performance from 70.7 to 75.1 mAP50(52.3 to 55.2 mAP50 on MS COCO)

### 实验代码

论文中给出了他们的[github](https://github.com/rgeirhos/texture-vs-shape)