# 写作风格与列表规则详细参考

## 一、段落 vs 列表 决策

### 情境 A：连贯逻辑 → 使用段落
```latex
\subsection{研究背景}
随着社会经济的快速发展，该领域的重要性
日益凸显。近年来，国内外学者对此进行了
大量研究，取得了丰硕的成果。这些研究成果
为后续的深入探索奠定了坚实的理论基础，
也为实践应用提供了重要参考。
```

### 情境 B：有序枚举 → enumerate
```latex
\subsection{研究方法的三个核心要素}
本研究在方法论上需要明确以下三个核心要素：
\begin{enumerate}[label={(\arabic*)}]
  \item 研究对象的界定与选取标准
  \item 数据采集的具体方式与流程
  \item 分析框架的构建与验证方法
\end{enumerate}

理解了这三个要素之后，我们就可以开始探讨...
（此处必须有过渡段落，而非紧接另一个列表）
```

### 情境 C：无序快速列举 → itemize
```latex
\subsubsection{常见的指针错误类型}
在使用指针时，初学者容易犯以下错误：
\begin{itemize}
  \item 野指针
  \item 内存泄漏
  \item 重复释放
  \item 越界访问
\end{itemize}
```

## 二、判断标准速查

| 场景 | 选择 |
|------|------|
| 因果关系、逻辑推导、叙事描述 | 段落 |
| 有序步骤、编号要点 | `enumerate[label={(\arabic*)}]` |
| 无序、简短、快速列举 | `itemize` |

## 三、列表间隔规则

❌ **错误**：连续列表
```latex
\begin{enumerate}[label={(\arabic*)}]
  \item 第一点
  \item 第二点
\end{enumerate}
下面是另一组要点：  % 仅一句引导语，不够！
\begin{enumerate}[label={(\arabic*)}]
  \item 另一点
\end{enumerate}
```

✅ **正确**：有完整过渡段落
```latex
\begin{enumerate}[label={(\arabic*)}]
  \item 第一点
  \item 第二点
\end{enumerate}

在理解了上述概念之后，我们需要进一步探讨其实际应用。
这些要点在实践中的表现形式各有不同，具体取决于使用场景
和数据结构的复杂程度。通过深入分析，我们可以发现...
（至少一个完整的过渡段落）

基于以上分析，我们可以总结出以下实践原则：
\begin{enumerate}[label={(\arabic*)}]
  \item 另一点
\end{enumerate}
```
