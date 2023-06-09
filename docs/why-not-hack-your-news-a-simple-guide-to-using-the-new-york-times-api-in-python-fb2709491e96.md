# 为什么不黑掉你的新闻？Python 中使用纽约时报 API 的简单指南

> 原文：<https://medium.com/mlearning-ai/why-not-hack-your-news-a-simple-guide-to-using-the-new-york-times-api-in-python-fb2709491e96?source=collection_archive---------4----------------------->

## 无论你是在寻找一个有趣的研究项目，还是厌倦了滚动——这个工具正是你所需要的

![](img/ab736e26ddb6e699a5e48cca677a71e2.png)

Photo by [Jakayla Toney](https://unsplash.com/@jakaylatoney?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

《纽约时报》是全球最知名、最受信赖的报纸之一。这是一个很好的资源来了解最新的政治，浏览电影评论，或者试试你的运气对他们的商业新闻做一些自然语言处理。

如果我告诉您，您可以使用纽约时报 API 从纽约时报网站获取所有这些数据，会怎么样？下面是怎么做的。

## 第一步:在纽约时报开发者平台上创建一个账户

![](img/089bf1229058c812b5470e905ef96bfd.png)

首先你需要在[纽约时报开发者平台](https://developer.nytimes.com/accounts/create)上做一个账号。幸运的是，这是完全免费的。

创建帐户后，点击屏幕右上角的电子邮件地址，在下拉菜单中选择“应用程序”。现在，选择蓝色的“+新应用”图标，给你的新应用命名。

有两个部分值得一提。首先，向下滚动到 APIs *部分。你可以在这里看到，纽约时报 API 有许多不同的功能，你可以为你的应用程序启用或禁用:关于热门故事的数据，最多人观看或分享的文章，书籍和电影评论以及畅销书排行榜，文章元数据或 NYT 档案。出于演示的目的，本文中我将只关注**文章搜索**特性。如果您想继续学习本教程，请确保您启用了此功能。

一旦你启用了**文章搜索**功能，回到 API 密匙部分，复制你的 API 密匙。

## 步骤 2:设置您的 Python 脚本

为了能够访问 Python 中的 API，需要使用 Python 模块 [*pynytimes*](https://pypi.org/project/pynytimes/) *。*您可以通过在命令行中键入:

```
pip install pynytimes
```

当您安装了 *pynytimes* 之后，您需要导入该模块。您可以通过在 Python 脚本的顶部键入以下内容来实现这一点:

现在，您需要设置您的 API。还记得我们在上一节中创建的 API 键吗？复制您的密钥，并将其插入到您的代码中(括号只是一个占位符，不要在您的代码中使用):

恭喜你！您现在已经成功地设置了纽约时报 API！那很容易，不是吗？

## 步骤 3:编写第一个查询

现在有趣的部分可以开始了。使用文章搜索 API，我们可以搜索纽约时报网站上当前列出的所有文章，并根据关键字、标题、出版日期、位置、来源、新闻台等进行过滤。让我们首先构建一个简单的查询来提取 2020 年发表的包含关键字“气候变化”的所有观点:

请注意，“来源”、“新闻服务台”和“出版日期”并不是筛选搜索的唯一方式。[API 文档](https://developer.nytimes.com/docs/articlesearch-product/1/overview)提供了关键字和可能值的综合列表，包括材料类型、地理位置、文档类型、作者等等。

## 步骤 4:为分析准备好数据

我们现在已经成功地从网站上检索到了我们感兴趣的文章。然而，输出是嵌套列表和字典的组合——仍然有些晦涩，并且不太用户友好。还包括很多我们不感兴趣的数据。在这一节中，我将展示如何检索我们想要的信息，将它们存储为 pandas 数据框，并以 excel 或 CSV 格式导出它们。

让我们看看查询输出的结构。这是一个包含多个(在某些情况下是嵌套的)词典的大列表。为了提取相关信息，我使用了*地图功能。这个函数允许我在一个列表的任何元素上执行一个给定的函数。这是从嵌套字典或列表中检索信息的一个极好的特性。*λ函数*检索我感兴趣的查询输出元素的字典值:*

*地图函数*返回一个地图对象。要将数据输入数据框，我们仍然需要将它们转换成列表:

数据也可以导出为选择的格式:

整个代码可以在[这里](https://github.com/evadrichter/nyt_api)访问。