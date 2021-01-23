# 第一章 好的推荐系统

## 1.1 什么是推荐系统

推荐系统的基本任务是联系用户和物品，解决信息过载的问题。

## 1.2 个性化推荐系统的应用

和搜索引擎不同，个性化推荐系统需要依赖用户的行为数据，因此一般都是作为一个应用存在于不同网站中。

总的来说，几乎所有的**推荐系统**应用都是由<u>**前台的展示页面**</u>、<u>**后台的日志系统**</u>以及<u>**推荐算法系统**</u>。

### 1.2.1 电子商务

如亚马逊的个性化推荐系统，实现“千人千面”，让每个用户都能拥有一个自己的在线商店，并且能在商店中找到自己感兴趣的商品。

功能点：cross selling打包售卖，基于第三方登录用户喜爱推荐商品等。

### 1.2.2 电影和视频网站

如Netflix等电影推荐界面包括：

+ 电影的标题和海报
+ 用户反馈模块——包括play播放、评分和NOt Interested不感兴趣3种
+ 推荐理由——因为用户曾经喜欢过别的电影

## 1.3 推荐系统评测

评测推荐系统时，我们可以从以下角度进行：准确度、覆盖度、新颖度、惊喜度、信任度、透明度等。这些指标中，有些可以离线计算，有些只有在线才能计算，有些只能通过用户问卷获得。



### 1.3.1 推荐系统实验方法

在推荐系统中，主要有3种评测推荐效果的实验方法，即离线实验（offline experiment）、用户调查（user study）和在线实验（online experiment）。

1. 离线实验

  离线实验的方法由如下几个步骤构成：

  + 通过日志系统获得用户行为数据，并按照一定格式生成一个<u>标准的数据集</u>；
  + 将数据集按照一定的规则分成<u>训练集和测试集</u>；
  + 在训练集上训练用户兴趣模型，在测试集上进行预测；（一个数据集进行模型训练，一个数据集用来预测）
  + 通过事先定义的<u>离线指标</u>评测算法在测试集上的预测结果。（对预测结果进行评分）

  离线实现的优缺点：

|            优点             |                     缺点                     |
| :-------------------------: | :------------------------------------------: |
| 不需要 有对实际系统的控制权 | 无法计算商业上关心的指标（如点击率，转化率） |
|     不需要用户参与实验      |       离线实验的指标和商业指标存在差距       |
|  速度快，可以测试大量算法   |                                              |

  

2. 用户调查

   优点：可以获得很多体现用户主观感受的指标，相对在线实现风险很低，出现错误很容易弥补。

   缺点：1/招募测试用户代价较大，很难组织大规模的测试用户，因此会使测试结果的统计意义不足。2/用户在测试环境和真实环境的行为可能有所不同。

3. 在线实验

   AB test：

   AB测试的缺点：

   1/周期比较长，必须进行长期的实验才能得到可靠的结果。

   2/复杂度高，一个大型网站的架构分前端和后端，从前端界面到最后端端算法，中国南京爱你往往经过很多层。

   

一般来说，一个新的推荐算法最终上线，需要完成3个实现：

+ 首先，需要通过实现实现证明它在很多离线指标上优于现有算法
+ 然后，通过用户调查确定它的用户满意度不低于现有算法
+ 最后，通过在线AB测试确定它在我们关心的指标上优于现有算法。



### 1.3.2 评测指标

1. 用户满意度

   可以通过用户点击率、停留时间和转化率等指标度量用户的满意度。

2. 预测准确度

   预测准确度是度量一个推荐系统或推荐算法预测用户行为的能力。这个指标是最重要的推荐系统离线评测指标。

   在计算该指标时需要有一个离线的数据集，该数据集包含用户的历史行为记录。然后，将该数据集通过时间分成训练集和测试集。最后在训练集上建立用户的行为和兴趣模型预测用户在测试集上的行为，并计算预测行为和测试集上实际行为的重合度作为预测准确度。

   + 评分预测

     如果知道了用户对物品的历史评分，就可以从中习得用户的兴趣模型，并预测该用户在将来看到一个他没有评分的物品时，会给这个物品评多少分。

   + Top N推荐

     网站在提供推荐服务时，一般是给用户一个个性化的推荐列表，这就是TopN推荐。

   + 关于评分预测和TopN推荐的讨论

     从实用性来看，TopN推荐能为用户推荐更多想看的电影，而不是预测评分，实际情况，即使有些电影用户会给高分，但用户看的可能性非常小。

3. 覆盖率

   coverage描述一个推荐系统对物品长尾的发掘能力。

4. 多样性

   多样性描述了推荐列表中物品两两之间的不相似性。因此多样性和相似性是对应的。

5. 新颖性

   新颖的推荐是指给用户推荐那些他们以前没有听说过的物品。通过牺牲精度来提高多样性和新颖性是很容易的，而困难的是如何在不牺牲精度的情况下提高多样性和新颖性。

6. 惊喜度

   如果推荐结果和用户的历史兴趣不相似性，但却让用户觉得满意，那么就可以说推荐结果的惊喜度很高，而<u>推荐的新颖性仅仅取决于用户是否听说过这个推荐结果</u>。

7. 信任度

   如果用户信任推荐系统，那就会增加用户和推荐系统的交互。

   如在电商推荐系统中，同样的推荐结果，以<u>让用户信任的方式推荐给用户就更能让用户产生购买欲</u>，而以类似广告形式的方法推荐给用户就可能很难让用户产生购买的意愿。

   提高推荐系统信任度的方法：

   + 增加推荐系统的透明度（transparency），而增加推荐系统透明度主要办法是提供推荐解释。只有让用户了解推荐系统运行机制，让用户认同推荐系统的运行机制。
   + 考虑用户的社交网络信息，利用用户的好友信息给用户做推荐。

8. 实时性

9. 健壮性

   任何一个能带来利益的算法系统都会被人攻击，这方面最典型的例子就是搜索引擎。


   算法健壮性的评测主要利用**模拟攻击**。首先，给定一个数据集和一个算法，可以用这个算法给这个数据集中的用户生成推荐列表。然后，用常用的攻击方法向数据集中注入**噪声数据**。然后利用算法在注入噪声的数据集上再次给用户生成推荐列表。最后，通过比较攻击前后推荐列表的相似度评测算法的健壮性。

10. 商业目标

    设计推荐系统时需要考虑最终的商业目标。









## Welcome to GitHub Pages

You can use the [editor on GitHub](https://github.com/charlesliuc63/test/edit/gh-pages/index.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/charlesliuc63/test/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://support.github.com/contact) and we’ll help you sort it out.
