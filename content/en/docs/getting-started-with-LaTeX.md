---
title: Getting Started with LaTeX
weight: 1
---
{{< katex />}}
# Installing the $\TeX$ software

To use $\LaTeX$, you will need access to a computer with $\LaTeX$ installed, or [download](https://www.latex-project.org/get/) and install a $\TeX$ distribution on your own computer. 

# Your first $\LaTeX$ file

1.	Create a new file below. 
	You can name it anything you like, but it should be a .tex file.

	```latex
	% helloworld.tex
	\documentclass{article}
	\begin{document}
	Hello, World!
	\end{document}
	```

2.	Open a shell or cmd window, `cd` to the directory containing the file, and run `xelatex` on your file. 
	If successful, you should see a PDF file called `helloworld.pdf` in the same directory.

	```bash
	$ cd /path/to/your/folder
	$ xelatex helloworld
	```
	When your file has a bug $\LaTeX$ will tell you about it and stop processing. Type
	`ctrl-D` to get back to the shell.

# File structure

When $\LaTeX 2 \varepsilon$ processes an input file, it expects it to follow a certain structure. Thus every input file must start with the command

```latex
\documentclass{...}
```

This specifies what sort of document you intend to write. 
After that, add commands to influence the style of the whole document, 
or load packages that add new features to the LATEX system. 
To load such a package you use the command

```latex
\usepackage{...}
```

When all the setup work is done, you start the body of the text with the command

```latex
\begin{document}
```

Now you enter the text mixed with some useful $\LaTeX$ commands. 
At the end of the document you add the

```latex
\end{document}
```

command, which tells $\LaTeX$ to call it a day. 
Anything that follows this command will be ignored by $\LaTeX$.

# The layout of the document

1.	**document class**: 
	The first information LATEX needs to know when processing an input file is the type of document the author wants to create. 
	This is specified with the `\documentclass` command.
	```latex
	\documentclass[options]{class}
	```
	The following table lists some common document classes and options:

  | **Class** | **Description**                                                                           |
  | --------- | ----------------------------------------------------------------------------------------- |
  | article   | For short documents and journal articles\. Is the most commonly used\.                    |
  | report    | For longer documents and dissertations\.                                                  |
  | book      | Useful to write books                                                                     |
  | beamer    | Slides in the Beamer class format\. See the beamer documentation for a better description |


  | **Options**        | **Description**                                                                                                |
  | ------------------ | -------------------------------------------------------------------------------------------------------------- |
  | \(\\d\+\)pt        | Sets the size of the main font in the document\. default: 10pt                                                 |
  | \(\\w\+\)paper     | Defines the paper size\. default: letterpaper\. Other values: a5paper, b5paper, executivepaper, and legalpaper |
  | fleqn              | Typesets displayed formulae left\-aligned instead of centred\.                                                 |
  | leqno              | Places the numbering of formulae on the left hand side instead of the right\.                                  |
  | \(no?\)titlepage   | Specifies whether a new page should be started after the document title or not\.                               |
  | \(one\|two\)column | Instructs $\LaTeX$ to typeset the document in one column or two columns\.                                      |
  | \(one\|two\)side   | Specifies whether double or single sided output should be generated\.                                          |

2.	**packages**: While writing your document, 
	you will probably find that there are some areas where basic $\LaTeX$ cannot solve your problem. 
	If you want to include graphics, coloured text or source code from a file into your document, you need to enhance the capabilities of LATEX. 
	Such enhancements are called packages. Packages are activated with the command

	```latex
	\usepackage[options]{package}
	% or
	\usepackage[options]{package1, package2, ...}
	```

	Modern $\TeX$ distributions come with a large number of packages prein-stalled. 
	If you are working on a Unix system, use the command

	```bash
	$ texdoc package
	```

	for accessing package documentation.
