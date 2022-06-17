---
title:  编辑器推荐
weight: 7
---
{{< katex />}}

# 编辑器推荐

一个好用的$\LaTeX$编辑器无疑会极大地提高输入和编译效率，也可以让使用者有一个好的心情，不用一直面对终端手动输入指令(虽然部分人也喜欢这么做)。

本篇推荐两个笔者长期使用的编辑器，并介绍部分特性与使用方法。
本文并不致力于写成编辑器使用指南，因此主要介绍其中与$\LaTeX$相关的部分。

此外，你也可以使用你喜欢的编辑器探索如何提升$\LaTeX$文档的编辑体验。

# Visual Studio Code

[Visual Studio Code](https://code.visualstudio.com/) (简称VS Code)是由微软公司开发的跨平台免费开源的编辑器，主要用于编写程序，预设支持多数常用语言，也包括$\LaTeX$。
在2021年问答网站Stack Overflow的[开发环境调研](https://insights.stackoverflow.com/survey/2021#section-most-popular-technologies-integrated-development-environment)中，其获得了71.06%的推荐率，远超其后的Visual Studio (33.03%)等。

VS Code支持通过扩展增强功能，在其扩展商店中的[LaTeX Workshop](https://github.com/James-Yu/LaTeX-Workshop)可以极大地提升编辑器中$\LaTeX$文件的编辑和编译效率。

以下介绍其主要功能。更详细的介绍可以查看[Features](https://github.com/James-Yu/LaTeX-Workshop#features-taster)和其[Wiki](https://github.com/James-Yu/LaTeX-Workshop/wiki)。

## 一般代码支持

支持$\LaTeX$, $\LaTeX$3, Bib$\TeX$语法高亮、代码折叠、代码格式化。

## 自动编译

LaTeX Workshop默认会在你保存文件时自动编译$\LaTeX$文档，
因此可以告别生成引用、文献、索引等多次编译的烦恼。

如果使用`\input`, `\include`来形成文件树，其会智能地在保存树中任意文件时重新编译主文件。

此外，可以选择删除编译过程中出现的辅助文件。

该设定可以关闭。

![Build](https://raw.githubusercontent.com/James-Yu/LaTeX-Workshop/master/demo_media/build.gif)

## PDF预览和SyncTeX支持

LaTeX Workshop支持在VS Code内与外部PDF查看器实时预览编译出的PDF文档。

![Preview](https://raw.githubusercontent.com/James-Yu/LaTeX-Workshop/master/demo_media/preview.gif)

此外，支持通过SyncTeX从文档中的`\label`和`\ref`处跳转PDF至相应部分，或是从PDF任意部分跳转至生成该部分的一行(同样支持访问文件树)。

![SyncTeX](https://raw.githubusercontent.com/James-Yu/LaTeX-Workshop/master/demo_media/synctex.gif)

## Snippets, Shortcuts 与 IntelliSense

智能提示宏命令(包含可能的参数类型)，`\cite`和`\ref`引用内容，以及`\input`, `\include`, `\includegraphics`等文件导入路径，可以选择并按`tab`键补完。

![IntelliSense](https://raw.githubusercontent.com/James-Yu/LaTeX-Workshop/master/demo_media/ref.gif)

智能生成列举环境中的`\item`，

![Auto Item](https://raw.githubusercontent.com/James-Yu/LaTeX-Workshop/master/demo_media/auto%20item.gif)

更方便地给文本提供`\emph`等样式。

![Emph](https://raw.githubusercontent.com/James-Yu/LaTeX-Workshop/master/demo_media/emph.gif)

此外，可以通过VS Code自定义代码片段，形成适合个人的代码片段。

## 数学公式和TikZ绘图，图片预览

将光标置于数学公式与TikZ绘图，或图片插入处可以看到渲染效果。

![Hover](https://raw.githubusercontent.com/James-Yu/LaTeX-Workshop/master/demo_media/hover.gif)

## 错误分析

将编译报错显示于文件中。

![Errors](https://raw.githubusercontent.com/James-Yu/LaTeX-Workshop/master/demo_media/errors.png)


## 大纲，代码片段插入

在资源管理器->大纲处(或$\TeX$->STRUCTURE处)可以看到树状组织的全部章节和标签，支持点击跳转。

在$\TeX$->SNIPPET VIEW处可以根据符号插入对应的命令，以及常用的TikZ绘图片段。

## 其它插件

你也可以在扩展商店搜索自己喜欢的扩展。
如笔者会使用hypersnips(借助Vim中的王牌插件Ultisnips灵感创作)以根据上下文(context)快速自动展开代码片段。
由于其目前为beta版，存在部分问题，故此处不介绍。

# VIM

[Vim](https://www.vim.org/)是从vi发展出的开源自由文本编辑器，于1991年发布，可以在终端使用，是类Unix系统用户最喜欢的编辑器。其以学习曲线陡峭著称，但一旦掌握后能大幅提高编辑效率。

笔者因著名文章[How I'm able to take notes in mathematics lectures using LaTeX and Vim](https://castel.dev/post/lecture-notes-1/)入坑。
虽有差生文具多之嫌，但经过测试确实能够与课堂同步做笔记(而笔者并不喜欢做笔记)，可以在无需思考的情况下高速输出文字。

本部分推荐主要参考上述文章，此外会增加部分个人的使用体验。

<!-- todo -->