# JavaScript 机器学习:第 2 部分

> 原文：<https://medium.com/hackernoon/machine-learning-with-javascript-part-2-da994c17d483>

深入监督学习🏊

![](img/306a6c3100296d79bf8ca5016422e513.png)

Petal Length vs Sepal Length by [plot.ly](http://plot.ly)

> 这是使用 JavaScript 的机器学习系列*的第 2 部分。下面是第一部分。*

*是时候了。*

*kNN 代表 **k 最近邻**，是一种监督学习算法。它可以用于分类，以及回归问题。首先，我们要向 kNN 问好，但是如果你愿意，你可以直接跳到代码。GitHub 库:[带 JS 的机器学习](https://github.com/abhisheksoni27/machine-learning-with-js)。*

## *kNN 算法是如何工作的？*

*kNN 基于数据点具有的属于同一类的最大邻居数量来决定新数据点的类。*

*如果一个新数据点的邻居如下: *NY* : **7** ， *NJ* : **0** ，中的*:**4**，那么这个新数据点的类将是 **NY** 。**

*假设你在邮局工作，你的工作是组织信件并在邮递员之间分发，以尽量减少去不同社区的次数。因为我们只是在想象，我们可以假设只有七个不同的街区。这是一种分类问题。你需要把字母分成类，这里的类指的是上东区，曼哈顿下城，等等。*

*![](img/a1301aef22db1799e2b8a3044e65ee93.png)*

*[Photo credit](https://blog.logos.com/2015/10/how-to-start-a-bible-book-study-using-logos/)*

*如果你喜欢浪费时间和资源，你可能会从每个街区给每个邮递员一封信，并希望他们在同一街区相遇并发现你的腐败计划。这是你能实现的最糟糕的分配方式。*

*另一方面，你可以根据地址的接近程度来组织信件。*

*你可以从“如果在三个街区范围内，把它交给同一个邮递员”开始那个*最近的块数*就是`**k**` 的来源。您可以不断增加块数，直到达到有效分布。对于你的分类问题，这是最有效的 k 值。*

*所以，根据一些参数，比如这里房子的地址，你分类一封信是否属于曼哈顿下城，时代广场，等等。(我不擅长记名字，所以)*

## *实践中的 kNN |代码*

*正如我们在上一个教程中所做的那样，我们将使用 ml.js 的 KNN 模块来训练我们的 kNearestNeighbors 分类器。每个机器学习问题都需要数据，我们将在本教程中使用 IRIS 数据集。*

***鸢尾数据集**包含 3 种不同类型的鸢尾(Setosa、Versicolour 和 Virginica)花瓣和萼片长度，以及表示其各自类型的字段。*

***第一步。**安装库*

```
*$ yarn add ml-knn csvtojson prompt*
```

*或者如果你喜欢`npm`*

```
*$ npm install ml-knn csvtojson prompt*
```

*`[ml-knn](https://github.com/mljs/knn)` : k 个最近邻居*

*`[csvtojson](https://github.com/Keyang/node-csvtojson)`:解析数据*

*`[prompt](https://github.com/flatiron/prompt)`:允许用户提示预测*

***第二步。**初始化库并加载数据*

*虹膜数据集由加州大学欧文分校提供，可在此处获得。然而，由于它的组织方式，你必须在浏览器中复制内容(*全选|复制*)并粘贴到一个名为 ***iris.csv.*** 的文件中。你可以随意命名，除了扩展名必须是**。csv** 。*

*现在，初始化库并加载数据。我假设你已经有一个空的 npm 项目设置，但是如果你不熟悉它，[这里有一个快速介绍。](https://docs.npmjs.com/cli/init)*

*`header names`用于可视化和理解。稍后将删除它们。*

*另外，`seperationSize`用于将数据分成训练和测试数据集。*

*酷吧。*

*我们导入了`csvtojson`包，现在我们将使用它的`fromFile`方法来加载数据。(因为我们的数据没有标题行，所以我们提供自己的标题名。)*

*我们将每一行推送到数据变量，当该过程完成时，我们将把数据集中的样本数`seperationSize`设置为**的 0.7 倍**乘以*。请注意，如果训练样本的大小太低，分类器的性能可能不会像在较大集合中那样好。**

**因为我们的数据集是按照类型排序的(`console.log`来确认)，所以`shuffleArray`函数被用来洗牌以允许分割。(如果你不洗牌，你可能会得到一个在前两个类中运行良好，但在第三个类中失败的模型。)**

**下面是它的定义。我是从在 StackO verflow 的一个回答中得知的。**

****第三步。**着装数据(又一次)**

**我们的数据组织如下:**

```
**{
 sepalLength: ‘5.1’,
 sepalWidth: ‘3.5’,
 petalLength: ‘1.4’,
 petalWidth: ‘0.2’,
 type: ‘Iris-setosa’ 
}**
```

**在将数据提供给 kNN 分类器之前，我们需要对数据做两件事:**

1.  **将字符串值转换为浮点数。(`parseFloat`)**
2.  **将`type`变成编号类。(计算机喜欢数字，你知道吗？)**

**如果你不熟悉集合，它们就像它们的数学对应物，因为它们不能有重复的元素，并且它们的元素没有索引。(与数组相反。)**

**使用`spread`操作符或 Set 构造函数可以很容易地将它们转换成数组。**

## **第四步。训练您的模型，然后测试它**

**数据已穿戴整齐，魔杖已准备就绪——除武器:**

**`train`方法接受两个强制参数，输入数据，比如花瓣长度、萼片宽度，以及它的实际类，比如 Iris-setosa，等等。它还带有一个可选的 options 参数，这只是一个 JS 对象，可以传递它来调整算法的内部参数。我们将`**k**`的值作为选项传递。`k`的默认值为 **5** 。**

**现在我们的模型已经被训练好了，让我们看看它在测试集上的表现如何。主要地，我们感兴趣的是发生的错误分类的数量。(即，它预测输入为**某物**的次数，即使它实际上是**某物*else*。)****

**误差计算如下。我们使用简单的 for 循环来遍历数据集，并查看预测的输出是否等于实际输出的 ***而不是*** 。那是一个*误分类*。**

****步骤五。(可选)开始预测****

**是时候有一些提示和预测了。**

**如果您不想在新输入上测试模型，请随意跳过这一步。**

## **第六步。嘣-肖-谢-搞定。🚀**

**如果您遵循了这些步骤，您的 index.js 应该是这样的:**

**去点燃一个终端💻，并运行`node index.js.`**

```
**$ node index.jsTest Set Size = 45 and number of Misclassifications = 2
prompt: Sepal Length:  1.7
prompt: Sepal Width:  2.5
prompt: Petal Length:  0.5
prompt: Petal Width:  3.4
With 1.7,2.5,0.5,3.4 -- type =  2**
```

**干得好。这就是你的 kNN 算法在工作，分类就像一个魔咒。💹**

**所有代码都在 Github 上:[带 js 的机器学习](https://github.com/abhisheksoni27/machine-learning-with-js)**

**kNN 算法的一个重要方面是 **k** 的值，它被称为**超参数**。超参数是 a，我从 Quora 上的[这个](https://www.quora.com/What-are-hyperparameters-in-machine-learning)答案中意译出来，“那种不能从常规训练过程中直接学习的参数。这些参数表达了模型的“高级”属性，比如它的复杂性或它应该学习的速度。它们被称为**超参数**。”**

> **k 定义了应该考虑在该地址的邻域中有多少块来对其进行分类。**

**![](img/d75e67090e5b8eddf54a2740bb07660b.png)**

**[Photo credit](http://blogs.edweek.org/teachers/prove-it-math-and-education-policy/2016/04/math-ought-to-make-sense.html)**

**我正在开发`ml-knn`模块，希望选择 k 的过程能很快自动化。**

**如果你有点兴奋，想看看这能做什么，你可以去 [**加州大学欧文分校机器学习库**](http://archive.ics.uci.edu/ml/index.php) 并在不同的数据集上使用你的分类器。(那仓库里有**。*)***

> ***要获得本系列的最新文章，请关注我的个人资料，或者你也可以放自己一马，关注我。*😄****

*****感谢阅读**！如果你喜欢，点击**绿色** **按钮❤️** 让其他人知道 **JS** 有多强大，以及为什么在机器学习方面*不应该落后于*。***

***[![](img/50ef4044ecd4e250b5d50f368b775d38.png)](http://bit.ly/HackernoonFB)******[![](img/979d9a46439d5aebbdcdca574e21dc81.png)](https://goo.gl/k7XYbx)******[![](img/2930ba6bd2c12218fdbbf7e02c8746ff.png)](https://goo.gl/4ofytp)***

> ***[黑客中午](http://bit.ly/Hackernoon)是黑客如何开始他们的下午。我们是 [@AMI](http://bit.ly/atAMIatAMI) 家庭的一员。我们现在[接受投稿](http://bit.ly/hackernoonsubmission)并乐意[讨论广告&赞助](mailto:partners@amipublications.com)机会。***
> 
> ***如果你喜欢这个故事，我们推荐你阅读我们的[最新科技故事](http://bit.ly/hackernoonlatestt)和[趋势科技故事](https://hackernoon.com/trending)。直到下一次，不要把世界的现实想当然！***

***![](img/be0ca55ba73a573dce11effb2ee80d56.png)***