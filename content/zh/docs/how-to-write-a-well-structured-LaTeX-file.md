---
title:  如何写出一个结构化的LaTeX文档
weight: 5
---
{{< katex />}}

# 文章结构

了解了如何输入文字内容后，我们可以尝试写出一个结构化的$\LaTeX$文档。

{{<mermaid class="text-center">}}
flowchart LR
A(内容) --> B(开端)
A --> C(正文)
A --> D(结尾)
B --> E(标题)
B --> F(前言)
B --> G(目录)
C --> H(章, 节, 小节)
H --> I(章节内容)
D --> J(附录)
D --> L(参考文献)
D --> M(索引)
{{</mermaid>}}

以上仅为示意图，可根据实际需要增加或删减部分。

# 标题

$\LaTeX$支持生成简单的标题页。

需要在导言区提供标题、作者和日期信息：

```latex
\documentclass{article}
...
\title{标题\thanks{致谢}}
\author{
	作者A\thanks{its@pku.edu.cn} 
	\and 
	作者B\thanks{通讯作者}
}
\date{日期}
\begin{document}
	\maketitle
	...
\end{document}
```

其中前两个命令是必须的(不用`\title`会报错；不用`\author`会警告)，而`\date`可选，不使用时默认为`\today`(生成当前日期)。

`\title`和`\author`可以使用`\thanks`命令来添加致谢信息，会像脚注一样出现在页面下方。
此外`\author`的参数可以使用`\and`来并列多个作者。

在信息给定后，就可以在正文区插入标题页：`\maketitle`。

# 目录与章节

一篇结构化、条理清晰的文档一定是层次分明的，可以通过命令分割为章、节、小节等：
```latex
\begin{document}
\chapter{chapter 1}
	\section{section 1.1}
		\subsection{subsection 1.1.1}
			\subsubsection{subsubsection 1.1.1.1}
				\paragraph{title}
				内容
					\subparagraph{subtitle}
					内容
				...
	\section{section 1.2}
	...
\chapter*{chapter 2}
...
\end{document}
```

其中`\chapter`仅在`report`和`book`文档类有定义。这些命令会生成标题并自动编号。
此外$\LaTeX$还提供了`\part`指令，用来将文档分割为大块，但不影响章节的编号。

章节命令还会在目录中添加条目。每个章节命令有两个变体：

```latex
\section[short]{title}
% 以及
\section*{title}
```

前者会在目录添加短标题，后者标题无编号，也不生成目录项。

在正文部分使用命令`\tableofcontents`会生成目录页。

**注意事项**：可能需要多次编译以使目录正常显示。

## 章节层级

$\LaTeX$标准文档类对章节划分了层级：

*	在`article`中`part`为0，`section`为1，依此类推；

*	在`report`/`book`中`part`为-1，`chapter`为0，`section`为1，依此类推

`secnumdepth`计数器控制编号深度，在`article`中默认值为3，在`report`/`book`中默认值为2。$\LaTeX$会将深度不大于`secnumdepth`的章节进行标号。

`tocdepth`计数器控制目录深度，与`secnumdepth`默认值相同。

我们可以通过命令`\setcounter{secnumdepth}{n}`来将`secnumdepth`计数器的值设置为`n`，
如`\setcounter{secnumdepth}{5}`会给全体章节标号，
而`\setcounter{tocdepth}{-1}`在`article`中会不显示章节目录，在`report`/`book`中会仅显示`part`部分。

## 章节计数器

如果我们需要修改章节的计数，以`section`为例，
可以使用命令`\setcounter{section}{n}`，如

```latex
\begin{document}
\setcounter{section}{-2}
\section{section} % -1
\section*{section} % null
\setcounter{section}{10}
\section*{section} % null
\section{section} % 11
\section{section} % 12
\end{document}
```

# 文档结构的划分

所有标准文档类都提供了`\appendix`命令将正文和附录分开[^appendix]。
在`\appendix`以后最高一级章节使用拉丁字母编号，从A开始。

此外，`book`文档类还提供了前言、正文、后记结构的划分命令：

*	`frontmatter`：前言部分，页码使用小写罗马数字；`\chapter`不编号
*	`mainmatter`：正文部分，页码使用阿拉伯数字；`\chapter`正常编号
*	`backmatter`：后记部分，页码使用阿拉伯数字；`\chapter`不编号

以上命令可以与`\appendix`共同使用，生成有前言、正文、附录、后记的文档。

[^appendix]: 部分文档可能采用`\begin{appendix}...\end{appendix}`的写法，效果相同，但并不规范。

# 脚注与边注

使用`\footnote`命令可在页面底部生成一个脚注，如：

 {{<columns>}}

## 源代码

```latex
j'en ai découvert une démonstration véritablement merveilleuse. 
\footnote{cette marge est trop étroite pour contenir.}
```

<--->

## 编译结果

j'en ai découvert une démonstration véritablement merveilleuse. [^1]

[^1]: cette marge est trop étroite pour contenir.

 {{</columns>}}

在一些环境内(如表格环境)使用`\footnote`无法正确生成脚注，我们可以分两步进行：

1.	在原地使用`\footnotemark`计数

1.	在合适的位置用`\footnotetext`生成脚注

使用`\marginpar[left-margin]{right-margin}`可以生成边注。
如果仅给定`{right-margin}`，则边注在奇偶页相同；
否则奇数页使用`right-margin`，偶数页使用`left-margin`。

**注意事项**：边注较窄，建议不要写过多文字。可以使用`\footnotesize`等命令设置较小的字号。

# 引用与链接

引用是$\LaTeX$强大排版功能的体现之一。

在章节、公式、图表、定理等位置都支持引用。
使用`\label{label-name}`命令后，
在别处可以使用`\ref{lable-name}`生成引用的编号，或是`\pageref{label-name}`生成页码。

以下是一个例子：
{{<columns>}}

## 源代码

```latex
A reference to this subsection
\label{sec:this} looks like:
``see section~\ref{sec:this} on
page~\pageref{sec:this}.''
```

<--->

## 编译结果

A reference to this subsection looks like:
"see section 3.3 on page 22."

(数字为样例)

{{</columns>}}

**注意事项**：可能需要多次编译以生成正确交叉引用。

`\label`命令的使用位置为：

*	**章节标题**：在下一个章节标题前的任意位置
*	**行间公式**：在每一行公式的任意位置
*	**有序列表**：在的任意位置
*	**图表标题**：紧接图表标题
*	**定理环境**：在环境内任意位置

**注意事项**：`label`仅对记编号的命令形式生效。

## 使用超链接

电子文档最实用的需求之一就是超链接功能。$\LaTeX$中实现这一功能的是`hyperref`宏包。

`hyperref`宏包会将目录、引用、脚注、索引、参考文献等封装为超链接，
这也使其与其它宏包发生冲突的可能性增加。
为减少可能的冲突，习惯上将`hyperref`宏包**放在其它宏包之后**调用。

`hyperref`宏包使用`\hypersetup`配置参数。参数也可以作为选项在调用时指定：

```latex
\hypersetup{key1 = value1, ...}
% or
\usepackage[key1 = value1, ...]{hyperref}
```

以下是常用的参数设置：

| 参数       | 默认值  | 描述                                          |
| ---------- | ------- | --------------------------------------------- |
| colorlinks | false   | true：链接文字带颜色；false：加上带颜色的边框 |
| linkcolor  | red     | 一般内部链接颜色                              |
| citecolor  | green   | 文献引用颜色                                  |
| urlcolor   | magenta | 网页地址颜色                                  |

更多参数见其[文档](https://mirror.bjtu.edu.cn/CTAN/macros/latex/contrib/hyperref/doc/hyperref-doc.pdf)。此外也可以访问网页版的[文档](https://mirrors.cloud.tencent.com/CTAN/macros/latex/contrib/hyperref/doc/hyperref-doc.html)。

使用`hyperref`宏包后，所有引用、参考文献、索引等都转化为超链接，也可以使用命令

```latex
\hyperref[label]{text}
```

来指定链接文字的样式，这里`[]`为**必填项**。

宏包提供了直接书写超链接的指令，如：

{{<columns>}}

## 源代码

```latex
\url{https://www.wikipedia.org}
% or
\nolinkurl{https://www.wikepedia.org}
% or
\href{https://www.wikipedia.org}{Wikipedia}
```

<--->

## 编译结果

<https://www.wikipedia.org>

https://www.wikipedia.org(无跳转)

[Wikipedia](https://www.wikipedia.org)

{{</columns>}}

# 参考文献

$\LaTeX$提供的参考文献和引用方式比较原始，需要用户自行书写参考文献列表，此处不介绍。
我们介绍两种方式。
`bibtex`数据库和`biblatex`宏包

## BIB$\TeX$数据库

BIB$\TeX$是目前最流行的参考文献数据组织格式之一。它的出现使我们摆脱手写参考文献条目的麻烦。我们还可以通过参考文献样式的支持，使同一份数据库生成不同样式的文献列表。

BIB$\TeX$以.bib为扩展名，内容使若干条文献条目，每个条目的格式为：

```bibtex
@type{citation,
	key1 = {value1},
	key2 = {value2},
	keyn = {valuen}
}
```

例如

```bibtex
@book{knuth1984texbook,
  title={The texbook},
  author={Knuth, Donald Ervin and Bibby, Duane},
  volume={15},
  year={1984},
  publisher={Addison-Wesley Reading}
}
```

BIB$\TeX$提供了几个预定义的样式，如`plain`, `unsrt`, `alpha`等，如果需要使用期刊模板的话，可能会提供自用样式。样式文件以.bst为扩展名。

使用样式文件的方法为`\bibliographystyle{name}`，其中`name`为样式文件的名称，**不要带扩展名**。

## 如何获取文献数据

多数时候我们不必手写BIB$\TeX$文献条目，
这是因为主流的文献数据库大都有简单的获取BIB$\TeX$文献条目的方式。

如[Google Scholar](https://scholar.google.com/)在每篇文献底下的`引用->BibTeX`存有文献条目。

[北京大学图书馆](https://www.lib.pku.edu.cn/)每篇文献右边的`引用->导出为BibTeX`可以下载bib格式的数据库。

## 完整的文献引用样例

```latex
% main.tex
\documentclass{article}
\bibliographystyle{plain}
\begin{document}
\section{section 1}
Some excellent books, for example, \cite{knuth1984texbook}.

\bibliography{books} % books.bib
\end{document}
```

在文件写好后，我们可以开始编译，命令如下：

```console
$ xelatex main
$ bibtex main
$ xelatex main
$ xelatex main
```

## `biblatex`宏包

`biblatex`宏包是基于$\LaTeX$宏命令的参考文献解决方案，
提供便捷的格式控制和强大的排序、分类、筛选、多文献表等功能。

因其对UTF-8和中文参考文献的良好支持，被国内较多$\LaTeX$模板采用。

使用方式如下：

1.	在导言区调用`biblatex`宏包。宏包支持以`key = value`形式指定参数，包括文献样式、排序规则等。

1.	在其后导言区使用`\addbibresource`命令引入参考文献数据库，与BIB$\TeX$传统方式不同的是，需要写**完整的文件名**。

1.	在正文使用`\cite`命令引用参考文献。此外可用`\citeauthor`, `\citeyear`等单独引用作者与年份，也可用`\footcite`以脚注式引用。

1.	在需要排版参考文献的位置使用`\printbibliography`

`biblatex`自带的常用样式有`authoryear`, `authortitle`, `verbose`, `gb7714-2015`, `ieee`等。

以下是一个样例

```latex
% main.tex
\documentclass{article}
\usepackage[style=gb7714-2015]{biblatex}
\addbibresource{books.bib}
\begin{document}
\section{section 1}
Some excellent books, for example, \cite{knuth1984texbook}.

\printbibliography
\end{document}
```

与BIB$\TeX$传统方式不同的是，`biblatex`使用`biber`程序处理参考文献，命令如下：

```console
$ xelatex main
$ biber main
$ xelatex main
$ xelatex main
```

# 索引

书籍和大文档通常用索引来归纳关键词，方便用户查询。$\LaTeX$借助`makeindex`程序完成对索引的排版。

添加索引需要在导言区调用`makeidx`宏包，并使用`\makeindex`命令开启索引收集。·

```latex
\usepackage{makeidx}
	\makeindex
```

添加索引项的命令为`\index{index-entry}`，常用写法如下：

| 类型       | 样例                 | 索引项                         |
| ---------- | -------------------- | ------------------------------ |
| 一级索引   | `test`               | test, 1                        |
| 二级索引   | `test!sub`           | &emsp;$\text{sub}$, 3          |
| 三级索引   | `test!sub!subsub`    | &emsp;&emsp;$\text{subsub}$, 5 |
| 格式化索引 | `Mobius@\""obius`    | $\text{M\\\"obius}$, 7         |
|            | `alpha@$\alpha$`     | $\alpha$, 9                    |
|            | `bold@\textbf{bold}` | $\textbf{bold}$, 11            |
| 页码范围   | `morning\|(`         | $\text{morning}$, 6-7          |
|            | `morning\|)`         |                                |

其中`!`, `@`, `|`为特殊字符，使用`"`转义，而`"`使用`""`输出。索引至多三级，以上命令可组合使用。

在需要输出索引的地方(如正文区末尾)使用`\printindex`命令。

编译命令如下：

```console
$ xelatex main % 生成索引记录文件main.idx
$ makeindex main.idx % 生成索引文件main.ind
$ xelatex main % 生成索引列表
```

详情可以查看`makeindex`宏包的[文档](https://mirrors.nju.edu.cn/CTAN/indexing/makeindex/doc/makeindex.pdf)。

# 使用`\include`和`\input`组织文件

当$\TeX$文档比较复杂(或是比较长)时，单个源文件的修改、校对、编译会变得十分困难。
此时，将源文件分割为若干子文件，如将每章内容单独写在一个文件中，会极大地简化工作。

$\LaTeX$提供两个命令`\include`和`\input`以在源代码中插入文件：

```latex
\include{filename}
%
\input{filename}
```

若引入文件和主文件不在同一个目录中，则要使用相对或绝对路径，见[使用本地字体](../international-language-support/#使用本地字体)。

两个命令各有特点：

1.	`\include`会在读入文件前另起一页，`\input`则不会。

1.	在被`\include`引用的文件中不能再次使用`\include`命令(包括被`\input`包含的文件)；而`\input`可以任意使用，相当于直接在文件中插入被引用的文件。

1.	在导言区使用指令`\includeonly{filename1, filename2, ...}`可以仅载入指定文件。

以下是一个使用`\include`和`\input`文件树结构示例：

```latex
% main.tex
\documentclass{book}
\include{header}
\begin{document}
\include{part1}
\include{part2}
\appendix
\include{appendix}
\end{document}

% part1.tex
\part{Part I}
\input{chapter1}
\input{chapter2}

% part2.tex
\part{Part II}
\input{chapter3}
\input{chapter4}
```

# 标准文档类的主文件样例

## article

```latex
\documentclass{article}

\title{Title}
\author{Author}
\date{\today}

\begin{document}
	\maketitle
	\begin{abstract}
		...
	\end{abstract}
	\tableofcontents
	\include{section1}
	\include{section2}
	\appendix
	\include{appendix}
	\bibliography{books}
\end{document}
```

## book

```latex
\documentclass{book}

\usepackage{makeidx}
	\makeindex

\usepackage[style=gb7714-2015]{biblatex}
	\addbibresource{bibliography.bib}

\title{Title}
\author{Author}
\date{\today}

\begin{document}
\frontmatter
	\maketitle
	\include{preface}
	\tableofcontents
\mainmatter
	\include{chapter1}
	\include{chapter2}
	...
	\appendix
	\include{appendixA}
	...
\backmatter
	\include{epilogue}
	\printbibliography
	\printindex
\end{document}
```