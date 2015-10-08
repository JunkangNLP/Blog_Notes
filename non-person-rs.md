title: 非个性化推荐
date: 2015-09-29 09:40:34
tags: [推荐系统]
categories: 算法
---

### <font color="#32CD99"> 非个性化推荐 </font> ###

  [stackoverflow](http://stackoverflow.com/), [知乎](http://zhihu/com/) 等等网站都有投票机制，单一的按投票排序也许对于充分展示答案没有提供比较大的帮助，此文主要介绍非个性化推荐的主流排序以及其中存在的一些缺陷。当然用户的喜好(Preference)有显式(explicit)和隐式(implicit)两种，显式包括打分(rating)，评价(review)和投票(vote)等等，隐式包括点击(click)，购买(purchase)和关注(follow)等等。这里讨论的主要是显式的表达方式。

### <font color="#32CD99"> 预测和推荐 </font> ###

  打分有很多种，比如亚马逊和豆瓣的星级评分(star rating)，知乎和微博的投票点赞机制。这里的推荐就是预测(predict)物品的受欢迎程度和做排序(recommend)。预测可以具体表示你喜欢这个物品的程度，推荐就是列出一系列你可能喜欢的物品。
  #### 预测(predictiction) #### 


  ##### 1.  <font color="green">投票人数占总购买人数的比例来表示物品的受欢迎程度:  </font> #####
  *  无法知晓投票人是否喜欢这个物品
  *  无法知道这个物品是否受欢迎  


  ##### 2.  <font color="green">点赞数量  </font> #####
  *  显示了是否受欢迎(popularity)
  *  没有显示 downvote，无法看到争议  


  ##### 3.  <font color="green">大于4颗星的评分比例  </font> #####


  ##### 4.  <font color="green">所有评分的分布  </font> #####


  #### 推荐(recommendation) ####


  ##### 1.  <font color="green">推荐不能以分数作为排序(rank by score)</font> #####

  *  数据太少，如果只有一个5星
  *  不同人评分维度不同
  *  相关领域的考虑，(物品过时，不流行了)


  ##### 2.  <font color="green">推荐需要考虑的方面</font> #####

  *  物品是流行的，符合结果的置信区间
  *  风险的承担，保守还是激进、高风险高收益
  *  相关领域考虑，推荐系统的目的是什么、受众人群特征等等。


  ##### 3.  <font color="green">Damped Means</font>  ##### 

  Damped Means 可以克服数据量比较小的时候，平均分数并不客观的缺点。 
      $$\frac{\sum \_{u}r\_{ui}+k\mu}{n+k}$$ 
      u = 用户, i = 物品, r = 分数, n = 打分人数, k = 控制力度(control strength) 
      

  ##### 4.  <font color="green">Hacker News 网站的排序算法。</font>##### 

  Hacker News 只显示用户赞成票数，主要考虑时间因素对于排序的影响。
      $$\frac{P-1}{(T+2)^{G}}$$
      P = 投票数, T = 时间, G = 重力因素(Gravityth power，default:1.8)
      

  ##### 5.  <font color="green">Reddit 网站的排序算法。</font>#####

  Reddit 每个帖子会有向上和向下的箭头，代表了赞成和反对的票数，从上面的公式看(赞成票为1，反对票为0)会比(赞成票1000, 反对票1000)排名靠前，因此 Reddit 会将受大众欢迎的帖子排在前面，有争议的帖子排在后面。z是赞成和反对票的差额，如果是0则赋值为1。y是如果赞成票多于反对票则是1，反正为-1，相等为0。t是时间。
      $$Score=log\_{10}z+\frac{yt}{45000}$$
    
      
  ##### 6. <font color="green">Wilson Interval</font> #####

  不考虑时间因素，通常两个<font color="red">错误</font>。
  1)  得分 = 赞成票 - 反对票

      (550 - 450 = 100) > (60 - 40 > 20), 但是就好评率来说 40/100 > 450/1000

  2)  得分 = 赞成票 / 总票数

      2/2 > 100/101, 这个显然有问题，amazon.com 有犯过这样的错误。
      
      1. 计算好评率(赞成票比例)
      2. 根据好评率计算置信区间(比如以95%的概率)
      3. 根据置信区间的下限值排序。
      这里的置信区间就是 Wison Interval, 见参考文献链接。



参考文献:
*  [Recommedation System(Coursera)](https://www.coursera.org/learn/recommender-systems/home/welcome)
*  [基于用户投票的排名算法](http://www.ruanyifeng.com/blog/search.html?cx=016304377626642577906%3Ab_e9skaywzq&cof=FORID%3A11&ie=UTF-8&q=%E5%9F%BA%E4%BA%8E%E7%94%A8%E6%88%B7%E6%8A%95%E7%A5%A8%E7%9A%84%E6%8E%92%E5%90%8D%E7%AE%97%E6%B3%95&sa.x=0&sa.y=0)
*  [Wison Interval](https://en.wikipedia.org/wiki/Binomial_proportion_confidence_interval)
     
      