# Algorithm For Decision Making

## 4. Parameter Learning

### 4.2 Bayesian Parameter Learning

#### 4.2.2 Bayesian Learning for Categorical Distributions ◎

### 4.3 Nonparametric Learning

### 4.4 Learning with missing data

#### 4.4.1 Data Imputation

#### 4.4.2 Expectation-Maximization

## 5 Structure Learning

### 5.1 Bayesian Network Scoring

p98
Finding the G

式(5.2)を最大化するGを見つけることは、ベイズスコアと呼ばれるものを最大化するGを見つけることと同じである

The Bayesian score

ベイズスコアは、小さな数を掛け合わせるより、小さな数の対数を足し合わせる方が簡単なので、数値的に計算する方がより便利である．多くのソフトウェア・ライブラリはガンマ関数の対数を直接計算することが可能である．

A variety

様々な事前分布のグラフが検討されてきたが，単一事前分布はしばしば実用で利用され，式5.5におけるBayesianスコアの計算からlogP(G)が除外することができる．

Algorithm 5.1 provides

Algorithm5.1 が実装を与えている．

Algorithm 5.1. An algorithm

変数のリスト vars，データ Dが与えられたGparh Gに対して，Bayesianスコアを計算する．

This method
algorithm4.2によって生成されたように，すべてのi, j, kについて aijk = 1 であるような単一事前分布をこの手法では利用する．

The loggamma

loggamma 関数は，SpecialFunctions.jlによって提供される，

Chapter4

4章では，statistics, prior関数を導入しました．

Note that 

以下の2つの等式が成り立つことに注意してください．


A by-product

ベイズスコアに関して構造を最適化する副産物として、利用可能なデータがある場合、モデルの複雑さの適切なバランスを見つけることができるようになります。

We do not

変数間の重要な関係を捉え損ねるようなモデルは避けたいが、パラメータが多すぎて限られたデータから十分に学習できないようなモデルも避けたい。

### 5.2 Directed Graph Search

To illustlate

モデルの複雑性のバランスをとるために，Bayesianスコアがどのように役立つのか，示すために図5.1について考える．

The value of

Aの値は，Bに弱い影響を与えるが，Cは他の変数から独立している．

p105


Algorithm 5.4 A method

p106

Instead of searching the space of directed acyclic graphs, we can search the space of Markov equivalence classes represented by partially directed graphs.

有向無サイクルグラフの空間を探索する代わりに、部分有向グラフで表現されるマルコフ同値類空間を探索することができる。

※9 この空間の探索方法の参考文献

Although the space of Markov equivalence classes is, of course, smaller than the space of directed acyclic graphs, it is not significantly smaller; the ratio of directed acyclic graphs to equivalence classes asymptotes to around 3.7 fairly quickly.

もちろんマルコフ同値類空間は有向無サイクルグラフ空間より小さいが、著しく小さいわけではなく、有向無サイクルグラフと同値類の比率はかなり早く3.7程度に漸近している。

※10 マルコフ同値類や無サイクルグラフのサイズの分散：参考文献

A problem with hill climbing in the space of directed acyclic graphs is that the neighborhood may consist of other graphs that are in the same equivalence class with the same score, which can lead to the search becoming stuck in a local optimum. Searching the space of equivalence classes allows us to jump to different directed acyclic graphs outside the current equivalence class.

有向無サイクルグラフ空間におけるHill Climbing の問題点は、近傍が同じスコアで同値類に属する他のグラフで構成されている場合があり、探索が局所最適に陥ってしまうことである。同値類空間を探索することで、現在の同値類外の異なる有向無サイクルグラフにジャンプすることができる。(局所最適解で停止することを防ぐ)

Any of the general search strategies presented in section 5.2 can be used. If a form of local search is used, then we need to define the local graph operations that define the neighborhood of the graph. Examples of local graph operations include:

5.2節で紹介した一般的な探索手法のいずれも使用可能である。局所探索の形式を用いる場合、グラフの近傍を定義する局所グラフ操作を定義する必要がある。局所的なグラフ操作の例としては

If an edge between X and Y does not exist, add either X − Y or X → Y.

ノードX,Yの間の辺が存在しない場合，X,Yを結ぶ辺または，X->Yへの有向辺を追加する．

If X − Y or X → Y, then remove the edge between X and Y.

X − Y or X → Yであれば，X,Y間の辺を取り除く

If X → Y, then reverse the direction of the edge to get X ← Y.

X → Yであれば，有向辺の向きを逆にすれば，X ← Y となる．

If X − Y − Z, then add X → Y ← Z.

X - Y - Z(X,Y,Z間に無向辺が存在)であれば，X → Y ← Z を追加する．

To score a partially directed graph, we generate a member of its Markov equivalence class and compute its score.

部分有向グラフをスコアリングするために、そのマルコフ同値類のメンバーを生成し、そのスコアを計算する。


### 5.5 Summary

- Fitting a Bayesian network to data requires selecting the Bayesian network structure that dictates the conditional dependencies between variables.

データにベイジアンネットワークをFittingするには、変数間の条件の依存関係を規定するベイジアンネットワークの構造を選択する必要がある。

- Bayesian approaches to structure learning maximize the Bayesian score, which is related to the probability of the graph structure given a data set.

構造学習に対するベイズアプローチは、データセットが与えられたときのグラフ構造の確率に関係するベイズスコアを最大化する。

- The Bayesian score promotes simpler structures for smaller data sets and supports more complicated structures for larger data sets.

ベイズスコアは、小さなデータセットにはよりシンプルな構造を、大きなデータセットにはより複雑な構造をサポートする。

- The number of possible structures is superexponential in the number of variables, and finding a structure that maximizes the Bayesian score is NP-hard.

可能な構造の数は変数の数に対して超指数的であり、ベイズスコアを最大化する構造を見つけることはNP困難である。 

- Directed graph search algorithms like K2 and local search can be efficient but do not guarantee optimality.

K2や局所探索のような有向グラフ探索アルゴリズムは効率的であるが、最適性を保証するものではありません。

- Methods like partially directed graph search traverse the space of Markov equivalence classes, which may be more efficient than searching the larger space of directed acyclic graphs.

部分有向グラフ探索のような方法は、マルコフ同値類空間をtraverseするので、より大きな有向無サイクルグラフの空間を探索するよりも効率的かもしれません。

## 6 Simple Decisions

This chapter introduces the notion of simple decisions, where we make a single decision under uncertainty.

この章では、不確実性の下で一つの決定を下す、simple decisionsの概念を紹介する。

※1  Simple decisions are simple compared to sequential problems, which are the focus of the rest of the book. Simple decisions are not necessarily simple to solve, though.

Simple Decisions は，本書の残りの部分で焦点を当てているSequentialな問題と比べてシンプルです．
しかし，Simple Decisionsは必ず解けるほど，単純な問題ではありません．

We will study the problem of decision making from the perspective of utility theory, which involves modeling the preferences of an agent as a real-valued function over uncertain outcomes.

我々は，意思決定問題をUtlity Theoryの観点に基づいて研究している．

(Utility Theory：効用理論は、個人の観察された行動や選択を説明しようとする理論である)

Utility Theoryでは，エージェントの選択を不確実な結果に対する実数地関数としてモデル化している．

※2 Utility Theory の参考文献

This chapter begins by discussing how a small set of constraints on rational preferences can lead to the existence of a utility function.

合理的な選択に対する，小さな制約の集合が，どのようにしてUtility Functionの存在を導くことができるのか，を本章のはじめに議論する．

This utility function can be inferred from a sequence of preference queries.

この効用関数は一連のpreferenceの問合せから推測することができる。

We then introduce the maximum expected utility principle as a definition of rationality, a central concept in decision theory that will be used as a driving principle for decision making in this book.

次に、合理性の定義として，Maximum expected utility principleを紹介する．
合理性は，本書で意思決定の駆動原理として利用されている．

※3 Decision Making 参考文献

We show how decision problems can be represented as decision networks and show an algorithm for solving for an optimal decision.

意思決定問題がどのように意思決定ネットワークとして表現されるかを示し、最適な意思決定を解くためのアルゴリズムを示す。

The concept of value of information is introduced, which measures the utility gained through observing additional variables.

また、追加的な変数を観測することによって得られる効用を測定する情報価値という概念を導入する。

The chapter concludes with a brief discussion of how human decision making is not always consistent with the maximum expected utility principle.

本章の最後に、人間の意思決定がMaximum expected utility principle と必ずしも一致しないことを簡単に説明する。

### 6.1 Constraints on Rational Preferences

We began our discussion on uncertainty in chapter 2 by identifying the need to compare our degree of belief in different statements.

第2章では、不確実性の議論を始めるにあたり、異なる記述に対する信憑性の度合いを比較する必要性を指摘した。

This chapter requires the ability to compare the degree of desirability of two different outcomes.

この章では、2つの異なる結果の望ましさの度合いを比較する能力が必要である。

We state our preferences using the following operators:

我々は，次のような演算子を利用し，preferencesを述べています．





