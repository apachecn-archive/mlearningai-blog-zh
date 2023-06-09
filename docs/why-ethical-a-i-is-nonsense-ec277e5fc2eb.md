# 为什么道德人工智能是无稽之谈

> 原文：<https://medium.com/mlearning-ai/why-ethical-a-i-is-nonsense-ec277e5fc2eb?source=collection_archive---------4----------------------->

解决人工智能偏见问题的根本方法。

![](img/fd100b994f27f4d5a1cebe117e7ceb71.png)

Image ShutterStock

众所周知，用人工智能技术构建的系统经常表现出不道德的行为。他们可能是种族主义者、性别歧视者或其他偏见者。问题不在于算法。它们只是应用数学，因此是不会被腐蚀的。但是用这些算法建立的模型是用人类创造的数据训练的。这就是偏见的来源。人类的行为往往不道德，因此人工智能表现出相应的行为并不奇怪。如果你在一个包含种族主义观点的文本语料库上训练一个自然语言处理人工智能，很明显，最终的人工智能也会变成种族主义者。为了应对这一挑战并试图拯救人工智能技术，科学家和工程师们已经开始开发各种方法来“去偏置”人工智能模型。我相信这种努力产生的系统可能是危险的，这篇文章是关于为什么。

偏见如何被引入人工智能模型的一个经过充分研究的例子是所谓的“单词嵌入”。为了能够处理语言，单词需要被翻译成实数的向量。用于实现这一点的算法(如“word2vec”)需要大量的文本数据进行训练。几年前就已经表明，这些词的嵌入经常传达种族和性别的刻板印象。还表明，建立在这种单词嵌入基础上的 NLP 人工智能系统也显示出有问题的行为(即，在招聘中使用的 CV 分析软件系统地偏向男性而不是女性)。

科学家们有许多想法如何修复这种破碎的单词嵌入。有纯数学方法(例如使用线性代数)。其他算法试图识别训练数据中导致偏差的部分，并删除或修改它们。

但是这种方法有一些基本的问题:

1.  它们可能只是表面上起作用，有些方法似乎在某种意义上起作用，因为它们减少了偏差的抽象度量。但后来可以证明，这种偏见实际上仍然存在于单词 embeddings 中，并可能对使用它们创造的人工智能产生负面影响。这是危险的，因为它给了我们一种错误的安全感，而且不能保证这种事情不会在更先进的未来方法中再次发生。
2.  它们只修复我们知道的东西
    即使单词嵌入可以消除性别偏见，它们在许多其他方面仍然是邪恶的。不幸的是，人类有无数种邪恶的方式。一个足够大的语言语料库包含了人类行为和观点的所有方面。去偏算法可能包含的误差太多了。
3.  它们让我们任由专家摆布，这种去偏置方法在数学上具有挑战性，只有少数专家能够完全理解。正常人无法评估这些方法的性能和质量。公开讨论他们的表现和问题是不可能的。
4.  它们导致不切实际的期望
    如果我们期望人工智能在伦理上是不可靠的，我们就开始相信一个虚假的上帝。我们开始将道德决策委托给专业工程师和机器，我认为这只会导致灾难。

对于人工智能偏见的问题，我提出了一个完全不同的解决方案:

1.  给每个人工智能一个单独的“脸”
    当我们遇到人时，我们可以从他们的外表和行为“计算”出一些关于他们可能是谁的统计数据。我们不自觉地知道人们的历史和背景如何影响他们的行为和思考方式。我们必须让我们的直觉也为人工智能服务。这意味着我们需要实施法律，迫使公司披露他们的人工智能是在何种数据上接受训练的。然后我们可以猜测我们面对的是什么样的人工智能“个性”。如果一个人工智能受过古典文学的训练，那么我们可以预期他是种族主义者(《鲁滨逊漂流记》)，并且对吸烟的危害一无所知。
2.  教大家永远不要完全相信人工智能
    我们已经教会了孩子们不要相信陌生人。我们应该从小就教他们同样的人工智能。人工智能不可能比人类更好，因为它是根据我们的过去训练出来的。因此人工智能将永远落后于我们。
3.  永远不要让人工智能在没有人类监督的情况下做某些决定
    这是 2 的后果。我们不让公司会计单独处理所有账目而不进行审计。我们知道，作为一个人，他可能会被诱惑转移一些钱，因此我们实施控制结构。我们应该对人工智能做同样的重要决定。人工智能永远不应该独自决定邀请哪个求职者参加面试。人工智能的这种应用必须受到法律的管制，就像我们今天有会计条例一样。
4.  利用人工智能提高认识
    提到的嵌入这个词也可以用来研究和展示我们社会固有的种族主义(例如)(这是一个不断发展的研究领域)。我相信这是人工智能提供的一个好机会！人工智能可以向我们展示我们的真实身份。

人工智能很快就会让我们人类变得非常强大。我们最好尽快为此做好准备，因为应该是我们来控制机器，而不是相反。

我们不应该试图创造神，这样我们就可以保持愚蠢。相反，我们应该努力提高自己。