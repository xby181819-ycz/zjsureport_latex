# 浙工商课程论文 LaTeX 模板说明

该仓库提供浙江工商大学课程论文latex模板和word模板，可用于课程论文撰写

主要工作目录在 [`LATEX模板/`](./LATEX模板/)。

- 主文件：[`LATEX模板/main.tex`](./LATEX模板/main.tex)
- 样式文件：[`LATEX模板/zjsureport.sty`](./LATEX模板/zjsureport.sty)
- 参考文献库：[`LATEX模板/reference.bib`](./LATEX模板/reference.bib)
- 图片资源：[`LATEX模板/figures/`](./LATEX模板/figures/)

建议使用 `XeLaTeX` 编译。

## 快速上手

### 1. 修改页眉右侧文字

页眉右侧“课程论文：R语言”由样式文件中的两个位置共同决定：

- 课程名变量在 `LATEX模板/zjsureport.sty` 第 `40` 行
  ```tex
  \newcommand{\reportcourse}{...}
  ```
- 页眉右侧实际渲染在 `LATEX模板/zjsureport.sty` 第 `91` 行
  ```tex
  \fancyhead[R]{... 课程论文：\reportcourse}
  ```

常见做法是只改 `\reportcourse`，不直接改页眉渲染行。

### 2. 修改封面“《R 语言》课程论文”

封面顶部这行文字由变量控制：

- 标题变量在 `LATEX模板/zjsureport.sty` 第 `41` 行
  ```tex
  \newcommand{\reporttitlecn}{...}
  ```
- 封面实际使用位置在 `LATEX模板/zjsureport.sty` 第 `114` 行
  ```tex
  {\bfseries\zihao{1}\reporttitlecn\par}
  ```

通常只改 `\reporttitlecn` 即可。

### 3. 修改论文题目

题目相关有两处：

- 题目变量在 `LATEX模板/zjsureport.sty` 第 `42` 行
  ```tex
  \newcommand{\reporttopic}{...}
  ```
- 封面“题目：”使用位置在 `LATEX模板/zjsureport.sty` 第 `118` 行
- 摘要页顶部标题使用位置在 `LATEX模板/zjsureport.sty` 第 `137` 行

如果你只想换题目文本，改 `\reporttopic` 即可，封面和摘要页会同时跟着变。

### 4. 修改学院、专业、学号等封面信息

这些字段都集中定义在样式文件前部：

- 学院：`LATEX模板/zjsureport.sty` 第 `43` 行
- 专业：`LATEX模板/zjsureport.sty` 第 `44` 行
- 学号：`LATEX模板/zjsureport.sty` 第 `45` 行
- 学生姓名：`LATEX模板/zjsureport.sty` 第 `46` 行
- 成绩：`LATEX模板/zjsureport.sty` 第 `47` 行
- 日期：`LATEX模板/zjsureport.sty` 第 `48` 行

封面字段排版统一在 `LATEX模板/zjsureport.sty` 第 `120` 到 `128` 行。

### 5. 参考文献引用格式

当前模板使用的是：

- 主文件加载：`LATEX模板/main.tex` 第 `3` 行
  ```tex
  \usepackage{gbt7714}
  ```
- 正文引用示例：`LATEX模板/main.tex` 第 `22` 行
  ```tex
  \cite{gu2020xgboost}
  ```
- 参考文献输出命令：`LATEX模板/main.tex` 第 `60` 行
  ```tex
  \reference
  ```
- 样式定义位置：`LATEX模板/zjsureport.sty` 第 `159` 到 `164` 行
  ```tex
  \bibliographystyle{gbt7714-numerical}
  \bibliography{reference}
  ```

参考文献数据文件是 [`LATEX模板/reference.bib`](./LATEX模板/reference.bib)。

## 进阶调整

这一部分列出模板里常改的布局参数。

### 1. 页眉图标大小与位置

页眉左侧两个图标都在 `LATEX模板/zjsureport.sty` 第 `85` 到 `89` 行：

```tex
\fancyhead[L]{%
  \hspace*{0.5cm}%
  \raisebox{0cm}{\includegraphics[height=1.27cm]{figures/zjgsu_badge.png}}%
  \hspace{0.5cm}%
  \raisebox{0cm}{\includegraphics[width=4.75cm,height=1.38cm]{figures/zjgsu_header_wordmark.png}}%
}%
```

可调参数：

- `\hspace*{0.5cm}`：两张图整体左右移动
- 第一个 `\raisebox{0cm}`：校徽上下微调
- `height=1.27cm`：校徽大小
- 中间 `\hspace{0.5cm}`：两图之间的间距
- 第二个 `\raisebox{0cm}`：校名字图上下微调
- `width=4.75cm,height=1.38cm`：校名字图大小

### 2. 页眉横线粗细、上下位置

页眉横线在 `LATEX模板/zjsureport.sty` 第 `94` 到 `97` 行：

```tex
\renewcommand{\headrule}{%
  \vspace{0.4cm}%
  {\color{black}\hrule width\headwidth height\headrulewidth}%
}
```

可调参数：

- `\vspace{0.4cm}`：横线相对页眉内容的上下位置
- `height\headrulewidth`：横线厚度实际由 `\headrulewidth` 决定

如果你要改粗细，通常直接把这里改成固定值更直观，例如：

```tex
{\color{black}\hrule width\headwidth height 0.6pt}%
```

### 3. 页眉上下距离

控制页眉和版心关系的主要参数在 `LATEX模板/zjsureport.sty` 第 `3` 到 `12` 行，以及第 `80` 到 `81` 行：

- `top=2.54cm`：页面顶部边距
- `headheight=44pt`：页眉区域高度
- `headsep=18pt`：页眉与正文的初始间距
- `\setlength{\headsep}{0.8cm}`：最终生效的页眉与正文间距
- `\setlength{\footskip}{1.75cm}`：页脚位置

注意：后面的 `\setlength{\headsep}{0.8cm}` 会覆盖前面 `geometry` 里的 `headsep=18pt`。

### 4. 页眉右侧文字字体与大小

页眉右侧文字在 `LATEX模板/zjsureport.sty` 第 `91` 行：

```tex
\fancyhead[R]{\songti\fontsize{9pt}{11.25pt}\selectfont 课程论文：\reportcourse}
```

可调参数：

- `\songti`：字体
- `\fontsize{9pt}{11.25pt}`：字号与行距
- `课程论文：\reportcourse`：显示内容

### 5. 每页第一行离最上面的位置

这一项主要由页面边距和页眉共同决定，相关参数有：

- `LATEX模板/zjsureport.sty` 第 `6` 行 `top=2.54cm`
- `LATEX模板/zjsureport.sty` 第 `8` 行 `headheight=44pt`
- `LATEX模板/zjsureport.sty` 第 `80` 行 `\setlength{\headsep}{0.8cm}`

如果你觉得正文第一页第一行太高或太低，一般优先调：

1. `top`
2. `headheight`
3. `\headsep`

### 6. 各个部分字体、行间距等参数

#### 全文基础字体与行距

在 `LATEX模板/zjsureport.sty` 第 `30` 到 `38` 行：

- `\setmainfont{Times New Roman}`：西文字体
- `\setsansfont{Arial}`：西文无衬线字体
- `\setCJKmainfont{SimSun}`：中文正文字体
- `\setCJKsansfont{SimHei}`：中文黑体
- `\setCJKmonofont{FangSong}`：中文等宽/仿宋
- `\setstretch{1.25}`：全局行距
- `\setlength{\parindent}{2em}`：首行缩进

#### 章节标题字体与间距

在 `LATEX模板/zjsureport.sty` 第 `57` 到 `62` 行：

- `\section`：章标题格式
- `\subsection`：节标题格式
- `\subsubsection`：小节标题格式
- `\titlespacing*{...}`：各级标题上下间距

#### 封面字体与间距

在 `LATEX模板/zjsureport.sty` 第 `112` 到 `128` 行：

- `\zihao{1}`：封面大标题字号
- `\zihao{3}`：封面题目、日期字号
- 各处 `\vspace{...}`：封面垂直间距
- `\coverfield` 的定义在 `LATEX模板/zjsureport.sty` 第 `106` 行

#### 摘要与关键词

摘要部分在 `LATEX模板/zjsureport.sty` 第 `134` 到 `156` 行：

- `\maketitle`：摘要页顶部题目
- `abstract` 环境：摘要标题与摘要正文
- `\keywords{...}`：关键词样式

#### 代码附录

代码块样式在 `LATEX模板/zjsureport.sty` 第 `71` 到 `78` 行：

- `basicstyle=\ttfamily\small`：代码字体和字号
- `breaklines=true`：长行自动换行
- `frame=none`：无边框


