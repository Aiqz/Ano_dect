# Some Issues?

* The difference between AUC(AUROC) and ROC?

  * AUC: Area Under The Curve

  * ROC: Receiver Operating Characteristics

  * AUROC: Area Under the Receiver Operating Characteristics

  * Confusion matrix (混淆矩阵):

    |                  | Prediceted Class |                    |                    |
    | :--------------: | :--------------: | :----------------: | :----------------: |
    | **Actual Class** |                  |     Class=Ture     |    Class=False     |
    |                  |    Class=Ture    | True Positive(TP)  | False Negative(FN) |
    |                  |   Class=False    | Flase Positive(FP) | True Negative(TN)  |

    > Note: First letter means if the prediction is correct or not; Second letter means the predict result.

  * TPR (True Postive Rate, **Sensitivity** ):
    $$
    TPR = \frac{TP}{TP+FN}
    $$

    > Note: 分类器预测的正类中实际正实例占所有正实例的比例。

  * FPR（False Postive Rate）:
    $$
    FPR=\frac{FP}{FP+TN}
    $$

    > Note: 分类器预测的正类中实际负实例占所有负实例的比例。

  * TNR(Ture Negative Rate, **Specificity**):
    $$
    TNR = \frac{TN}{TN+FP}
    $$

    > Note: 分类器预测的负类中实际负实例占所有负实例的比例。

  * Recall and Precision
    $$
    Recall = TPR \\
    Precision = \frac{TP}{TP+FP} \\
    Accuracy(ACC) = \frac{TP+TN}{TP+TN+FN+FP} \\
    F-score = \frac{(a^2+1)Precision*Recall}{a^2(Precision+Recall)}
    $$

    > Note: 权重a可以调节Precision与Recall的比重，重要性程度。

  * ROC: Given some threshold, get a pairwise TPR and FPR, get a curve.

  <img src="figure/roc.jpg" alt="image-20220111174257429" style="zoom: 43%;" />

  * AUROC: Area Under the Receiver Operating Characteristics.

    

* How to compute image-level(Detection) and pixel-level(Segmentation) AUC?

  * Image-level
  
    **Reconstruction-based method** 
      &emsp;使用误差作为anomaly score，给定score阈值，得到ROC以及AUC。

    **Representation-based method**
    &emsp;使用特征提取结构提取样本的特征向量，然后利用一些非参方法，比如KDE，GDE等构造一个分布。则给定另外一个测试样本$x$，可以得到$p(x)$或者$\log p(x)$，进一步可以据此得到一个反比的anomaly score。然后给定一个socre阈值，得到ROC，最后利用插值得到AUC。

  * Pixel-level

    **Reconstruction-based method** pixel-wise reconstruction error

    $p(x)$
    
    sliding window method

* Other data partition methods for regular dataset like MNIST/CIFAR10?
  



