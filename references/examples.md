# 呈现示例（非规则）

**本文件不是规则，也不是结构处置清单。** 它只展示「尽可能可读、可渲染、不丢原意」在某个支持 Markdown 与 KaTeX 的宿主里可能长成什么样。你的渲染层不同，结果完全可以不同；请以 `SKILL.md` 的目标与边界为准，不要照抄这里的写法。

下面用引用块只是为了在本文档里把示例与说明区分开，**不代表译文应当被引用块包裹**。素材均为自造文本，不含真实论文内容。各示例只展示片段；完整译文末尾还应有一条横线与一句极简的修正说明，见 `SKILL.md` 的「收尾说明」。

## 示例一：公式

输入：

```latex
The objective is \( \alpha\|u\|^2 \) and we minimize
\begin{equation}
\min_{\vx} \frac{1}{2m}\sum_{i=1}^{m}(\va_i^\top\vx - y_i)^2 + \lambda\|\vx\|_1
\end{equation}
```

一种呈现：

> 目标函数为 $\alpha\|u\|^2$，本文最小化
>
> $$
> \min_{\vx} \frac{1}{2m}\sum_{i=1}^{m}(\va_i^\top\vx - y_i)^2 + \lambda\|\vx\|_1
> $$

两处公式各自单独包裹；编号、标签一类不进公式块；正文没有套任何容器，也没有残留反斜杠命令。

## 示例二：伪代码

输入：

```latex
\begin{algorithmic}[1]
\REQUIRE $\mA$, $\vy$, $K$
\FOR{$k=1$ \TO $K$}
  \STATE $\vg_k \leftarrow \nabla f(\vx_k)$
\ENDFOR
\RETURN $\vx_K$
\end{algorithmic}
```

一种呈现：

> 算法步骤：输入 $A$、$\mathbf{y}$、$K$。
>
> 1. 对 $k=1$ 到 $K$，计算 $\mathbf{g}_k \leftarrow \nabla f(\mathbf{x}_k)$。
>
> 最后返回 $\mathbf{x}_K$。

原本读不出来的结构被改写成可读的中文编号步骤，文字译中、数学含义不变，没有用围栏代码块把整块框住，也没有丢步骤。

## 示例三：图片模块

输入：

```latex
\begin{figure}[t]
\centering
\includegraphics[width=0.85\linewidth]{figs/convergence.pdf}
\caption{Convergence over 20 runs.}
\label{fig:conv}
\end{figure}
```

一种呈现：

> 图 convergence.pdf：20 次运行的收敛曲线（标签 fig:conv）。

既不能渲染又不承载译文语义的排版参数被删掉，文件名、图题、标签这些承载原意的信息以可读文字留下。

## 示例四：渲染层不认识的自定义宏

输入（导言区定义不会随片段一起贴进对话）：

```latex
\newcommand{\Rset}{\mathbb{R}}
Let $\vy = \mA\vx^{\star} + \boldsymbol{\varepsilon}$, with $\mA \in \Rset^{m \times n}$.
```

一种呈现：

> 设 $\mathbf{y} = A\mathbf{x}^{\star} + \boldsymbol{\varepsilon}$，其中 $A \in \mathbb{R}^{m \times n}$。

`\vy`、`\mA`、`\vx`、`\Rset` 在对话里没有定义，直接写进公式或正文会被渲染层标红。AI 自行展开成等价写法，数学含义不变；正文里也没有留下宏定义或裸命令。若宿主连展开后仍无法渲染，也可以把整条公式降级为可读文字，而不是把解析不了的字节交给渲染层。

---

四例只是同一目标在不同内容上的结果。**Skill 不规定「遇到某结构就这么做」**：如果宿主有更好的可视化能力，AI 完全可以给出另一种呈现；判断权在调用方 AI，不在这份示例里。
