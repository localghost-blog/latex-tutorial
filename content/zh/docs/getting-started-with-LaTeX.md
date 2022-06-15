---
title: 初次使用 LaTeX
weight: 1
---
{{< katex />}}

# 准备工作

使用$\LaTeX$前，你需要有一台已安装$\LaTeX$的电脑，或者前往The LaTeX Project官网[下载](https://www.latex-project.org/get/)并安装一个$\TeX$发行版。

如官网不方便访问，可以访问清华大学开源软件镜像站获取$\TeX$发行版，其中Windows系统或Linux系统使用[TeX Live](https://mirrors.tuna.tsinghua.edu.cn/CTAN/systems/texlive/Images/)，而MacOS使用[MacTeX](https://mirrors.tuna.tsinghua.edu.cn/CTAN/systems/mac/mactex/)。

或者通过命令行下载并安装$\TeX$发行版，如下：

{{<tabs "get-tex">}}

{{<tab "Windows">}}
```console
$ choco install texlive
```
{{</tab>}}

{{<tab "MacOS">}}
```console
$ brew cask install mactex
# 或者
$ brew cask install basictex
```
{{</tab>}}

{{<tab "Ubuntu">}}
```console
$ apt install texlive
# or
$ apt install texlive-base
```
{{</tab>}}

{{</tabs>}}

此外，也可以访问[Overleaf](https://www.overleaf.com)等在线服务以联网使用$\LaTeX$。

以下以本地运行为例。

# 第一个$\LaTeX$文件

1.	创建新文件如下。可以使用任意名字，但建议以`.tex`结尾。 

	```latex
	% helloworld.tex
	\documentclass{article}
	\begin{document}
	Hello, World!
	\end{document}
	```

2.	打开命令行， 用命令 `cd` 切换至文件所在目录，然后运行`xelatex`。 
	编译成功后，你会在当前目录发现`helloworld.pdf`以及一些其它文件。

	```shell
	$ cd /path/to/your/folder
	$ xelatex helloworld # or xelatex helloworld.tex
	```

	若编译失败，则会显示错误信息，并停止编译。此时按`ctrl-D`(MacOS下为`control-D`)返回命令行。

# 代码结构

一个合法的$\LaTeX$代码需要正确格式以使编译程序处理。一般来说，任何一个$\TeX$文件需要以以下命令开始：

```latex
\documentclass{...}
```

该命令指定了PDF文档的类型(如文章、书籍、演示文稿等)。
在此之后，可以添加命令来改变文档的样式，或者加载宏包(package)以获取拓展功能。
加载宏包的命令如下：

```latex
\usepackage{...}
```

完成所有准备工作后，用以下命令进入正文内容。正文内容以前的部分称为导言(preamble)。

```latex
\begin{document}
```

正文内容包括$\LaTeX$命令以及普通文本。
在正文结束后，用以下命令结束文档。

```latex
\end{document}
```

该命令后的任何字符将被忽略。

在[LaTeX 文件内容](../latex-file-content)一章会具体展开代码结构和内容的讨论，在此之前我们先介绍一些常用的文档类型。

# 文档导言

1.	**文档类型:** 
	文档类型由命令`\documentclass`指定:
	```latex
	\documentclass[options]{class}
	```
	其中`class`是文档类型的名称，控制整篇文档的大致风格，而`[]`内的部分提供一些参数的调整，可以如前文样例一样省去或置空。常用的名称和参数见以下表格：

  | **class** | **描述**                                                       |
  | --------- | -------------------------------------------------------------- |
  | article   | 文章格式，常用于科技论文、短篇报告、说明文档等。               |
  | report    | 报告格式，适用分数个章节的长篇报告，或是短篇书籍、博士论文等。 |
  | book      | 书籍格式。                                                     |
  | beamer    | 演示文稿格式，适于做报告时配合使用。                           |


  | **options**        | **描述**                                                                                                                                             |
  | ------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------- |
  | \(\\d\+\)pt        | 设置正文主要字体大小。如`12pt`，默认为`10pt`。                                                                                                       |
  | \(\\w\+\)paper     | 设置页面大小。默认为`letterpaper`(8.5in$\times$11in，约合21.6cm$\times$28.0cm)。其它可选值有`a5paper`，`b5paper`，`executivepaper`及`legalpaper`等。 |
  | fleqn              | 行间公式左置。默认居中。                                                                                                                             |
  | leqno              | 公式编号左置。默认居右。                                                                                                                             |
  | \(no\)?titlepage   | 设置命令`\maketitle`是否生成单独页。`article`默认为`notitlepage`，`report`，`book`默认为`titlepage`。                                                |
  | \(one\|two\)column | 单/双列排版。默认为单列。                                                                                                                            |
  | \(one\|two\)side   | 单/双面排版。双面时奇偶页页眉页脚及页边距不同。`artcle`，`report`默认为单面，`book`默认为双面                                                        |

以下是一个合法(但没必要)的文档类型命令

```latex
\documentclass[10pt, letterpaper, titlepage, onecolumn, twoside]{book}
```

2.	**宏包:** 编写文档时偶尔会发现部分需求难以用最基本的$\LaTeX$实现，例如插入图片，文字上色、高亮代码等。此时一般可以通过使用宏包来简单实现。
	宏包用以下命令调用：

	```latex
	\usepackage[options]{package}
	% 或者
	\usepackage[options]{package1, package2, ...}
	```

	其中`package`是宏包的名称，`options`是宏包的参数。可以一次性调用多个宏包，但参数作用于所有宏包。

	现代的$\TeX$发布版有大量的预安装宏包，可以使用命令`texdoc`来阅读已安装宏包的文档：

	```bash
	$ texdoc package
	```