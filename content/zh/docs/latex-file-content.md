---
title:  LaTeX 文件内容
weight: 3
---
{{< katex />}}

# $\LaTeX$文件结构

在此前的[代码结构](../getting-started-with-latex/#代码结构)一节中，我们初步介绍了$\LaTeX$文件的结构。以下是文件内容的示意图。

{{<mermaid class="text-center">}}
flowchart LR
A(文件) --> B(导言)
A --> C(正文)
A --> D(忽略)
B --> E(文档类型)
B --> F(宏包, 全局设定, 注释)
C --> G(开始)
C --> H(文字, 命令, 环境, 注释)
C --> I(结束)
{{</mermaid>}}

正文部分的内容由文字，命令，环境，注释组成。一般来说，文字会被按照原样处理为文档的内容，其余部分会按照$\LaTeX$的语法规则进行处理。我们将分别介绍这些部分的内容。

# 文字

## 空格

1.	`\n([ \t]*\n)+ -> 段落终止`: 两个文段间的空行定义段落的终止，多个空行被视为一个空行。
1.	`(?<=\n)[ \t]+ -> 忽略, (?<!\n)([ \t]+|[ \t]*\n) -> 空格`: 
	空白符，如空格键、`tab`键输入的字符皆视为空格，连续的多个空格视为一个空格。行头空格忽略不计，而单个换行符亦视为空格。 

以下是一个例子：

{{<columns>}}

## 源代码

```latex
It does not matter whether you
enter one or several     spaces
after a word.

An empty line starts a new
paragraph.
```

<--->

## 编译结果

It does not matter whether you enter one or several spaces after a word.

An empty line starts a new paragraph.
{{</columns>}}

### 单词间距与断行

在进行西文排版时，为了使文字达到右边界，$\LaTeX$会适度调整单词间距。为提高可读性，其也会在句尾稍加间距。$\LaTeX$会自动选择断行位置。若在空格处断行，会舍去空格生成的间距；若在词中断行，会生成连接符。

$\LaTeX$的默认句终止符为句号`.`，问号`?`与感叹号`!`。若句号紧随大写字母，则其不会处理为语句终止，这是因为句号常出现于单词缩写中，如`Q.E.D.`。

你可以以特殊命令改变当前空格和句号的规则。
如`~`会生成不调整间距，亦不断行的空格。
而命令`\@`则会指定其紧随的句号为语句终止，即使其前为大写字母。

例子见下

{{<columns>}}

## 源代码

```latex
Mr.~Smith was happy to see her\\
cf.~Fig.~5\\
I like BASIC\@. What about you?
```

<--->

## 编译结果

Mr. Smith was happy to see her

cf. Fig. 5

I like BASIC. What about you?

{{</columns>}}

以下命令禁止句尾的额外间距：
```latex
\frenchspacing
```

这在非英文语言中是常见的，若你使用该命令，命令`\@`非必要。

## 特殊字符

### 保留字符

多数字符在$\LaTeX$中为其本义，但以下字符有特殊用途：

<center># $ % ^ & _ { } ~ \</center>

其中`$`，`^`，`_`用于数学公式排版，`&`用于表格排版，`~`用途见上，`%`用于注释。
若想在文档中使用其本义，须在其前面加上`\`，如`\$`。`\`为例外，需要使用命令`\textbackslash`(在数学环境为`\backslash`)。细表见下：

 |  \#   |   $   |   %   |    ^    |   &   |  \_   |  \{   |  \}   |    ~    |               \\                |
 | :---: | :---: | :---: | :-----: | :---: | :---: | :---: | :---: | :-----: | :-----------------------------: |
 | \\\#  |  \\$  |  \\%  | \\^\{\} |  \\&  | \\\_  | \\\{  | \\\}  | \\~\{\} | \\textbackslash \(\\backslash\) |

### 引号

在$\LaTeX$不能直接使用引号，单引号`‘`和`’`分别用`` ` ``和`'`输入；双引号则用``` `` ```和`''`输入。在使用ctex宏包或文档类时，中文引号可以直接输入。

{{<columns>}}

## 源代码

```latex
``Please press the `x' key.''
```

<--->

##international-language-support/#使用本地字体 编译结果

"Please press the 'x' key."

{{</columns>}}

### 连字与破折号 (-)

$\LaTeX$按连续`-`的个数提供3种“横线”：
单个`-`用来组成复合词，
连续两个`-`用来连接数字表示范围，
连续三个`-`用来连接单词，语义上类似破折号。

{{<columns>}}

## 源代码

```latex
daughter-in-law, X-rated\\
pages 13--67\\
yes---or no? \\
$0$, $1$ and $-1$
```

<--->

## 编译结果

daughter-in-law, X-rated

pages 13–67

yes—or no?

$0$, $1$ and $-1$

{{</columns>}}

### 斜杠 (/)

在两个单词间加入斜杠`/`会使编译器将其视为一个单词，如`read/write`。
但在排版时也会禁止在行尾生成连字符，因此可能出现错误‘overfull’。
解决方案是改用`\slash`。尽管如此，普通的`/`仍然会在表示比例时使用，如`5 MB/s`.

### 度数符号 ($^\circ$)

在纯净`\LaTeX`中，使用`$^\circ$`表示度数。

```latex
It's $-30\,^{\circ}\mathrm{C}$. I will soon start to super-conduct.
```

It's ${-30\,}^{\circ}$C. I will soon start to super-conduct.

而宏包`textcomp`提供了`\textdegree`和`\textcelsius`等用于方便地表示度数。

{{<columns>}}

## 源代码

```latex
30 \textcelsius{} is 86 \textdegree{F}.
```

<--->

## 编译结果

30 $\text{\textdegree}$C is 86 $\text{\textdegree}$F.

{{</columns>}}

# 命令

$\LaTeX$ 命令以反斜杠`\`开头，大小写敏感，有以下两种形式：

*	`\\[a-zA-Z]+\*?([...]|{...})*`：
	在反斜杠后紧随若干字母，然后终止于非字母。
	部分命令可以带星号，与不带星号的命令有差异。
	部分命令提供以`[]`或`{}`包围的若干参数。
	一般来说，`[]`为可选参数，`{}`为必须参数，不可以随意调换参数的顺序。
	此外，一般来说可选参数会在必须参数的前面。
*	`\\[^a-zA-Z]`：由反斜杠及紧随的一个非字母组成。

**注意事项**：
1.	命令后的空格会被忽略。若想在命令后间隔，可以使用空参数`{}`加上空白符，或是用使用`~`，或`\ `(反斜杠加空格)。

1.	如果未使用`{}`包围必须参数，可能出现不可预料的结果。大体来说有两种情况：
	1.	以下一条命令/非空白字符作为参数。对于数学环境中的分式`\frac{}{}`，如不使用`{}`包围，例如`\frac \alpha \beta`，编译器会将其认为`\frac{\alpha}{\beta}`。

	1.	对其后的所有内容产生作用。如`\bfseries{}`，其会加粗命令后的所有内容，截至`\bfseries`所在环境结束。如`\text{\bfseries bold} normal`会加粗bold。

	**请不要省去必须参数，除非你知道如此做的后果。**

{{<columns>}}

## 源代码

```latex
New \TeX users may miss whitespaces after a command. % renders wrong 
Experienced \TeX\ users are \TeX perts, and know how to use whitespaces. % renders correct
```

<--->

## 编译结果

New $\TeX$users may miss whitespaces after a command. 
Experienced $\TeX$ users are $\TeX$perts, and know how to use whitespaces.

{{</columns>}}

第2类命令分为以下几种类型：

1.	`\#`, `\$`, `\%`, `\^{}`, `\&`, `\_`, `\{`, `\}`, `\~{}`：转义为反斜杠后的特殊字符；

1.	`\!`, `\,`, `\:`, `\;`, `\ `：转义为空格；具体宽度如下：

	| \\\! | \\, | \\: | \\; | \\  | \\quad              |
	| ---- | --- | --- | --- | --- | ------------------- |
	| \-3  | 3   | 4   | 5   | 6   | 18\(与M的宽度相同\) |

1.	`\(`, `\)`, `\[`, `\]`：分别为行内公式的开始与结束，以及行间公式的开始与结束；

1.	`\|`：数学公式中为$\\\|$；

1.	`` \` ``, `\'`, `\^`,  `\~`, `\=`, `\.`, `\"`：重音符，效果如下：

	| \\\`o   | \\\'o   | \\^o   | \\~o   | \\=o   | \\\.o   | \\\"o   |
	| ------- | ------- | ------ | ------ | ------ | ------- | ------- |
	| $\\\`o$ | $\\\'o$ | $\\^o$ | $\\~o$ | $\\=o$ | $\\\.o$ | $\\\"o$ |

1.	`\\`：结束当前行

1.	`\@`：见[单词间距与断行](#单词间距与断行)；

1.	`\-`：指定断词位置；

## 手动断行与断页

我们可以使用`\\`, `\newline`来手动断行(在`tabular`等环境中为`\\`或`\cr`)。其中`\\`有可选参数`[length]`，代表额外的垂直间距。

断页的命令有两个：`\newpage`, `\clearpage`。区别在于：在双栏排版中`\newpage`另起一栏，而`\clearpage`另起一页。

# 环境

`\begin{([a-zA-Z]+\*?)}([...]|{...})* ... \end{\1} -> 环境`：环境是一种特殊的命令，以`\begin{envname}`开头，以`\end{envname}`结尾，其中`envname`为环境名称，由字母组成，前后须相同。部分环境名支持在字母后面带星号，与不带星号的环境有差异。

环境用于令一些效果在局部生效，或是生成特殊的文档元素，[常见环境](../common-environments)会之后详细介绍。

# 注释

`%.*\n[ \t]* -> 注释`: 注释以`%`开头，截至行尾。所有字符皆被忽略，也包括下一行开头的空格。

{{<columns>}}

## 源代码

```latex
This is an % stupid
% Better: instructive <----
example: Supercal%
				ifragilist%
icexpialidocious
```

<--->

## 编译结果

This is an example: Supercalifragilisticexpialidocious.

{{</columns>}}

`%`可用于分隔不可以换行的环境。

## 多行注释

除了连续多行开头使用`%`，还有两种方案来更优雅地实现多行注释。

1.	`\iffalse`与`\fi`：编译器会忽略`\iffalse`和`\fi`之间的所有内容。该命令允许嵌套使用。
如

	{{<columns>}}

## 源代码

```latex
前面
\iffalse
	看不到
	\iffalse
		看不到
	\fi
	也看不到
\fi
后面
```

	<--->

## 编译结果

前面后面

	{{</columns>}}

1.	`\begin{comment}`与`\end{comment}`：编译器会忽略`\begin{comment}`和`\end{comment}`之间的所有内容。但是，该命令不允许嵌套，其会寻找`\begin{comment}`后的第一个`\end{comment}`作为命令的终止。

	**注意事项**：该命令需要使用宏包`comment`或`verbatim`。

	{{<columns>}}

## 源代码

```latex
前面
\begin{comment}
	看不到
	\begin{comment}
		看不到
	\end{comment}
	也看不到
% \end{comment} 若不注释，编译器会在该行报错
后面
```

<--->

## 编译结果

前面 也看不到后面[^1]

[^1]: 此处“也看不到”与“后面”间没有空格，是由于ctex的空格处理机制，若使用英文，可以看到单词间有空格，来源于注释前的换行符。

	{{</columns>}}

# 逐字输出(verbatim)

环境`verbatim`用于逐字输出，将环境中的所有字符输出为原始字符，不会根据$\LaTeX$的规则进行转义；而`verbatim*`会将空格显示为“&#9141;”。

`\verb\*?([^a-zA-Z\* \s])(.*?)\1`：需要简短地使用逐字输出，可使用`\verb`命令，其将紧邻的字符视为起始符与终止符，其间的字符将被输出为原始字符。带星号的会将空格显示为“&#9141;”。

起始符与终止符为字母、空格、星号以外的字符，一般使用`|`符号。

{{<columns>}}

## 源代码

```latex
The \verb|\ldots| command \ldots
\begin{verbatim}
10 PRINT "HELLO WORLD ";
20 GOTO 10
\end{verbatim}
```

<--->

## 编译结果

The `\ldots` command $\ldots$

10 PRINT \"HELLO WORLD \";

20 GOTO 10

{{</columns>}}

{{<columns>}}

## 源代码

```latex
\begin{verbatim*}
the starred version of
the      verbatim
environment emphasizes
the spaces   in the text
\end{verbatim*}
\verb*|like   this :-) |
```

<--->

## 编译结果

the&#9141;starred&#9141;version&#9141;of

the&#9141;&#9141;&#9141;&#9141;&#9141;&#9141;verbatim

environment&#9141;emphasizes

the&#9141;spaces&#9141;&#9141;&#9141;in&#9141;the&#9141;text

like&#9141;&#9141;&#9141;this&#9141;:-)&#9141;

{{</columns>}}