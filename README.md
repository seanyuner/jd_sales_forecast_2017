# [jd_sales_forecast_2017](https://jdder.jd.com/index/jddDetail?matchId=0890e7edc3c840ea9351e9d736da1e16)


**一、简单介绍**

1. 训练数据

训练数据包含2017-04-30日之前270天之内若干店铺的每日订单量、销售额、顾客数、评价数、广告费用等数据，下架时间在2017-04-30之后或者未下架的商品数据，以及这些店铺2016年6月-2017年1月每月末后90天内的销售额。

2. 评测数据

参赛者需要对每个店铺（训练数据中涉及的全部店铺id）在2017-04-30之后90天内的总销售额进行预测。

3. 评分标准
<p align='center'>
   <img src=pics/sample_score.png>
</p>

**二、简要记录**

1. **feature_extract**,最开始*逐两月提取*（sklearn.ipynb文件内），后*逐月提取*和*逐三月提取*，共三种方案。特征基本只做了最简单的提取，没有深入分析，其中品牌（3089种）和分类（310类）进行onehot处理，共计3413个featrues(3413-3089-310=14)。

2. **visualization**，所有店和单个店，一般存在“双11”和“618”两个高峰。
<p align='center'>
   <img src=pics/sales_amt_3m_shop1148.png>
</p>

3. **训练**，主要分为使用*scikit—learn*和*xgboost*两种方案。scikit-learn尝试了regression中[大部分模型](http://scikit-learn.org/stable/supervised_learning.html#supervised-learning)，结果见下图；xgboost开始自己试着简单调了以下参数，后面主要参考[Davut Polat的调参方案](https://www.kaggle.com/c/bnp-paribas-cardif-claims-management/discussion/19083)，见下图，当然[Aarshay Jain的调参方案](https://www.analyticsvidhya.com/blog/2016/03/complete-guide-parameter-tuning-xgboost-with-codes-python/)也非常值得参考。
<p align='center'>
   <img src=pics/sklearn23_SI.png>
</p>
<p align='center'>
   <img src=pics/Davut_tuning.png>
</p>

4. **结果**，应该说训练尝试了较多的方法，也花费了很长的时间，但是过拟合比较严重，效果并不理想，这其中特征的处理应该是有较大部分原因（毕竟太懒了，时间也有限）。

5. **反思**，对于时间序列来说，取最后三个月直接作为baseline是一个不错的选择(baseline0.449.py)，事实证明也是如此（这也是最好的成绩）。另外当时也是ML刚入门，对各种算法的理解很不够，RNN就更加没有听过，也是有一些遗憾吧。
