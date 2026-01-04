---
name: latex-document-writer
description: Assitant with the creation and modification about LaTeX Projects。Such as writing chapters, adding figures, creating tables, formatting code blocks, etc.
---

# latex-document-writer

当你作为 AI 助手参与本项目时，请严格遵守以下指令，以确保文档逻辑一致、编译通过且排版精美。

## 1. 编译与保存规则 (核心限制)
- **严禁在终端执行任何编译命令**（如 `pdflatex`, `xelatex`, `latexmk` 等）。
- **执行逻辑**：本项目已通过 VS Code 的 LaTeX Workshop 插件配置了自动编译。
- **你的任务**：仅负责编写或修改 `.tex` 代码并**执行保存操作**。所有的 `out/` 重定向、中间文件清理均由用户的 `settings.json` 自动处理。

## 2. 项目目录结构规范
必须维持以下文件层级，禁止随意在根目录创建内容文件：
- **根目录**：仅存放 `main.tex`、`.cursorrules` 及管理配置文件。
- **章节内容**：必须存放在 `latex/chapter[n]/[n.tex]`（例如：第一章的latex源码文件1.tex就这样存放于`latex/chapter1/1.tex`）。
- **资源与配置**：图片统一存放于 `figures/`，全局宏包与样式定义位于 `latex/config.tex`（没有明确要求，请不要修改该配置文件），参考文献存放于 `bib/`。

## 3. 环境与格式约束
### 3.1 写作风格与段落组织 (Writing Style)

文档的核心表现形式是**连贯的段落文字**，而非罗列式的分点。分点叙述仅作为辅助手段，在确有必要时才可使用。

**段落优先原则**：
- 当内容具有连贯的逻辑推导、因果关系或叙事性质时，必须以完整段落形式呈现，禁止将其强行拆解为列表。
- 只有当内容天然呈现并列、枚举特征（如：列举多个独立的选项、步骤或要点），且每项内容简短时，才可使用 `enumerate` 列表。
- **判断标准**：如果你发现自己正在将一个完整的句子拆成多个 `\item`，请停下来，改用段落。

**禁止连续分点**：
- 严禁在一个 `enumerate` 列表结束后，紧接着又开启另一个 `enumerate` 列表。
- 两个列表之间必须有实质性的段落文字（至少一个完整的过渡段落）进行衔接和解释，而非简单的一句引导语。

### 3.2 层次结构与列表规则 (Hierarchy & List Rules)

**标题层级**：文档正文遵循三级标题结构（`\section` -> `\subsection` -> `\subsubsection`）。

**三级标题前的决策逻辑**：在未达到 `\subsubsection` 前，若需对内容进行拆解，请根据内容体量选择表现形式：
- 若分点内容仅为寥寥数语、短句或摘要性质，使用带有 `[label={(\arabic*)}]` 参数的 `enumerate` 环境。
- 若分点内容包含大量长句、详细的技术推导或需要多个段落展开论述，使用下一级标题。

**三级标题后的列表**：在 `\subsubsection` 之后若需进一步细分内容，且内容符合上述"段落优先原则"中的列表使用条件时，必须使用带有参数 `[label={(\arabic*)}]` 的 `enumerate` 环境。

**禁令**：在任何情况下，禁止使用 `itemize` 或不带参数的默认 `enumerate`。

**代码示例**：
```latex
% 情境 A：内容具有连贯逻辑，使用段落
\subsection{指针的本质}
指针是 C 语言中用于存储内存地址的变量。当我们声明一个指针时，
编译器会为其分配足够的空间来保存一个地址值。这个地址指向内存中
的某个位置，而该位置存储着我们真正关心的数据。理解这一点对于
掌握指针至关重要，因为它揭示了指针与普通变量的本质区别。

% 情境 B：内容天然并列且简短，使用列表
\subsection{声明指针的三要素}
声明一个指针变量需要明确以下三个要素：
\begin{enumerate}[label={(\arabic*)}]
  \item 指针所指向数据的类型
  \item 星号 (*) 表明这是一个指针
  \item 指针变量自身的名称
\end{enumerate}

理解了这三个要素之后，我们就可以开始探讨指针的初始化问题了...
（此处应有过渡段落，而非紧接另一个列表）
  ```

### 3.3 文本样式
- **禁止加粗**：除非用户明确要求，否则禁止在 `\item` 开头自动添加 `\textbf{...}`。
- **风格**：保持技术文档的简洁、专业，避免口语化。

### 3.4 源代码行宽限制 (Line Width)

为适应窄屏编辑环境，`.tex` 源文件中的**中文段落文字**每行应控制在约 **25 个汉字**左右，然后手动换行。LaTeX 中单次换行不会产生分段效果（需空一行才分段），因此这样做不影响最终排版，却能显著提升源码在窄窗口下的可读性。

**适用范围**：
- 所有连续的中文段落正文。
- `\item` 内的长句描述。

**例外情况**（允许超出 25 字）：
- 必须保持在同一行的功能性代码，如 `\begin{...}`、`\end{...}`、`\section{...}` 等 LaTeX 命令。
- `lstlisting` 环境内的 C 语言代码（遵循代码自身的格式规范）。
- 表格单元格、数学公式等结构化内容。

**正确示例**：
```latex
指针是 C 语言中用于存储内存地址的变量。
当我们声明一个指针时，编译器会为其分配
足够的空间来保存一个地址值。这个地址指向
内存中的某个位置，而该位置存储着我们真正
关心的数据。
```

## 4. 代码块规范
- **环境选择**：必须使用 `latex/config.tex` 中定义的 `\begin{lstlisting}` 环境。
- **语言指定**：根据文章上下文自动判断所需的编程语言，并显式指定 `language=` 参数（如 `C`, `Python`, `Java`, `JavaScript`, `SQL` 等）。
- **元数据要求**：每个代码块必须包含 `caption`（中文说明）和 `label`（格式：`lst:关键字`）。
- **示例**：
  ```latex
  % C 语言示例
  \begin{lstlisting}[language=C, caption={指针初始化示例}, label={lst:ptr_init}]
  int *p = NULL;
  \end{lstlisting}

  % Python 示例
  \begin{lstlisting}[language=Python, caption={列表推导式示例}, label={lst:list_comp}]
  squares = [x**2 for x in range(10)]
  \end{lstlisting}
  ```

## 5. 图像与绘图 (Figures & TikZ)

### 5.1 决策逻辑
根据内容性质选择合适的图形方案：

**使用 TikZ 的场景**（推荐优先考虑）：
- 简单的流程图、框图、树状结构
- 内存布局示意图（栈、堆的可视化）
- 指针指向关系图
- 数据结构图示（链表、数组等）
- 简单的几何图形或示意图

**使用外部图片的场景**：
- 复杂的截图或照片
- 第三方工具生成的图表
- 需要特殊效果的插图

### 5.2 TikZ 绘图规范

**基本模板**：
```latex
\begin{figure}[H]
  \centering
  \begin{tikzpicture}[scale=0.8]
    % TikZ 绘图代码
    \node[draw, rectangle] (a) at (0,0) {节点A};
    \node[draw, rectangle] (b) at (3,0) {节点B};
    \draw[->] (a) -- (b);
  \end{tikzpicture}
  \caption{图形说明文字}
  \label{fig:example}
\end{figure}
```

**常用 TikZ 元素示例**：

**(1) 内存布局图**：
```latex
\begin{tikzpicture}
  % 栈区
  \draw[thick] (0,0) rectangle (2,3);
  \node at (1,3.3) {栈 (Stack)};
  \draw (0,2.5) -- (2,2.5);
  \node at (1,2.75) {\small 局部变量};
  
  % 堆区
  \draw[thick] (3,0) rectangle (5,3);
  \node at (4,3.3) {堆 (Heap)};
  \node at (4,1.5) {\small 动态分配};
  
  % 箭头指向
  \draw[->, thick] (2.2,2) -- (2.8,2) node[midway,above] {\tiny 指针};
\end{tikzpicture}
```

**(2) 指针指向图**：
```latex
\begin{tikzpicture}[
  box/.style={draw, rectangle, minimum width=1.5cm, minimum height=0.8cm}
]
  \node[box] (ptr) at (0,0) {p};
  \node[box] (var) at (4,0) {100};
  \draw[->, thick] (ptr.east) -- (var.west) node[midway,above] {指向};
\end{tikzpicture}
```

### 5.3 外部图片规范

**图片引用模板**：
```latex
\begin{figure}[H]
  \centering
  \includegraphics[width=0.8\textwidth]{figures/图片文件名.png}
  \caption{图片说明}
  \label{fig:example_image}
\end{figure}
```

**注意事项**：
- 图片文件必须存放在 `figures/` 目录
- 支持格式：`.png`, `.jpg`, `.pdf`
- `width` 参数通常设为 `0.6\textwidth` 到 `0.9\textwidth`
- 必须使用 `[H]` 参数固定位置（需 float 宏包）
- `caption` 必须在图片下方
- `label` 格式：`fig:关键字`（使用小写字母和下划线）

## 6. 表格规范 (Tables)

### 6.1 三线表基本格式

**标准模板**：
```latex
\begin{table}[H]
  \centering
  \caption{表格标题说明}
  \label{tab:example}
  \begin{tabular}{lcc}
    \toprule
    \textbf{列标题1} & \textbf{列标题2} & \textbf{列标题3} \\
    \midrule
    内容1 & 内容2 & 内容3 \\
    内容4 & 内容5 & 内容6 \\
    \bottomrule
  \end{tabular}
\end{table}
```

### 6.2 列格式说明

**对齐方式**（在 `\begin{tabular}{...}` 中指定）：
- `l`：左对齐（Left）- 适用于文本内容
- `c`：居中对齐（Center）- 适用于数值或短文本
- `r`：右对齐（Right）- 适用于数字

**示例**：
```latex
% 第一列左对齐，后两列居中
\begin{tabular}{lcc}
  ...
\end{tabular}

% 三列都居中
\begin{tabular}{ccc}
  ...
\end{tabular}
```

### 6.3 复杂表格示例

**(1) 包含数值的对比表**：
```latex
\begin{table}[H]
  \centering
  \caption{不同数据类型的指针大小对比}
  \label{tab:ptr_size}
  \begin{tabular}{lcc}
    \toprule
    \textbf{数据类型} & \textbf{32位系统} & \textbf{64位系统} \\
    \midrule
    int*    & 4 字节 & 8 字节 \\
    char*   & 4 字节 & 8 字节 \\
    double* & 4 字节 & 8 字节 \\
    \bottomrule
  \end{tabular}
\end{table}
```

**(2) 包含代码片段的表格**：
```latex
\begin{table}[H]
  \centering
  \caption{指针操作符对比}
  \label{tab:ptr_operators}
  \begin{tabular}{lll}
    \toprule
    \textbf{操作符} & \textbf{示例} & \textbf{含义} \\
    \midrule
    \texttt{*}  & \texttt{*p}   & 解引用 \\
    \texttt{\&} & \texttt{\&var} & 取地址 \\
    \texttt{->} & \texttt{p->member} & 成员访问 \\
    \bottomrule
  \end{tabular}
\end{table}
```

### 6.4 注意事项

- **题注位置**：`\caption` 必须在 `\begin{tabular}` 之前（表格上方）
- **标签命名**：`\label{tab:关键字}`，使用小写字母和下划线
- **禁用元素**：严禁使用 `\hline`（应使用三线表的 `\toprule/\midrule/\bottomrule`）
- **表头加粗**：列标题建议使用 `\textbf{...}` 加粗
- **代码文本**：表格中的代码片段使用 `\texttt{...}` 等宽字体
- **固定位置**：使用 `[H]` 参数固定表格位置

## 7. 术语一致性与交叉引用
- **专业术语对照**：
    - 内存布局：堆 (Heap)、栈 (Stack)、常量区 (Data Segment)。
    - 指针操作：解引用 (Dereference)、野指针 (Wild Pointer)。
    - 遇到不确定的词汇，采用 `中文 (English)` 格式。
- **交叉引用 (Cross-Referencing)**：
    - 引用章节：`\ref{sec:...}`
    - 引用代码：`\ref{lst:...}`
    - 引用图片：`\ref{fig:...}`
    - **警告**：严禁捏造不存在的标签名，引用前请结合上下文确认标签是否存在。