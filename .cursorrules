# LaTeX 项目协作准则

当你作为 AI 助手参与此项目时，请严格遵守以下指令：

## 1. 编译与保存规则 (核心要求)
- **禁止在终端执行任何编译命令**（如 pdflatex, xelatex, latexmk 等）。
- 理由：本项目已在 VS Code 的 LaTeX Workshop 插件中配置了完善的 `settings.json` 规则，负责处理 `out/` 文件夹重定向、中间文件自动清理及 SyncTeX 定位。
- 你的任务：仅负责编写、改写或增删高质量的 LaTeX 代码并**保存文件**。编译工作将由用户的 `Ctrl+S` 自动触发。

## 2. 项目目录结构规范
- **根目录**：仅存放 `main.tex`、配置文件及管理文件。
- **章节内容**：必须按照 `latex/chapter[n]/[n].tex` 的路径进行存放和引用（例如第一章位于 `latex/chapter1/1.tex`）。
- **资源文件**：图片存放在 `figures/`，配置文件位于 `latex/config.tex`。
- 在创作新章节或链接文件时，请务必遵循并维持这一层级结构。

## 3. 列表格式约束
- 在任何标题（\section, \subsection 等）后的分点叙述，必须使用 `enumerate` 环境。且必须包含参数 `[label={(\arabic*)}]` 以实现“(1) (2) (3)”的编号效果。
- **禁止**使用 `itemize` 或默认不带参数的 `enumerate`。

即使用如下类似的代码；
 \begin{enumerate}[label={(\arabic*)}]
   \item 第一项
   \item 第二项    
   \item 第三项
 \end{enumerate}



## 4. 文本格式约束
- 禁止在 `\item` 开头自动添加 `\textbf{...}` 进行加粗，除非用户明确要求。
- 保持技术文档的简洁、专业风格。