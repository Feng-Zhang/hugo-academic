---
title: 合集
linktitle: 第二章 合集
summary: 数学符号手册，翻译至Mathematical Notation by Edward R. Scheinerman。如何表示合集。
toc: true
type: book
date: "2020-09-03T00:00:00+01:00"
draft: false

# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 20
---

## 1. 集合

　　集合是指一个或多个无序的且不重复的对象组成的整体。最简单的方法来指明一个集合是用花括号括起所有对象，比如：$\lbrace 1,2,7\rbrace$。这个集合由3个元素组成，数字1、2和7。元素的顺序和重复是不重要的，所以$\lbrace 2, 1, 7 \rbrace$和 $\lbrace 7,1,1,2\rbrace$是同一个集合且只有3个元素。 

　　集合中的成员用符号$\in$来表示“属于”。这个符号看起来跟希腊字母epsilon ($\epsilon$)很像，但实际上是不同的。因此$x \in A$是表明元素$x$是集合$A$的成员。例如：$2 \in \lbrace 1,2,7\rbrace$。符号$\notin$表示不属于，就像$2 \notin \lbrace1,2,7\rbrace$。当符号$\in$反向写$\ni$表示“包含”，比如$A \ni x$。这和$x \in A$是一个意思。例如$\lbrace1,2,7\rbrace \ni 7$。

　　集合不包括任何元素被称为空集或零集。我们可以用符号$\emptyset$或$\varnothing$，或空的花括号$\lbrace \rbrace$表示。这些符号中$\varnothing$ 表达的是最清楚的。

　　大集合很可能用少量元素加代表类似模式的省略号（$\ldots$）来表示。这对于表示有固定模式的无限集合和有限集合都很浅显易懂。比如：$\lbrace1,2,3,\ldots,100\rbrace$很明确地表示整数1到100，而$\lbrace2,4,6,\ldots\rbrace$则表示大于0的偶数集合。

　　然而，一个更准确的描述集合的方法是使用集合建构式符号（set builder notation）。这种注释格式是这样的：$\lbrace x\in \Bbb Z:1 \leq x \leq 100 \rbrace$。这个字母$x$是一个虚拟变量，它是用来代表这个集合的元素的名称。接着$\in \Bbb Z$意思是这个集合的元素来自正整数。然后用冒号间隔，后面接一个条件，它告诉我们哪些正整数在这个集合里。在这个例子中，它们是1到100的正整数。

　　有时候冒号会用竖线$|$代替，比如$\lbrace u \in \Bbb Z | u \geq 100\rbrace$，这表示集合是大于100的正整数。

---

<center> 第5页 </center>

　　冒号后面的条件也可以用词语表示。比如$\lbrace a \in \Bbb Z: a能被5整除\rbrace$，这代表集合$\lbrace\ldots,-15,-10,-5,0,5,10,15,\ldots\rbrace$。

　　如果上下文清晰，集合建构式符号是可以省略冒号的左边。$\lbrace n:n>5\rbrace$，这个表达的就不清楚，它是指所有大于5的实数还是指大于5的正整数呢？

　　当然冒号左边也可以更复杂的表达式。比如$\lbrace(x,y):x+y=5\rbrace$代表了一个集合对，它包括元素$(2,3)$但是不包括$(4,4)$。

　　此外，集合中有多种多样的关系和操作符，这里列举一些最常见的：

- **集合相等**。如果有集合集合$A$和集合$B$，$A=B$意味着集合$A$和$B$有相同的元素。

- **子集**。如果有集合$A$和集合$B$，$A \subseteq B$意思是每个属于A的元素也是集合B的元素。有些书中可能会简单地写$A \subset B$。这个意思是A是B的子集但是不相等。$\subset / \subseteq$和$</\leq$是比较类似的意思，但是在集合中不用小于号。此外，注意$A \subseteq B$与$A\in B$表达的并不是同一个事。

- **超集**。$A \supseteq B$就是$B \subseteq A$。也就是说A的元素包含了B的元素。

- **并集**。如果有集合$A$和集合$B$，$A \bigcup B$表示元素属于A或B或两者共有。例如$\lbrace1,2,3\rbrace\bigcup \lbrace2,4,6\rbrace=\lbrace1,2,3,4,6\rbrace$。有很多种方式表示两个集合不相交。常见的有$+,\bigoplus,\biguplus$。不相交这个注释表达了两层意思。首先两个集合不相交，即没有元素同时属于两个集合。第二，它是集合的并集。比如，$A_1 \biguplus A_2 \biguplus \ldots \biguplus A_n =B$，这表示1）对于所有$i\neq j$时$A_i \cap A_j = \emptyset$，2）集合$A_1,A_2,\ldots,A_n $的并集是$B$。

- **交集**。如果有集合$A$和集合$B$，$A \bigcap B$表示一个集合，它的元素同时属于$A$和$B$。例如$\lbrace 1,2,3 \rbrace \bigcap \lbrace 2,4,6 \rbrace = \lbrace 2 \rbrace$。

  ---

  <center> 第6页 </center>

- **差集**。如果有集合$A$和集合$B$，$A-B$则表示这个集合的所有元素属于A但是不属于B。例如$\lbrace 1,2,3 \rbrace - \lbrace 2,4,6 \rbrace = \lbrace 1,3 \rbrace$。有人也会用$A \setminus B$来表示并集，与普通的减号区分开。

- **补集**。集合$A$的补集写成$\overline A$。它表示一个集合，且其元素不属于$A$。我们要根据上下文来理解这个注释。例如：如果谈论整数，$X$表示奇数集合，那么$\overline X$表示偶数集合，而不是表示除奇数外的所有实数或复数。通常，最好用$\Bbb Z - X$来表示$X$以外的集合。

- **对称差**。如果有集合$A$和集合$B$，$A \triangle B$表示一个集合且它的元素属于$A$或$B$但不属于它们俩共有的。例如$\lbrace 1,2,3 \rbrace \triangle \lbrace 2,4,6 \rbrace = \lbrace 1,3,4,6 \rbrace$。我们可知$A \triangle B = (A \bigcup B)-(A \bigcap B)=(A-B) \bigcup (B-A)$。

- **势**。如果$A$是一个集合，那么$|A|$表示$A$的元素个数，有时也会用#$A$来表示。例如，如果集合$A = \lbrace 1,2,4 \rbrace$，那么$|A|=3$。

- **笛卡尔乘积**。集合$A$和集合$B$的笛卡尔乘积为$A \times B = \lbrace (a,b):a \in A,b\in B \rbrace$。例如$\lbrace 1,2,3 \rbrace \times \lbrace 3,4 \rbrace = \lbrace (1,3),(1,4),(2,3),(2,4),(3,3),(3,4) \rbrace$。符号$A^2$表示$A \times A$，即所有的有序元素对$(x,y)$，其中$x,y \in A$。当$n$是正整数时，$A^n$则表示一个集合，它的每个元素是长度为n的有序**列表**。

- **幂集**。集合$A$的幂集是指元素为A的所有子集的集合。通常用$2^A$或$\mathcal P(A)$。例如，如果$A=\lbrace 1,2,3 \rbrace$，那么$\mathcal P(A)=2^A=\left \lbrace \lbrace 1,2,3 \rbrace,\lbrace 1,2\rbrace,\lbrace 1,3 \rbrace,\lbrace 2,3 \rbrace,\lbrace 1 \rbrace,\lbrace 2 \rbrace,\lbrace 3 \rbrace,\emptyset \right \rbrace$。

- **设定幂**。如果有集合$A$和集合$B$，$B^A$表示一个集合，且它的元素是从A到B的所有函数（这个没看明白什么意思？），即$B^A = \lbrace f | f:A \to B\rbrace$。第25页有它的扩展$f:A \to B$。这个如果集合$A$和集合$B$是有限的，那么$|A|=a$和$|B|=b$，那么有$b^a$个函数从A到B，$|B^A|=|B|^{|A|}$。

  ---
<center> 第7页 </center>


- **最大值和最小值**。如果集合A是一个实数集合，那么max A表示集合A中最大的那个元素，min A则表示集合A中最小的那个元素。一般用楔形和V形符号来表示，如$x \wedge y = max \lbrace x,y \rbrace $和$x \vee y = min \lbrace x,y \rbrace$。不过并不是所有的集合都一定有最大值和最小值。与之相关的概念是上确界和下确界，分别用sup A和inf A来表示。

## 2. 列表

　　数学领域中，列表是指一个有序的对象集，对象的重复是有意义的。列表通常是用括号括起来，尽管有时候会使用中括号。例如$(1,2,2,3)$是一个列表。而列表$(1,2,2,3), (1,2,3)$和$(2,1,2,3)$是三个不同的东西，因为这三个列表的元素顺序和个数是不同的。

　　一个有n个元素的列表有时也被称为一个n元组。

　　当我们用$a$来指代一个列表，那么列表的元素通常被命名为$a_1,a_2$等等。

## 3. 累加和累乘等

　　符号$\sum$和$\prod$的意思分别是累加和累乘。典型的累加注释有这样的格式：$\sum_{j=start}^{stop} {expression\ involving\ j}$。这里$j$是一个虚拟变量。比如：$\sum_{j=1}^5{x^j}=x^1+x^2+x^3+x^4+x^5$。如果累加的目标是无限大，这意味着这个累加会一直持续下去没有尽头：$\sum_{n=0}^{\infty}{\frac{1}{2^n}}=1+\frac 1 2 +\frac 1 4+\frac 1 8 +\frac 1 {16}+\ldots$。

　　符号$\prod$与$\sum$类似，不同的是运算符是乘法。例如$\prod_{j=0}^5(2j+1)=1\times 3\times 5\times 7\times 9\times 11$。

---

<center> 第8页 </center>

　　上面的例子中，下标（虚拟变量）是连续不间断的正整数。但是如果我们希望累加的下标是其它形式的怎么办？例如，当$A$是集合$\lbrace 1,5,6,22 \rbrace$，然后$\sum_{t \in A}{t^2}=1^2+5^2+6^2+22^2$。

　　当然，下标也可以是简单的英文描述。例如：

$$
\begin{smallmatrix}\prod_{p\ prime}{(1-\frac{1}{p})}=(1-\frac 1 2)\times(1-\frac 1 3)\times(1-\frac 1 5) \times(1-\frac 1 7)\times(1-\frac 1 {11})\times {\cdots}\end{smallmatrix}
$$


　　有时候累加表达式可能不会显式地展示出上下标，即没有虚拟变量和上下限。这种情况下，通常重复的那个变量是上标或下标。比如说，你看出这样的表达式：$\sum{\binom{n}{k}}x^k$，那么$k$很可能是下标。我们得根据上下文推测$k$的范围。在这个例子中，由于二项式$\binom{n}{k}$的定义，那么$k \geq 0$，如果$k >n$的话整个二项式为0，所以可以得出$k$的范围是从0到$n$。通常，如果没有显式地标出上下限，那么默认要穷尽所有的范围。例如，当A是一个$n\times m$的矩阵，B是一个$m\times p$的矩阵，那么$\sum{a_{i,j}}{b_{j,k}}$意味着虚拟变量$j=1,2,3,\ldots,m$。

　　在某些情况下，如使用爱因斯坦求和约定时，为了方便，写累加表达式的时候会省略$\sum$符号。任何情况下上下标的虚拟变量被重复使用时，我们要对那个变量进行累加。例如，表达式$a_{i,j}b_j$的意思是$\sum_j{a_{i,j}}b_j$，我们需要在$j$的取值范围内进行累加。

　　按照这种约定，当A是一个方阵时，那么$a_{i,i}$指的是矩阵A的迹，即对角线上所有元素之和。对于合适的矩阵A和B，$a_{i,j}b_{j,k}$是指$AB$的第$i$行第$k$列的元素。

　　其它运算符也会使用类似于$\sum$和的注释。例如，当$A_1,A_2,A3,\ldots$是集合时，它们的并集可以写成：$\bigcup_{i=1}^{\infty}A_i$，这是指$A_1 \bigcup A_2\bigcup A_3\bigcup \ldots$。当然$\bigcap_{i=1}^{\infty}$是指它们的交集。

---

<center> 第9页 </center>

　　如果操作符太多的话，一般都会写成虚拟变量的形式。例如，当$p_1,p_2,\ldots,p_n$是逻辑值(真或假)时，$\wedge_{i=1}^n{p_i}$是指$p_1 \wedge p_2 \wedge \ldots \wedge p_n$。

---

<center> 第10页 </center>

