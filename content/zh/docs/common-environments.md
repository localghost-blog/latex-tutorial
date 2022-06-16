---
title: 常见环境
weight: 4
---
{{< katex />}}

# 列表环境

列表环境有三种，分别是：
1.	`itemize`：无序列表；
1.	`enumerate`：有序列表；
1.	`description`：描述列表。


列表的项以`\item`开头，后面可以跟着一个描述，描述的内容会被放在列表项的右边。
`\item`有可选参数`[name]`，用于指定列表项的名称，对于`desription`为必须项。例子见下：

{{<columns>}}

## 源代码

```latex
\begin{enumerate}
	\item You can nest the list environments to your taste:
		\begin{itemize}
			\item But it might start to look silly.
			\item[-] With a dash.
		\end{itemize}
	\item Therefore remember:
		\begin{description}
			\item[Stupid] things will not become smart because they are in a list.
			\item[Smart] things, though, can be presented beautifully in a list.
		\end{description}
\end{enumerate}
```

<--->

## 编译结果

1.	You can nest the list environments to your taste:
	
	•	But it might start to look silly.

	\-	With a dash.
1.	Therefore remember:

	**Stupid** things will not become smart because they are in a list.

	**Smart** things, though, can be presented beautifully in a list.

{{</columns>}}

**注意事项**：列表环境可以如上例一样嵌套，但环境`itemize`及`enumerate`的嵌套层数至多为4层，其中`itemize`中的`\item`对应的命令为`\labelitemi` 至 `\labelitemiv`，而`enumerate`中的`\item`对应的命令为`\labelenumi` 至 `\labelenumiv`。
其代表的符号可以使用`texdef`查找：

```console
$ texdef -t latex -f \labelitemi \labelitemii \labelitemiii \labelitemiv
```

我们可以更改默认的列表样式。
在纯净$\LaTeX$环境中，可以使用`\renewcommand{command}{symbol}`命令，例如`\rewnewcommand{\labelitemi}{\dag}`将第1层`itemize`的`\item`显示为`\dag`($\dag$)。

宏包`enumitem`给出了方便地更改默认列表样式的方法，或仅修改当前的列表环境，也可以设置其它参数，见其[文档](https://mirrors.ircam.fr/pub/CTAN/macros/latex/contrib/enumitem/enumitem.pdf)。

# 对齐环境

环境`center`, `flushleft`, `flushright`可以用于对齐文本，例如：

{{<columns>}}

## 源代码

```latex
\begin{flushleft}
This text is\\ left-aligned.
\LaTeX{} is not trying to make
each line the same length.
\end{flushleft}

\begin{flushright}
This text is right-\\aligned.
\LaTeX{} is not trying to make
each line the same length.
\end{flushright}

\begin{center}
At the centre\\of the earth
\end{center}
```

<--->

## 编译结果


<div style="text-align: left;">
This text is <br>
left-aligned. $\LaTeX$ is not trying to make <br>
each line the same length.
</div>


<div style="text-align: right;">
This text is right- <br>
aligned. $\LaTeX$ is not trying to make each <br>
line the same length.
</div>

<div style="text-align: center;">
At the centre <br>
of the earth
</div>
{{</columns>}}

此外，可用`\centering`, `\raggedright`, `\raggedleft`等命令来设置文本的对齐方式。
区别在于环境会在上下文产生额外间距，而命令仅改变对齐方式。

# 引文环境

$\LaTeX$提供了`quote`和`quotation`两种引文环境，其中`quote`适于引用短文字，首行不缩进；`quotation`适用于引用若干段文字，首行缩进。
此外，引文环境相比一般文字有额外的左右缩进。

{{<columns>}}

## 源代码

```latex
France is Bacon:
\begin{quote}
	Knowledge is power.
\end{quote}
```

<--->

## 编译结果

France is Bacon:

&emsp;Knowledge is power.

{{</columns>}}

{{<columns>}}

## 源代码

```latex
《孔雀东南飞》：
\begin{quotation}
孔雀东南飞，五里一徘徊。

十三能织素，十四学裁衣，
十五弹箜篌，十六诵诗书。
十七为君妇，心中常苦悲。
\end{quotation}
```

<--->

## 编译结果

《孔雀东南飞》：

&emsp;&emsp;&emsp;孔雀东南飞，五里一徘徊。

&emsp;&emsp;&emsp;十三能织素，十四学裁衣，
十五弹箜篌，十六诵诗书。
十七为君妇，心中常苦悲。

{{</columns>}}

## 摘要环境

摘要环境`abstract`默认仅在文档类`article`, `report`中可用，一般紧跟`\maketitle`命令。
若指定`titlepage`选项，则单独成页；若否，单栏排版时相当于居中标题与`quotation`环境，双栏排版时相当于`\section*`中的一节。

# 定理环境

在使用$\LaTeX$排版数学或其它科技文档时，
会大量使用定理、证明等内容，但定理环境不仅限于此。
在写其它文档时，如剧本等，我们也可以灵活使用定理环境。
$\LaTeX$提供命令`\newtheorem`来定义定理环境：

```latex
\newtheorem{envname}{title}[section-level]
% or
\newtheorem{envname}[counter]{title}
```

其中`envname`为定理环境名称，`title`为定理标题，`section-level`为章节层级，见[章节层级](../how-to-write-a-well-structured-latex-file/#章节层级)，`counter`为定理计数器名称。

**注意事项**：`\newtheorem`的出现位置应早于其定义环境的实例，可以出现在正文区，但一般会放在导言区。

若选用第一种定义，定理的序号(计数器)为章节名的下一级序号(计数器)。

在定义好定理环境后，就可以使用环境了。定理环境提供可选参数`options`

```latex
\begin{envname}[options]
...
\end{envname}
```

效果见下

{{<columns>}}

## 源代码

```latex
\newtheorem{theorem}{Theorem}[section]
\section{section name}
\begin{theorem}
	All triangles are isosceles.
\end{theorem}
\begin{theorem}[This is TRUE!]
	All isosceles are triangles.
\end{theorem}
```

<--->

## 编译结果

### **1 section name**

**Theorem 1.1** *All triangles are isosceles.*

**Theorem 1.2** **(This is TRUE!)** *All isosceles are triangles.*

{{</columns>}}

例中命令新建了一个名为`theorem`的计数器。
此时如果需要新建一个和`theorem`共享编号的定理环境，可以使用
```latex
\newtheorem{proposition}[theorem]{Proposition}
```

**注意事项**：一般来说我们会使用其它新建的定理名作为`counter`的参数。请尽量不要使用章节层级名等作为`counter`参数。

## 使用`amsthm`宏包定制定理环境

宏包`amsthm`提供了`\theoremstyle`来支持定理格式的切换，在`\newtheorem`前使用。

`amsthm`预定义了三种格式用于`\theoremstyle`：

1.	`plain`：与$\LaTeX$原始格式相同，即**粗体标签**，*斜体内容*

1.	`definition`：使用**粗体标签**、正体内容

1.	`remark`：使用*斜体标签*、正体内容

此外`amsthm`支持带星号的`\newtheorem*{envname}{title}`定义不带序号的定理环境。

**注意事项**：`amsthm`会将定理环境的可选参数内容以正体(而非粗体)显示，此外，会在标签后加上一个句号。

{{<columns>}}

## 源代码

```latex
\newtheorem*{Nick}{Nick}
\newtheorem*{Doctor}{Doctor}
\begin{Nick}
When I came back from New York I was disgusted.
\end{Nick}
\begin{Nick}[CONT'D]
Disgusted... with everyone, and everything... Only one man was exempt from my disgust.
\end{Nick}
\begin{Doctor}
One man...? Mr. Carraway?
\end{Doctor}
\begin{Nick}[whispers]
Gatsby...
\end{Nick}
```

<--->

## 编译结果

**Nick.** *When I came back from New York I was disgusted.*

**Nick** (CONT'D)**.** *Disgusted... with everyone, and everything... Only one man was exempt from my disgust.*

**Doctor.** *One man...? Mr. Carraway?*

**Nick** (whispers)**.** *Gatsby...*

{{</columns>}}

此外，`amsthm`也可以使用`\newtheoremstyle`来自定义定理格式，参见其[文档](https://mirrors.hit.edu.cn/CTAN/macros/latex/required/amscls/doc/amsthdoc.pdf)。

## `amsthm`的证明环境

`amsthm`还提供了一个`proof`环境用于排版定理的证明过程。`proof`环境基于`remark`定理风格，在末尾自动加上一个$\square$证毕符号。

**注意事项**：若定理环境末尾为环境，证毕符号可能出现在独立一行，此时可用命令`\qedhere`指定证毕符号的位置。

# 表格环境

排班表格的基本环境为`tabular`，使用方法如下：

```latex
\begin{tabular}[align]{column_spec}
⟨item1⟩ & ⟨item2⟩ & … \\
\hline
⟨item1⟩ & ⟨item2⟩ & … \\
\end{tabular}
```

每行的单元格以`&`分隔，`\\`(或`\cr`)切换新行。

**注意事项**：直接`tabular`环境时会和**文字混排**。此时`align`控制表格的垂直对齐方式：`t`, `b`对应按顶部、底部对齐，其余情况为居中对齐。
通常表格很少与文字混排，而是放在`table`浮动体环境中，并使用`\caption`命令加标题，此时`align`参数非必要。

而`column_spec`指定列数及每列格式。常见的列格式如下：

| 格式     | 描述                                   |
| -------- | -------------------------------------- |
| l/c/r    | 单元格左对齐/居中/右对齐               |
| p{width} | 单元格宽度固定为width(如6em)，自动换行 |
| \|       | 绘制竖线                               |
| @{str}   | 自定义内容                             |

其中l/c/r/p个数之和为列数。

单元格前后会额外添加间距，而@格式会取消间距。

此外，$\LaTeX$提供将参数重复的写法`*{n}{arg}`，如以下的写法等效：

```latex
\begin{tabular}{|c|c|c|c|c|p{4em}|p{4em}|}
% 及
\begin{tabular}{|*{5}{c|}*{2}{p{4em}|}}
```

## 分割线绘制

在表格每行的开头使用命令`\hline`可以绘制分割线。此外`\cline{i-j}`可以绘制第i列至第j列的横线。

此外，宏包`booktabs`提供了科技论文中常用的三线表，提供`\toprule`、`\midrule`、`\bottomrule`以绘制三条线，以及和`\cline`对应的`\cmidrule`命令。请尽量不要用其它横线和竖线。

## 合并单元格

$\LaTeX$按行排版表格，因此横向合并单元格较容易，命令为

```latex
\multicolumn{n}{column_spec}{text}
```

其中`n`为行数，`column_spec`为列格式，`text`为合并单元格的内容。其中`column_spec`仅允许出现一列。该命令也可用于修改某一个单元格的列样式。

纵向合并需要用宏包`multirow`提供的命令`\multirow`，其参数为`n`、`width`、`text`，其中`width`参数指定宽度，可以填`*`以使用自然宽度，其余参数与`\multicolumn`相同。

# 图片环境

该环境需要`graphicx`宏包支持。

插入图片的命令如下：

```latex
\includegraphics[options]{filename}
```

其中`options`中的参数指定为`key = value`的形式，常用参数如下：

| 参数              | 描述                    |
| ----------------- | ----------------------- |
| width = (width)   | 缩放至宽度为(width)     |
| height = (height) | 缩放至高度为(height)    |
| scale = (scale)   | 相对原尺寸缩放(scale)倍 |
| angle = (angle)   | 逆时针旋转(angle)度     |

`filename`用相对路径或绝对路径表示，见[使用本地字体](../international-language-support/#使用本地字体)一节。

XeLaTeX原生支持.pdf, .eps矢量图，以及.jpg, .png, .bmp位图。

## svg格式图片支持

由于LaTeX并不支持.svg格式文件的导入，因此需要将其转换为其它格式。

此处推荐使用软件[inkscape](https://inkscape.org/)，安装后可以在命令行使用：

```console
$ inkscape sample.svg --export-eps=sample.eps
# or
$ inkscape sample.svg --export-pdf=sample.pdf
```

# 迷你页环境

$\LaTeX$提供了生成独立页的环境`minipage`。命令如下：

```latex
\begin{minipage}[align][height][inner-align]{width}
```

其中`align`为迷你页与文字的混排格式(见[表格环境](#表格环境))，`height`为高度，`inner-align`为内部的对齐方式，分为顶部`t`, 底部`b`, 居中`c`, 分散`s`, `width`为宽度。

迷你页常在并排显示图片的时候使用，如并排显示两个图片，通常为以下格式(见[并排浮动体与子浮动体](#并排浮动体与子浮动体))。

```latex
\begin{figure}
	\centering
	\begin{minipage}{.5\textwidth}
		\centering
		\includegraphics[...]{figure1}
		\caption{...}
	\end{minipage}
	\begin{minipage}{.5\textwidth}
		\centering
		\includegraphics[...]{figure2}
		\caption{...}
	\end{minipage}
\end{figure}
```

# 浮动体环境

表格、图片等内容尺寸较大，会导致分页困难。
$\LaTeX$为此引入的浮动体的机制，使得大块内容可以脱离原文，自动放置在合适位置。

$\LaTeX$预定义了两类浮动体环境`table`和`figure`，一般来说`table`放表格，`figure`放图片，但也可以放置任意内容。

以`table`浮动体为例：

```latex
\begin{table}[placement]
	\centering
	\begin{tabular}{...}
	...
	\end{tabular}
\end{table}
```

参数`placement`提供浮动体允许排版的位置，见下表：

| 参数 | 描述                     |
| ---- | ------------------------ |
| h    | 此处                     |
| t    | 顶部                     |
| b    | 底部                     |
| p    | 单独成页                 |
| !    | 改变部分参数，提高强制性 |
| H    | 强制插入此处             |

其中`H`仅能单独使用，其余参数可以组合，如`[ht!p]`。

**注意事项**：排版位置的选取与参数内符号**顺序无关**，总是以h-t-b-p的优先级决定位置。

在双栏排版的环境下，$\LaTeX$提供了`table*`和`figure*`环境，用于处理跨栏浮动体，用法与`table`和`figure`相同，但参数`placement`仅允许`t`和`p`。

使用命令`\listoftables`和`\listoffigures`可以生成当前文件中的浮动体目录。

浮动体可以用`\caption[]{}`指定标题，其中长标题必须指定，短标题可选，会出现在目录中。

## 并排浮动体与子浮动体

我们经常需要在浮动体中放置多个表格或图片，最简单的是并排放置，如

```latex
\begin{figure}{...}
	\centering
	\includegraphics[...]{figure1}
	\qquad
	\includegraphics[...]{figure2}
	\\
	\includegraphics[...]{figure3}
	\caption{...}
\end{figure}
```

如需给并排图片添加标题，则需要借助`minipage`环境，见[迷你页环境](#迷你页环境)。

如果需要给一个`figure`浮动体中的两个子图添加标题，则需要引入`subcaption`宏包(依赖于`caption`宏包)，具体请参考其[文档](https://mirrors.ircam.fr/pub/CTAN/macros/latex/contrib/caption/subcaption.pdf)。

```latex
\begin{figure}
	\centering
	\begin{subfigure}{...}
		\centering
		\includegraphics[...]{figure1.a}
		\caption{...}
	\end{subfigure}
	\qquad
	\begin{subfigure}{...}
		\centering
		\includegraphics[...]{figure1.b}
		\caption{...}
	\end{subfigure}
\end{figure}
```

并排图片和子图片的区别在于，并排图片为多个图片，而包含子图片的图片为单个图片。