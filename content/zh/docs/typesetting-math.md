---
title:  排版数学公式
weight: 6
---
{{< katex />}}

# 使用$\LaTeX$排版数学公式

为较好地支持排版数学公式，需要使用AMS-$\LaTeX$宏集。
AMS-$\LaTeX$宏集是一个包含了若干类和宏包的数学排版拓展，我们主要使用`amsmath`宏包。
以下的命令总是假定已引用该宏包。

# 行内公式

数学公式的排版分为两种：其一是与文字混排，称为**行内公式**；其二是单独成行，称为**行间公式**。

行内公式是由一对`$`包裹($\TeX$语法)或是由`\(`与`\)`包裹($\LaTeX$语法)的环境：

{{<columns>}}

## 源代码

```latex
设直角三角形的两条直角边长度分别为$a$和$b$，
斜边长度为$c$，则$a^2+b^2=c^2$。
```

<--->

## 编译结果

设直角三角形的两条直角边长度分别为$a$和$b$，斜边长度为$c$，则$a^2+b^2=c^2$。

{{</columns>}}

也可以使用`\begin{math}`和`\end{math}`来包裹，甚至可以混用语法：`$a\)`。
但这两种都不推荐。

我们建议全部使用$\TeX$语法(即使用`$`包裹)，这样便于阅读。

# 行间公式

若需要将较长的公式独立于段落展示，需要使用环境`equation`：

{{<columns>}}

## 源代码

```latex
设直角三角形的两条直角边长度分别为$a$和$b$，
斜边长度为$c$，则
\begin{equation}
a^2 + b^2 = c^2
\end{equation}
```

<--->

## 编译结果

设直角三角形的两条直角边长度分别为$a$和$b$，
斜边长度为$c$，则
\begin{equation}
a^2 + b^2 = c^2
\end{equation}

{{</columns>}}

`equation`环境会为公式生成编号，可以使用`\label`, `\ref`进行引用。
`\tag{}`可为公式修改编号。

如果不需要编号，可以使用`\notag`命令。此外也有更直接的方式：

1.	使用`equation*`环境；

1.	使用`displaymath`环境；

1.	使用一对`$$`包裹($\TeX$语法)或者用`\[`与`\]`包裹($\LaTeX$语法)。

**注意事项**：请尽量不要使用`$$`包裹来生成行间公式，更不要混合使用语法。其并不支持如`fleqn`等命令(见[文档导言](../getting-started-with-LaTeX#文档导言))。此外还有其它支持问题，可以参考讨论[Why is `\[ ... \]` preferable to `$$ ... $$`?](https://tex.stackexchange.com/questions/503/why-is-preferable-to)。

{{<columns>}}

## 源代码

```latex
设直角三角形的两条直角边长度分别为$a$和$b$，
斜边长度为$c$，则
\begin{equation*}
a^2 + b^2 = c^2
\end{equation*}
或者更简单一些：
\[ a^2 + b^2 = c^2 \]
```

<--->

## 编译结果

设直角三角形的两条直角边长度分别为$a$和$b$，
斜边长度为$c$，则
\\[
a^2 + b^2 = c^2
\\]
或者更简单一些：
\\[ a^2 + b^2 = c^2 \\]

{{</columns>}}

## 数学模式

被数学环境包裹的片段进入数学模式，其与文本模式有差异，如：

1.	空格将被忽略，由表达式生成间距，也可以使用`\,`, `\quad`等手动调整间距；

1.	不允许有空行；

1.	所有字母被当作变量处理，间距与文本模式不一致，亦不会生成单词间的空格。
	如须嵌入文本模式，可以使用`\text{}`, `\textit{}`等命令。

{{<columns>}}

## 源代码

```latex
$\forall x \in \mathbb R: \qquad x^2 \geq 0$

$x^2 \geq 0 \qquad \text{for all } x \in \mathbb R$
```

<--->

## 编译结果

$\forall x \in \mathbb R: \qquad x^2 \geq 0$

$x^2 \geq 0 \qquad \text{for all } x \in \mathbb R$

{{</columns>}}

**注意事项**：请不要滥用`\text`命令进入文本模式，更不要做无必要的数学环境和文本环境的多层嵌套。

# 常用数学命令表

注：由于表格较宽，建议使用电脑浏览以获取最佳效果。

## 希腊字母

| 命令  |  \alpha  |   \beta    |  \gamma  |  \delta   |  \epsilon  |  \varepsilon  |  \zeta   |    \eta    |  \theta   |  \vartheta  |    \iota    |
| :---: | :------: | :--------: | :------: | :-------: | :--------: | :-----------: | :------: | :--------: | :-------: | :---------: | :---------: |
| 字母  | $\alpha$ |  $\beta$   | $\gamma$ | $\delta$  | $\epsilon$ | $\varepsilon$ | $\zeta$  |   $\eta$   | $\theta$  | $\vartheta$ |   $\iota$   |
| 命令  |  \kappa  |  \lambda   |   \mu    |    \nu    |    \xi     |      \pi      |  \varpi  |    \rho    |  \varrho  |   \sigma    |  \varsigma  |
| 字母  | $\kappa$ | $\lambda$  |  $\mu$   |   $\nu$   |   $\xi$    |     $\pi$     | $\varpi$ |   $\rho$   | $\varrho$ |  $\sigma$   | $\varsigma$ |
| 命令  |   \tau   |  \upsilon  |   \phi   |  \varphi  |    \chi    |     \psi      |  \omega  |            |           |             |             |
| 字母  |  $\tau$  | $\upsilon$ |  $\phi$  | $\varphi$ |   $\chi$   |    $\psi$     | $\omega$ |            |           |             |             |
| 命令  |  \Gamma  |   \Delta   |  \Theta  |  \Lambda  |    \Xi     |      \Pi      |  \Sigma  |  \Upsilon  |   \Phi    |    \Psi     |   \Omega    |
| 字母  | $\Gamma$ |  $\Delta$  | $\Theta$ | $\Lambda$ |   $\Xi$    |     $\Pi$     | $\Sigma$ | $\Upsilon$ |  $\Phi$   |   $\Psi$    |  $\Omega$   |

## 数学字体

|        命令        |      描述       |                       大写字母                       |                       小写字母                       |          数字           |
| :----------------: | :-------------: | :--------------------------------------------------: | :--------------------------------------------------: | :---------------------: |
| \mathnormal (默认) |     default     |            $ABCDEFGHIJKLMN$$OPQRSTUVWXYZ$            |             $abcdefghijklmnopqrstuvwxyz$             |      $0123456789$       |
|      \mathrm       |      Roman      |   $\mathrm{ABCDEFGHIJKLMN}$$\mathrm{OPQRSTUVWXYZ}$   |   $\mathrm{abcdefghijklmn}$$\mathrm{opqrstuvwxyz}$   |  $\mathrm{0123456789}$  |
|      \mathit       |     Italic      |   $\mathit{ABCDEFGHIJKLMN}$$\mathit{OPQRSTUVWXYZ}$   |   $\mathit{abcdefghijklmn}$$\mathit{opqrstuvwxyz}$   |  $\mathit{0123456789}$  |
|      \mathcal      |  Calligraphic   |  $\mathcal{ABCDEFGHIJKLMN}$$\mathcal{OPQRSTUVWXYZ}$  |  $\mathcal{abcdefghijklmn}$$\mathcal{opqrstuvwxyz}$  | $\mathcal{0123456789}$  |
|     \mathfrak      |     Frakutr     | $\mathfrak{ABCDEFGHIJKLMN}$$\mathfrak{OPQRSTUVWXYZ}$ | $\mathfrak{abcdefghijklmn}$$\mathfrak{opqrstuvwxyz}$ | $\mathfrak{0123456789}$ |
|      \mathbb       | Blackboard bold |   $\mathbb{ABCDEFGHIJKLMN}$$\mathbb{OPQRSTUVWXYZ}$   |   $\mathbb{abcdefghijklmn}$$\mathbb{opqrstuvwxyz}$   |  $\mathbb{0123456789}$  |
|      \mathbf       |    Boldface     |   $\mathbf{ABCDEFGHIJKLMN}$$\mathbf{OPQRSTUVWXYZ}$   |   $\mathbf{abcdefghijklmn}$$\mathbf{opqrstuvwxyz}$   |  $\mathbf{0123456789}$  |
|      \mathtt       |   Typewriter    |   $\mathtt{ABCDEFGHIJKLMN}$$\mathtt{OPQRSTUVWXYZ}$   |   $\mathtt{abcdefghijklmn}$$\mathtt{opqrstuvwxyz}$   |  $\mathtt{0123456789}$  |
|      \mathsf       |   Sans Serif    |   $\mathsf{ABCDEFGHIJKLMN}$$\mathsf{OPQRSTUVWXYZ}$   |   $\mathsf{abcdefghijklmn}$$\mathsf{opqrstuvwxyz}$   |  $\mathsf{0123456789}$  |

## 二元关系符

|       <       |       >       |     =     | \leq (or \le) | \geq (or \ge)  |    \equiv     |     \ll     |     \gg     |  \doteq   |    \prec    |    \succ    |  \sim   |
| :-----------: | :-----------: | :-------: | :-----------: | :------------: | :-----------: | :---------: | :---------: | :-------: | :---------: | :---------: | :-----: |
|      $<$      |      $>$      |    $=$    |    $\leq$     |     $\geq$     |   $\equiv$    |    $\ll$    |    $\gg$    | $\doteq$  |   $\prec$   |   $\succ$   | $\sim$  |
|    \preceq    |    \succeq    |  \simeq   |    \subset    |    \supset     |    \approx    |  \subseteq  |  \supseteq  |   \cong   |  \sqsubset  |  \sqsupset  |  \Join  |
|   $\preceq$   |   $\succeq$   | $\simeq$  |   $\subset$   |   $\supset$    |   $\approx$   | $\subseteq$ | $\supseteq$ |  $\cong$  | $\sqsubset$ | $\sqsupset$ | $\Join$ |
|  \sqsubseteq  |  \sqsupseteq  |  \bowtie  |      \in      | \ni (or \owns) |    \propto    |   \vdash    |   \dashv    |  \models  |    \mid     |  \parallel  |  \perp  |
| $\sqsubseteq$ | $\sqsupseteq$ | $\bowtie$ |     $\in$     |     $\ni$      |   $\propto$   |  $\vdash$   |  $\dashv$   | $\models$ |   $\mid$    | $\parallel$ | $\perp$ |
|    \smile     |    \frown     |  \asymp   |       :       |     \notin     | \neq (or \ne) |             |             |           |             |             |         |
|   $\smile$    |   $\frown$    | $\asymp$  |      $:$      |    $\notin$    |    $\neq$     |             |             |           |             |             |         |

## 二元运算符

| +         | -        | \pm        | \mp          | riangleleft     | \triangleright   | \cdot              | \div      | \times   | \setminus   | \star      | \cup     |
| --------- | -------- | ---------- | ------------ | --------------- | ---------------- | ------------------ | --------- | -------- | ----------- | ---------- | -------- |
| $+$       | $-$      | $\pm$      | $\mp$        | $\triangleleft$ | $\triangleright$ | $\cdot$            | $\div$    | $\times$ | $\setminus$ | $\star$    | $\cup$   |
| \cap      | \ast     | \sqcup     | \sqcap       | \circ           | \vee (or \lor)   | \wedge (or \land)  | \bullet   | \oplus   | \ominus     | \diamond   | \odot    |
| $\cap$    | $\ast$   | $\sqcup$   | $\sqcap$     | $\circ$         | $\vee$           | $\wedge$           | $\bullet$ | $\oplus$ | $\ominus$   | $\diamond$ | $\odot$  |
| \oslash   | \uplus   | \otimes    | \bigcirc     | \amalg          | \bigtriangleup   | \bigtriangledown   | \dagger   | \lhd     | \rhd        | \ddagger   | \unlhd   |
| $\oslash$ | $\uplus$ | $\otimes$  | $\bigcirc$   | $\amalg$        | $\bigtriangleup$ | $\bigtriangledown$ | $\dagger$ | $\lhd$   | $\rhd$      | $\ddagger$ | $\unlhd$ |
| \unrhd    | \wr      | \dotplus   | \centerdot   | \ltimes         | \rtimes          |                    |           |          |             |            |          |
| $\unrhd$  | $\wr$    | $\dotplus$ | $\centerdot$ | $\ltimes$       | $\rtimes$        |                    |           |          |             |            |          |

分式使用命令`\frac{分子}{分母}`书写，在行间公式中正常显示，而在行内公式中被压缩以适应行高。
可以使用`\tfrac`与`\dfrac`来获得行内和行间的分式风格。
此外我们也常使用`1/2`来表示分式，这在部分情况下会较为美观。  

{{<columns>}}

## 源代码

```latex
$1/2 \qquad \frac{1}{2} \qquad \dfrac{1}{2}$
\begin{equation*}
3/8 \qquad \frac{3}{8} \qquad \tfrac{3}{8}
\end{equation*}
```

<--->

## 编译结果

$1/2 \qquad \frac{1}{2} \qquad \dfrac{1}{2}$
\\[3/8 \qquad \frac{3}{8} \qquad \tfrac{3}{8}\\]

{{</columns>}}

对于模函数`mod`，使用`\bmod`来表示`mod`运算，而`\pmod`表示同余式等，如

{{<columns>}}

## 源代码

```latex
$a \bmod b$, $x \equiv a \pmod b$
```

<--->

## 编译结果

$a \bmod b$, $x \equiv a \pmod b$

{{</columns>}}

## 箭头

| \leftarrow (or \gets) | \longleftarrow      | \rightarrow (or \to) | \longrightarrow   | \leftrightarrow   | \longleftrightarrow   |
| --------------------- | ------------------- | -------------------- | ----------------- | ----------------- | --------------------- |
| $\leftarrow$          | $\longleftarrow$    | $\rightarrow$        | $\longrightarrow$ | $\leftrightarrow$ | $\longleftrightarrow$ |
| \Leftarrow            | \Longleftarrow      | \Rightarrow          | \Longrightarrow   | \Leftrightarrow   | \Longleftrightarrow   |
| $\Leftarrow$          | $\Longleftarrow$    | $\Rightarrow$        | $\Longrightarrow$ | $\Leftrightarrow$ | $\Longleftrightarrow$ |
| \mapsto               | \longmapsto         | \hookleftarrow       | \hookrightarrow   | \leftharpoonup    | \rightharpoonup       |
| $\mapsto$             | $\longmapsto$       | $\hookleftarrow$     | $\hookrightarrow$ | $\leftharpoonup$  | $\rightharpoonup$     |
| \leftharpoondown      | \rightharpoondown   | \rightleftharpoons   | \iff              | \uparrow          | \downarrow            |
| $\leftharpoondown$    | $\rightharpoondown$ | $\rightleftharpoons$ | $\iff$            | $\uparrow$        | $\downarrow$          |
| \updownarrow          | \Uparrow            | \Downarrow           | \Updownarrow      | \nearrow          | \searrow              |
| $\updownarrow$        | $\Uparrow$          | $\Downarrow$         | $\Updownarrow$    | $\nearrow$        | $\searrow$            |
| \swarrow              | \nwarrow            | \leadsto             |                   |                   |                       |
| $\swarrow$            | $\nwarrow$          | $\leadsto$           |                   |                   |                       |

## 分隔符

| (             | )               | [ (or \lbrack) | ] (or \rbrack) | \\{ (or \lbrace) | \\} (or \rbrace) | \langle   | \rangle   |
| ------------- | --------------- | -------------- | -------------- | ---------------- | ---------------- | --------- | --------- |
| $($           | $)$             | $[$            | $]$            | $\\{$            | $\\}$            | $\langle$ | $\rangle$ |
| \| (or \vert) | \\\| (or \Vert) | /              | \backslash     | \lfloor          | \rfloor          | \lceil    | \rceil    |
| $\|$          | $\\\|$          | $/$            | $\backslash$   | $\lfloor$        | $\rfloor$        | $\lceil$  | $\rceil$  |

可以在两个分隔符前分别用`\left`与`\right`命令来根据其间包裹内容大小自动调整分隔符大小。
对于单边的分隔符，可以使用`\left.`或`\right.`来使另一边不可见：

{{<columns>}}

## 源代码

```latex
\begin{equation*}
\left. \left(\alpha + \frac{1}{\beta}\right)^3 \right|_{\alpha = 1, \beta = -1} = 0
\end{equation*}
```

<--->

## 编译结果

\\[\left. \left(\alpha + \frac{1}{\beta}\right)^3 \right|_{\alpha = 1, \beta = -1} = 0\\]

{{</columns>}}

## 杂项

| \dots       | \cdots         | \vdots       | \ddots      | \hbar        | \imath          | \jmath     | \ell       | \Re           |
| ----------- | -------------- | ------------ | ----------- | ------------ | --------------- | ---------- | ---------- | ------------- |
| $\dots$     | $\cdots$       | $\vdots$     | $\ddots$    | $\hbar$      | $\imath$        | $\jmath$   | $\ell$     | $\Re$         |
| \Im         | \aleph         | \wp          | \forall     | \exists      | \mho            | \partial   | \prime     | \varnothing   |
| $\Im$       | $\aleph$       | $\wp$        | $\forall$   | $\exists$    | $\mho$          | $\partial$ | $\prime$   | $\varnothing$ |
| \emptyset   | \infty         | \nabla       | \triangle   | \Box         | \Diamond        | \bot       | \top       | \angle        |
| $\emptyset$ | $\infty$       | $\nabla$     | $\triangle$ | $\Box$       | $\Diamond$      | $\bot$     | $\top$     | $\angle$      |
| \surd       | \diamondsuit   | \heartsuit   | \clubsuit   | \spadesuit   | \neg (or \lnot) | \flat      | \natural   | \sharp        |
| $\surd$     | $\diamondsuit$ | $\heartsuit$ | $\clubsuit$ | $\spadesuit$ | $\neg$          | $\flat$    | $\natural$ | $\sharp$      |

## 算符

| \sin  | \cos  | \tan  | \cot  |  \sec   | \arcsin | \arccos  | \arctan |
| :---: | :---: | :---: | :---: | :-----: | :-----: | :------: | :-----: |
| \arg  | \csc  | \sinh | \cosh |  \tanh  |  \coth  |   \exp   |  \log   |
|  \lg  |  \ln  | \dim  | \ker  |  \hom   |  \deg   | \max[^1] |  \min   |
| \det  |  \Pr  | \gcd  | \inf  | \liminf |  \sup   | \limsup  |  \lim   |

[^1]: `\max`及其后的算符使用上下限。

对于未定义的算符，可以用`\DeclareMathOperator{}{}`命令定义，也可以用带星号的版本以支持上下限。

{{<columns>}}

## 源代码

```latex
\DeclareMathOperator{\argh}{argh}
\DeclareMathOperator*{\nut}{Nut}
\begin{equation*}
3 \argh = 2 \nut_{x = 1}
\end{equation*}
```

<--->

## 编译结果

\\[ 3 \operatorname{argh} = 2 \operatorname*{Nut} \limits_{x = 1} \\]

{{</columns>}}

## 巨算符

|   \sum    |    \prod    |   \coprod   |    \int    |    \oint    |   \bigcup    |  \bigcap  |  \bigsqcup  |
| :-------: | :---------: | :---------: | :--------: | :---------: | :----------: | :-------: | :---------: |
|  $\sum$   |   $\prod$   |  $\coprod$  |   $\int$   |   $\oint$   |  $\bigcup$   | $\bigcap$ | $\bigsqcup$ |
|  \bigvee  |  \bigwedge  |  \biguplus  |  \bigodot  |  \bigoplus  |  \bigotimes  |           |             |
| $\bigvee$ | $\bigwedge$ | $\biguplus$ | $\bigodot$ | $\bigoplus$ | $\bigotimes$ |           |             |

巨算符在行内与行间的大小和形状有一定差异，在行内上下标位于右方，在行间上下标位于上下方。
可以使用`\limits`和`\nolimits`调整。

在连用多个积分号时可能间隔较大，可以用`\!`调整，或者使用由`amsmath`提供的命令，如
`\iint`, `\iiint`, `\iiiint`和`\idotsint`等。

## 重音

| \hat{a}               | \grave{a}              | \bar{a}                    | \acute{a}                   | \mathring{a}           | \check{a}               |
| --------------------- | ---------------------- | -------------------------- | --------------------------- | ---------------------- | ----------------------- |
| $\hat{a}$             | $\grave{a}$            | $\bar{a}$                  | $\acute{a}$                 | $\mathring{a}$         | $\check{a}$             |
| \dot{a}               | \vec{a}                | \breve{a}                  | \tilde{a}                   | \ddot{a}               | a' (= a^{\prime})       |
| $\dot{a}$             | $\vec{a}$              | $\breve{a}$                | $\tilde{a}$                 | $\ddot{a}$             | $a^{\prime}$            |
| \widehat{AAA}         | \widetilde{AAA}        | \overline{AAA}             | \underline{AAA}             | \overrightarrow{AAA}   | \underrightarrow{AAA}   |
| $\widehat{AAA}$       | $\widetilde{AAA}$      | $\overline{AAA}$           | $\underline{AAA}$           | $\overrightarrow{AAA}$ | $\underrightarrow{AAA}$ |
| \overleftarrow{AAA}   | \underleftarrow{AAA}   | \overleftrightarrow{AAA}   | \underleftrightarrow{AAA}   | \underbrace{AAA}_{A}   | \overbrace{AAA}^A       |
| $\overleftarrow{AAA}$ | $\underleftarrow{AAA}$ | $\overleftrightarrow{AAA}$ | $\underleftrightarrow{AAA}$ | $\underbrace{AAA}_{A}$ | $\overbrace{AAA}^A$     |