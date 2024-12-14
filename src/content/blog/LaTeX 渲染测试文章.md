---
title: LaTeX 渲染测试文章
pubDate: 2023-08-31 13:47:18
tags:
  - 记录
  - 年记
categories:
  - tech
description: 仅用于测试博客框架是否对 LaTeX 支持完备
image: https://images.weserv.nl/?url=s2.loli.net/2023/08/22/xTOMJPSmbBHfDi7.webp
---
这篇文章用于测试LaTeX支持是否完整。

你问Markdown解析器不都支持LaTeX吗？是的，但这解析器是俺自己写的🤣

行内LaTeX：$ x^2 - x_1 - 6 = -3 $, 不等式： $\sqrt{|xy|}\leq\left|\frac{x+y}{2}\right|,$

泰勒公式：
$$
\begin{equation}
e^x = 1 + x + \frac{x^2}{2} + \frac{x^3}{6} + \cdots = \sum_{n\geq 0} \frac{x^n}{n!}
\end{equation}
$$
集合：
$$
(A\cup B)-(C-A) = A \cup (B-C)
$$






常微分方程：
$$
\left\{ \begin{array}{*{20}{l}}
{\mathop{{y}}\nolimits^{{ \left( {n} \right) }}=f{ \left( {x,y,{y \prime }, \cdots ,\mathop{{y}}\nolimits^{{ \left( {n-1} \right) }}} \right) }}\\
{y{ \left( {\mathop{{x}}\nolimits_{{0}}} \right) }=\mathop{{y}}\nolimits_{{0}}}\\
{y \prime { \left( {\mathop{{x}}\nolimits_{{0}}} \right) }={\mathop{{y}}\nolimits_{{0}} \prime }}\\
{ \cdots }\\
{\mathop{{y}}\nolimits^{{ \left( {n-1} \right) }}{ \left( {\mathop{{x}}\nolimits_{{0}}} \right) }=\mathop{{\mathop{{y}}\nolimits_{{0}}}}\nolimits^{{ \left( {n-1} \right) }}}
\end{array}\right.
$$


二阶常系数非齐次线性微分方程：
$$
\begin{array}{*{20}{l}}
{\text{对}\text{二}\text{阶}\text{方}\text{程}}\\
{y '' +p{y \prime }+qy=f{ \left( {x} \right) }}\\
{\text{先}\text{求}\text{对}\text{应}\text{齐}\text{次}\text{方}\text{程}}\\
{y '' +p{y \prime }+qy=0}\\
{\text{的}\text{通}\text{解}y\text{,}\text{再}\text{根}\text{据}f{ \left( {x} \right) }\text{求}\text{另}\text{一}\text{个}\text{特}\text{解}\mathop{{y}}\nolimits_{{0}}}
\end{array}

$$






LaTeX块：
$$
Are $a, b \in \mathbb{R}, then applies (a+b)^{2} = a^{2} + ab + b^{2} $ \\ 
better \\ 
are $a, b \in \mathbb{R}, \textrm{then apply} \, (a+b)^{2 } = a^{2 } + ab + b^{2}$\\
$$

$$
E=mc^2
$$

竖式：
$$
\frac{
    \begin{array}[b]{r}
      \left( x_1 x_2 \right)\\
      \times \left( x'_1 x'_2 \right)
    \end{array}
  }{
    \left( y_1y_2y_3y_4 \right)
  }

$$




求极限：
$$
\lim\limits_{x \to \infty} \exp(-x) = 0
$$
积分：
$$
\frac{d}{dx}(\sin(x)) = \cos(x)
$$

$$
\frac{d}{dx}(\cos(x)) = -\sin(x)
$$

$$
\frac{d}{dx}(\tan(x)) = \sec^2(x)
$$

不定积分：
$$
\begin{array}{*{20}{l}}
{{}_{ }^{ } \int _{ }^{ }k \text{d} x=kx+C}\\
{{}_{ }^{ } \int _{ }^{ }\mathop{{x}}\nolimits^{{ \mu }} \text{d} x=\frac{{\mathop{{x}}\nolimits^{{ \mu +1}}}}{{ \mu +1}}+C,{ \left( { \mu  \neq -1} \right) }}\\
{{}_{ }^{ } \int _{ }^{ }\frac{{1}}{{x}} \text{d} x= \text{ln} { \left| {x} \right| }+C}\\
{{}_{ }^{ } \int _{ }^{ }\frac{{1}}{{1+\mathop{{x}}\nolimits^{{2}}}} \text{d} x= \text{arctan} x+C}\\
{{}_{ }^{ } \int _{ }^{ }\frac{{1}}{{\sqrt{{1-\mathop{{x}}\nolimits^{{2}}}}}} \text{d} x= \text{arcsin} x+C}
\end{array}

$$


二重积分：
$$
\begin{array}{*{20}{l}}
{\begin{array}{*{20}{l}}
{D}&{\text{有}\text{界}\text{闭}\text{区}\text{域}\text{,}\text{积}\text{分}\text{区}\text{域}}\\
{ \Delta \mathop{{ \sigma }}\nolimits_{{i}}}&{\text{第}i\text{个}\text{小}\text{闭}\text{区}\text{域}}\\
{ \lambda }&{\text{所}\text{有}\text{小}\text{闭}\text{区}\text{域}\text{中}\text{直}\text{径}\text{最}\text{大}\text{的}\text{值}}\\
{f{ \left( {x,y} \right) },g{ \left( {x,y} \right) }}&{\text{定}\text{义}\text{在}D\text{上}\text{的}\text{有}\text{界}\text{函}\text{数}\text{,}\text{被}\text{积}\text{函}\text{数}}\\
{ \sigma }&{D\text{的}\text{面}\text{积}}\\
{ \text{d}  \sigma , \text{d} x \text{d} y}&{\text{直}\text{角}\text{坐}\text{标}\text{系}\text{中}\text{的}\text{微}\text{元}\text{面}\text{积}}\\
{ \alpha , \beta }&{\text{常}\text{数}}\\
{m,M}&{\text{在}D\text{上}f{ \left( {x,y} \right) }\text{的}\text{最}\text{小}\text{值}\text{和}\text{最}\text{大}\text{值}}
\end{array}}\\
{\mathop{ \iint }\nolimits_{{D}}f{ \left( {x,y} \right) } \text{d}  \sigma =\mathop{{ \text{lim} }}\limits_{{ \lambda  \to 0}}\mathop{ \sum }\limits_{{i=1}}^{{n}}f{ \left( {\mathop{{ \xi }}\nolimits_{{i}},\mathop{{ \eta }}\nolimits_{{i}}} \right) } \Delta \mathop{{ \sigma }}\nolimits_{{i}}}\\
{\mathop{ \iint }\nolimits_{{D}}f{ \left( {x,y} \right) } \text{d} x \text{d} y=\mathop{ \int }\nolimits_{{a}}^{{b}}{ \left[ {\mathop{ \int }\nolimits_{{\mathop{{ \varphi }}\nolimits_{{1}}{ \left( {x} \right) }}}^{{\mathop{{ \varphi }}\nolimits_{{2}}{ \left( {x} \right) }}}f{ \left( {x,y} \right) } \text{d} y} \right] } \text{d} x}
\end{array}
$$






连分数：
$$
  x = a_0 + \cfrac{1}{a_1 
          + \cfrac{1}{a_2 
          + \cfrac{1}{a_3 + \cfrac{1}{a_4} } } }
$$
矩阵：
$$
A_{m,n} = 
 \begin{pmatrix}
  a_{1,1} & a_{1,2} & \cdots & a_{1,n} \\
  a_{2,1} & a_{2,2} & \cdots & a_{2,n} \\
  \vdots  & \vdots  & \ddots & \vdots  \\
  a_{m,1} & a_{m,2} & \cdots & a_{m,n} 
 \end{pmatrix}
$$
