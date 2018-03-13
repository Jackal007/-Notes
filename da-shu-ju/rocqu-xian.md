详细图解（原创，转载请标明出处）如下：

![](//upload-images.jianshu.io/upload_images/145616-0a7a7fd1ff77dcd9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/700)

更多参数详细信息及其意义请参考 Wikipedia -

&gt;

 \[Confusion\_matrix\]\(https://en.wikipedia.org/wiki/Sensitivity\_and\_specificity\#Confusion\_matrix\).

上图中涉及到很多相关概念及参数，详细请见Wiki上的[定义](https://link.jianshu.com?t=https://en.wikipedia.org/wiki/Sensitivity_and_specificity#Definitions)及其[混淆矩阵](https://link.jianshu.com?t=https://en.wikipedia.org/wiki/Sensitivity_and_specificity#Confusion_matrix)，这里整理肺结节识别中的几个主要参数指标如下：

* 正确率\(
  [Precision](https://link.jianshu.com?t=https://en.wikipedia.org/wiki/Precision_and_recall#Precision)
  \)：

![](http://latex.codecogs.com/png.latex?Precision=%5Cfrac%7BTP%7D%7BTP+FP%7D)

* 真阳性率\(True Positive Rate，
  [TPR](https://link.jianshu.com?t=https://en.wikipedia.org/wiki/Sensitivity_and_specificity)
  \)，灵敏度\(
  [Sensitivity](https://link.jianshu.com?t=https://en.wikipedia.org/wiki/Sensitivity_and_specificity#Sensitivity)
  \)，召回率\(
  [Recall](https://link.jianshu.com?t=https://en.wikipedia.org/wiki/Precision_and_recall#Recall)
  \)：

![](http://latex.codecogs.com/png.latex?Sensitivity=Recall=TPR=%5Cfrac%7BTP%7D%7BTP+FN%7D)

* 真阴性率\(True Negative Rate，
  [TNR](https://link.jianshu.com?t=https://en.wikipedia.org/wiki/Sensitivity_and_specificity)
  \)，特异度\(
  [Specificity](https://link.jianshu.com?t=https://en.wikipedia.org/wiki/Sensitivity_and_specificity#Specificity)
  \)：

![](http://latex.codecogs.com/png.latex?Specificity=TNR=%5Cfrac%7BTN%7D%7BFP+TN%7D)

* 假阴性率\(False Negatice Rate，
  [FNR](https://link.jianshu.com?t=https://en.wikipedia.org/wiki/False_positives_and_false_negatives#False_positive_and_false_negative_rates)
  \)，漏诊率\( = 1 - 灵敏度\)：

![](http://latex.codecogs.com/png.latex?FNR=%5Cfrac%7BFN%7D%7BTP+FN%7D)

* 假阳性率\(False Positice Rate，
  [FPR](https://link.jianshu.com?t=https://en.wikipedia.org/wiki/False_positive_rate)
  \)，误诊率\( = 1 - 特异度\)：

![](http://latex.codecogs.com/png.latex?FPR=%5Cfrac%7BFP%7D%7BFP+TN%7D)

* [阳性似然比](https://link.jianshu.com?t=https://en.wikipedia.org/wiki/Likelihood_ratios_in_diagnostic_testing#positive_likelihood_ratio) = 真阳性率 / 假阳性率 = 灵敏度 / \(1 - 特异度\)

* [阴性似然比](https://link.jianshu.com?t=https://en.wikipedia.org/wiki/Likelihood_ratios_in_diagnostic_testing#negative_likelihood_ratio) = 假阴性率 / 真阴性率 = \(1 - 灵敏度\) / 特异度

* [Youden指数](https://link.jianshu.com?t=http://baike.baidu.com/link?url=ocB5vtVDdo5gYlDxy3xlonrDGQUTZVNv3_uK3FRE30qVYsTeeXPif3fEbQSw2-IZzEoseco7zo-WVEnXM2rngLNp-e2xSej_cUfT6a3afELWFUmvrLtZIKfwMOFNCbKG) = 灵敏度 + 特异度 - 1 = 真阳性率 - 假阳性率

  


  


作者：zhwhong

  


链接：https://www.jianshu.com/p/c61ae11cc5f6

  


來源：简书

  


著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。





[争取一遍过的大喵](https://www.zhihu.com/people/fang-kun-7)

Science is just organized curiosity

10 人赞同了该回答

举个栗子，就借网上的这个栗子好了，

第一步是按照属于‘正样本’的概率将所有样本排序，如下图所示

  


![](https://pic1.zhimg.com/80/v2-77e1e16ee58697a316cfe2728be86efe_hd.jpg)

  


第二步，让我们依次来看每个样本。对于样本1，如果我们将他的score值做阈值，也就是说，只有score大于等于0.9时，我们才把样本归类到真阳性（true positive），这么一来， 在ROC曲线图中，样本1对应的[混淆矩阵](https://www.zhihu.com/question/36883196)（confusion matrix）为

  


![](https://pic1.zhimg.com/80/v2-5ba41a6e4ca9370c2f4510d5a7b70daf_hd.jpg)

  


其中，只有样本1我们看作是正确分类了（也就是我们预测是正样本，实际也是正样本）；其余还有9个实际是正样本，而我们预测是负样本的（2，4，5，6，9，11，13，17，19）；剩下的实际是负样本，我们都预测出是负样本了（也就是false positive = 0， true negative = 10）。

  


从混淆矩阵中，我们可以算出X轴坐标（false positive rate）= 0/（0+10）= 0 和Y轴坐标（true positive rate）= 1/（1+9）= 0.1，这就是下图中的第一个点

![](https://pic2.zhimg.com/80/v2-10666128633da6ea072a4c87f21d6bdf_hd.jpg)

同理我们来看样本3，它的混淆矩阵为

