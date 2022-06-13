---
title:  多语言支持
weight: 2
---
{{< katex />}}

# 多语言支持

现代的$\TeX$引擎，如XeTeX和LuaTeX，原生支持UTF-8编码。如下：

{{< columns >}}

## 源代码

```latex
\documentclass{article}
\begin{document}
Français Português Español Føroyskt
\end{document}
```
<--->

## 编译结果

Français Português Español Føroyskt

{{< /columns >}}

然而非拉丁字母无法直接在$\LaTeX$中使用，如西里尔字母、希腊字母、阿拉伯字母以及东亚文字等。

我们主要介绍中文的支持，提供两种解决方案。

## 方案一：xeCJK宏包

xeCJK是一个XeLaTeX宏包，用于排版中日韩(CJK)文字，有以下功能：
1.	分别设置CJK与英文字体；
1.	自动忽略CJK文字间空格(保留其它空格)，允许在非标点汉字和英文字母间断行；
1.	提供多种标点处理方式；
1.	自动调整中英文间空白。

在引入宏包后，须指定CJK文字的字体，然后可以在文档中自由使用中日韩文字。

更多特性及设定见其[文档](http://mirrors.ibiblio.org/CTAN/macros/xetex/latex/xecjk/xeCJK.pdf)。

{{< columns >}}

## 源代码

```latex
\documentclass{article}
\usepackage{xeCJK}
\setCJKmainfont{SimSun}
\begin{document}
汉语测试
\end{document}
```

<--->

### 编译结果

汉语测试

{{< /columns >}}

## 方案二：ctex宏包与文档类

另一种方式是使用ctex宏包与文档类，其进一步封装了CJK，xeCJK，luatexja等宏包，
使得用户在排版时无须考虑排版引擎等细节。

**注意事项**：该方案会改变默认的页码位置，如果需要使用默认的页码位置，请在文档中使用以下命令：

```latex
\usepackage{fancyhdr}
	\pagestyle{fancy}
	\lfoot{}
```

{{<tabs "ctex">}}

{{<tab "ctexart文档类">}}
```latex
\documentclass{ctexart}
\begin{document}
少写两行太好用啦！
\end{document}
```
{{</tab>}}

{{<tab "ctex宏包">}}
```latex
\documentclass{article}
\usepackage{ctex}
\begin{document}
多了一行
\end{document}
```
{{</tab>}}

{{</tabs>}}

ctex会自动寻找中文字体。默认的字体如下：

|          | Windows             | MacOS           | Linux      |
| -------- | ------------------- | --------------- | ---------- |
| XeLaTeX  | 中易字库 + 微软雅黑 | 华文字库 + 苹方 | Fandol字库 |
| LuaLaTeX | 中易字库 + 微软雅黑 | 华文字库 + 苹方 | Fandol字库 |
| pdfLaTeX | 中易字库 + 微软雅黑 | 不可用          | 不可用     |

也可以使用`\setCJKmainfont{}`命令来设置中文字体。

更多特性及设定见其[文档](http://mirrors.ibiblio.org/CTAN/language/chinese/ctex/ctex.pdf)。


# 字体使用

## 使用本机安装字体

XeTeX通常使用fontconfig库查找和调用字体，因此可以用fc-list命令显示可用的字体。
在命令行运行以下命令：

```console
$ fc-list > fontlist.txt
```

可将系统中所有安装的字体列表存入`fontlist.txt`文件中。
而可用于CJK字体参数的字体名可用以下命令：

```console
$ fc-list -f "%{family}\n" :lang=zh > zhfont.txt
```

以下是部分预装字体
{{<tabs "zh-font">}}
{{<tab "Windows">}}
```console
$ fc-list -f "%{family}\n" :lang=zh
方正姚体,FZYaoTi
黑体,SimHei
微软雅黑,Microsoft YaHei
华文仿宋,STFangsong
华文楷体,STKaiti
华文隶书,STLiti
幼圆,YouYuan
```
{{</tab>}}
{{<tab "MacOS">}}
```console
$ fc-list -f "%{family}\n" :lang=zh
苹方-简,蘋方-簡,PingFang SC
.苹方-繁,.蘋方-繁,.PingFang TC
苹方-繁,蘋方-繁,PingFang TC
黑体-繁,黑體-繁,Heiti TC,黒体-繁,Heiti-번체
.苹方-繁,.蘋方-繁,.PingFang TC
黑体-繁,黑體-繁,Heiti TC,黒体-繁,Heiti-번체
```
{{</tab>}}
{{<tab "Ubuntu">}}
```console
$ fc-list -f "%{family}\n" :lang=zh
AR PL Mingti2L Big5,文鼎ＰＬ細上海宋
AR PL KaitiM GB,文鼎ＰＬ简中楷
AR PL KaitiM Big5,文鼎ＰＬ中楷
AR PL SungtiL GB,文鼎ＰＬ简报宋
Droid Sans Fallback
```
{{</tab>}}
{{</tabs>}}

以Windows系统为例，以下使用黑体方式均合法。

```latex
\setCJKmainfont{黑体}
% 或者
\setCJKmainfont{SimHei}
```

## 使用本地字体

若要使用本地字体，可以使用`\setCJKmainfont[options]{fontname}`命令，其中参数`options`为本地字体相对**命令行当前路径**的路径，`fontname`为字体名。

使用样例如下：

```latex
% folder/src/main.tex
\documentclass{ctexart}
\setCJKmainfont[Path=fonts/]{LXGWWenKaiScreen}
% located in folder/fonts/
\begin{document}
叽里呱啦。
\end{document}
```
```console
foo@bar:folder$ xelatex src/main
```