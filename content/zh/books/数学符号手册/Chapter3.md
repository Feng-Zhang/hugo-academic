---
title: 逻辑
linktitle: 第三章 逻辑
summary: 数学符号手册，翻译至Mathematical Notation by Edward R. Scheinerman。如何表示逻辑关系。
toc: true
type: book
date: "2020-09-14T00:00:00+01:00"
draft: ture


# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 30
---



## 1. 布尔操作和证明符号

　　数学中专业词汇：_和_，_或_，_非_ 等一般都有特殊符号来表示。

- **和**。$p \wedge q$这个符号表示我们常说的“p 和q”。有时候也会用符号&表示和。
- **或**。$p \vee q$符号则表示"p 或q"。有时候也用竖线$|$表示或。
- **非**。我们常说的"非p"用$\lnot p$或$\sim p$表示。注意很多数学关系符号会在上面加右斜线表示非的意思。比如说$\not =$（不等于）、$\not \in$ （不属于）和$\not \subseteq$ （不包含）等等。
- **异或**。$p\veebar q$表示$p$或$q$但是不包含$p$和$q$的交集。有时候也会用$\oplus$符号或缩写“$XOR$或$xor$”来表示异或。
- **与非**。$p \barwedge q$表示$\lnot (p \vee q)$。缩写为"nand".
- **推出**。$a \Rightarrow b$表示如果$a$成立时那么可推出$b$，或b也成立。
- **被推出**。$a \Leftarrow b$表示$a$可由$b$推出，或如果b成立那么a也成立。
- **当且仅当**。$a\iff b$表示如果$a$成立时则$b$一定成立，而且如果$b$成立时则$a$也一定成立。通常缩写成 iff。
- **所以**。三个点$\therefore$表示所以。
- **因为**。倒立的三个点$\because$表示因为。
- **矛盾**。符号$\Rightarrow \Leftarrow$表示证明过程中有矛盾。也就是说：我们证明过程中发现相互矛盾的地方，因此这个假设是错误的。
- **证明结束**。当一个数学证明结束时，我们用方形$\square$或实方形$\blacksquare$来表示。缩写字符$QED$也可以表示“证明结束”。它是"_Quod Erat Demonstrandum_"的缩写。

---

<center> 第11页 </center>



## 2. 量词

　　数学符号$\forall$和$\exists$通常可以当作是“_经常（always）_”和“_有时（sometimes）_”的缩写。符号$\forall$是被叫作“_全称量词（universal quantifier_）”，意思是任意（for all）。例如，$\forall x \in {\Bbb R}, x^2 \geq 0$。这可以理解成：每个实数$x$都有一种属性，即$x^2$是大于0的。更通俗易懂可以理解成：所有实数的平方都会大于或者等于0。

　　符号$\exists$被称作“_存在量词（existential quantifier）_”，意思是“_至少存在一个_”。比如：$\exists x \in {\Bbb R}, x^2=2$。这句话的意思是：肯定存在一个实数，它的平方等于2。这里我们知道是指$\sqrt{2}$。

　　为了使这个注释可以发音，有些人把"such that"的缩写s.t.插入到量词注释中：$\exists x \in {\Bbb R} \ {s.t.}\ x^2 =2 $可以读成“有一个实数$x$使得$x^2=2$。

　　当$\exists$后面跟着一个感叹号，它表示有一个“_惟一_”的对象满足条件。例如：$\exists ! \in {\Bbb R},x^2=0$。这是说有一个实数，它的平方等于0，且只有惟一一个这样的实数。

　　量词可以组合起来表示更复杂的意思。比如，加法的特性是可以相互交换，可以写成这样：$\forall x \in {\Bbb R},\forall y \in {\Bbb R}, x+y=y+x$。然而，量词交换顺序会让注释很难解析。比如，$\forall x \in {\Bbb R},\exists y \in {\Bbb R}, x+y=0$ 这表示无论什么时候我们选一个实数$x$，我们都可以找一个实数$y$，使得$x+y=0$。当然，这个$y$应该是$-x$。但是$\exists y \in {\Bbb R},\forall x \in {\Bbb R}, x+y=0$ 这就是一个错误的推断，这是说存在一个魔幻数字$y$，它和任意一个实数$x$相加都等于0。

---

<center> 第12页 </center>

