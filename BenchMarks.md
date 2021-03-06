# Benchmark整理

## Catalogue
  - [Datasets](#datasets)
    - [MVTec AD](#mvtec-ad)
    - [BTAD](#btad)
    - [MNIST / Fashion MNIST](#mnist--fashion-mnist)
    - [CIFAR10/CIFAR100](#cifar10cifar100)
    - [DogsVsCats](#dogsvscats)
    - [ImageNet-30](#imagenet-30)
    - [KDDCUP](#kddcup)
  - [Evaluation Metrics](#evaluation-metrics)
  - [SOTA methods](#sota-methods)
    - [Unsupervised](#unsupervised)
    - [Surpervised](#surpervised)
    - [Smi-supervised](#smi-supervised)

## Datasets

### MVTec AD

​&emsp;&emsp;MVTec AD is a dataset for benchmarking anomaly detection methods with a focus on industrial inspection. It contains over 5000 high-resolution images divided into fifteen different object and texture categories. Each category comprises a set of defect-free training images and a test set of images with various kinds of defects as well as images without defects.

​&emsp;&emsp;The training set is only composed of  normal images, while the test set is a mixture of normal images and abnormal images

​&emsp;&emsp;Defect Anomaly

<img src="figure/image-20220111173058753.png" alt="image-20220111173058753" style="zoom:33%;" />

<img src="figure/image-20220112100548496.png" alt="image-20220112100548496" style="zoom: 67%;" />

### BTAD

​&emsp;&emsp;BeanTech Anomaly Detection dataset (Mishraet al. 2021) has 3 categories industrial products with 2540 images.

​&emsp;&emsp;The training set consists only of normal images, while the test set is a mixture of normal images and abnormal images.

​&emsp;&emsp;pixel-wise

<img src="figure/image-20220111174257429.png" alt="image-20220111174257429" style="zoom: 33%;" />

### MNIST / Fashion MNIST

* unimodal： 一个类作为正常样本，其他类作为异常样本
* multimodal case： 一个类作为异常样本，其他类作为正常

### CIFAR10/CIFAR100

* unimodal： 一个类作为正常样本，其他类作为异常样本
* multimodal case： 一个类作为异常样本，其他类作为正常

### DogsVsCats

​&emsp;&emsp;The training archive contains 25,000 images of dogs and cats. Train your algorithm on these files and predict the labels for test1.zip (1 = dog, 0 = cat).

### ImageNet-30

&emsp;&emsp;Contain images from 30 classes of high resolution images chosen from the ImageNet dataset.

### KDDCUP

&emsp;&emsp;The KDDCUP99 10 percent dataset from the UCI repositor originally contains samples of 41 dimensions, where 34 of them are continuous and 7 are categorical. For categorical features, we further use one-hot representation to encode them, and eventually we obtain a dataset of 120 dimensions. As 20% of data samples are labeled as “normal” and the rest are labeled as “attack”, “normal” samples are in a minority group; therefore, “normal” ones are treated as anomalies in this task.


## Evaluation Metrics

* Receiver operating characteristic curve (AUROC)
* Per-region-overlap score(PRO-score)

* Anomaly score
  * Detection: single one for each input test image.
  * Segmentation: for each pixel.

* Mahalanobis distance


## SOTA methods

### Unsupervised

* **AnoGAN**. 	in   "Unsupervised Anomaly Detection with Generative Adversarial Networks to Guide Marker Discovery" 2017

* **F-AnoGAN**.    in  "f-AnoGAN: Fast unsupervised anomaly detection with generative adversarial networks" 2018

* **DAGMM**.    in    "Deep Autoencoding Gaussian Mixture Model for Unsupervised Anomaly Detection"  2018 ICLR

* **MemAE**.   in    "Memorizing Normality to Detect Anomaly: Memory-augmented Deep Autoencoder for Unsupervised Anomaly Detection" 2019 ICCV

  * MNIST: 0.9751 
  * CIFAR10: 0.6088

* **PaDiM**.    in    PaDiM: a Patch Distribution Modeling Framework for Anomaly Detection and Localization 2020
  * MVTec AD: 97.900(Detection AUROC); 97.500(Segmentation AUROC)
  
* **CFlOW-AD**.    in    "CFLOW-AD: Real-Time Unsupervised Anomaly Detection with Localization via Conditional Normalizing Flows" 2021
  * MVTec AD: 98.260(Detection AUROC); 98.620(Segmentation AUROC)

* **CS-Flow**. in "Fully Convolutional Cross-Scale-Flows for Image-based Defect Detection" 2022, WACV
  
* **FastFlow**.    in    "FastFlow: Unsupervised Anomaly Detection and Localization via 2D Normalizing Flows" 2021
  
  * MVTec AD: 99.400(Detection AUROC); 98.500(Segmentation AUROC)
  * CIFAR10: 0.667
  
  > 2D解释：
  >
  > &emsp;&emsp;论文中说是使用2D flow结构，然而在查看RealNVP论文源码之后，发现原始的Flow结构就是属于2D结构，故产生强调2DFlow结构的疑问。
  >
  > &emsp;&emsp;后续调研发现，其对比方法是基于之前将Flow用到Anomaly Detection中的方法，例如DifferNet(2020)。在这些已有工作中，Flow结构采用FC结构，即1DFlow。究其原因是文章将Flow模块接到Representation网络之后做分布变换，而一般Representation提取网络输出都是特征向量（即1D向量），所以使用1DFlow是比较自然的做法。
  >
  > &emsp;&emsp;回到FastFlow，文章提出需要保留图片局部特征结构，所以在特征提取阶段，并未使用最终1D特征向量，而是使用中间层具有2D结构的特征作为Flow的输入，从而可以使用2DFlow结构，即卷积操作。也就是原始的Flow结构。

### Surpervised

### Smi-supervised
* **DifferNET** "Same But DifferNet:Semi-Supervised Defect Detection with Normalizing Flows" 2020 WACV
  * ROC: Anomaly score based on $\log p(x)$ or $\log p(z)$; based on a scoring function, gievn a threshold $\theta$, get ROC curve.

### Self-supervised
* **Patch SVDD** in "Patch SVDD: Patch-level SVDD for anomaly detection and segmentation." ACCV 2020
* **CutPaste**  in "CutPaste: Self-Supervised Learning for Anomaly Detection and Localization" 2021
  * https://github.com/Runinho/pytorch-cutpaste Unofficial work in progress PyTorch reimplementation