# latex-academic-translate

把含 LaTeX 的英文论文片段译成中文，公式照样能渲染。

latex-academic-translate 是一个纯提示词 Skill：翻译结果直接留在对话里，无脚本、无依赖，运行时只读一个 `SKILL.md`。

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

## 特性

- **公式照常渲染**。行内、行间公式单独包裹成 `$...$` / `$$...$$`，不进代码块。
- **正文干净**。`\cite`、`\label` 之类的命令转成可读文字，译文正文不出现反斜杠命令。
- **数学含义不变**。公式源码默认不动；渲染层解析不了的自定义宏，展开、等价替换或降级为文字，以可读优先。
- **不丢原意**。公式、编号、引用键、图表标题、数值单位全部保留。不加译注、评价、对照。
- **零依赖**。不联网、不写文件、不需要安装任何包。

## 效果

输入（自造示例）：

```latex
中译：
\subsection{Setup}
We evaluate on three benchmarks with $\lambda > 0$ and $\|\vx\|_1$.
\begin{algorithmic}[1]
\FOR{$k=1$ \TO $K$}
  \STATE $\vx_{k+1} \leftarrow \vx_k - \eta \nabla f(\vx_k)$
\ENDFOR
\end{algorithmic}
\begin{figure}[t]
\centering
\includegraphics[width=0.85\linewidth]{figs/convergence.pdf}
\caption{Convergence over 20 runs.}
\end{figure}
```

输出（取决于宿主渲染能力，这是其中一种呈现）：

> ### 实验设置
>
> 我们在三个基准上评估，其中 $\lambda > 0$ 且使用 $\|\vx\|_1$。
>
> 算法步骤：
>
> 1. 对 $k=1$ 到 $K$，令 $\vx_{k+1} \leftarrow \vx_k - \eta \nabla f(\vx_k)$。
>
> 图 convergence.pdf：20 次运行的收敛曲线。
>
> ---
>
> 已把公式单独包裹、伪代码改写成可读步骤、图片模块压缩为文字说明，并删去无渲染意义的排版字节。

伪代码被改写成编号步骤，图片模块压成一句说明，末尾横线后是一句话收尾说明。更多呈现示例见 [`references/examples.md`](references/examples.md)。

## 安装

复制到技能目录，重载会话后生效：

```text
~/.workbuddy/skills/latex-academic-translate/
├── SKILL.md          # 唯一必需
├── README.md
└── references/       # 可选，仅示例
```

触发依赖宿主读取 `SKILL.md` 的 YAML frontmatter（WorkBuddy、Claude Code 等 Skill 机制）。

## 用法

带标签最稳，标签本身不会出现在译文里：

```text
中译：
<粘贴英文 LaTeX 片段>
```

可用标签：`中译`、`译中`、`/zh`、`ZH`。不加标签也行，含 LaTeX 特征的文本默认按中译处理。

完整规则见 [`SKILL.md`](SKILL.md)。

## 边界

- 只做英译中。
- 不生成 `.tex`、`.docx` 或 PDF，结果只在对话里返回。
- 公式最终能不能显示为可视化内容由调用方前端决定，本 Skill 只管译文怎么组织、怎么包裹。
- 不解析参考文献库，不做宏包依赖推断。
- 不做纯文本翻译、英文润色、LaTeX 命令讲解。

## 文件

| 文件 | 说明 |
|---|---|
| `SKILL.md` | 技能定义，运行时唯一必需 |
| `references/examples.md` | 呈现示例，非规则 |
| `CHANGELOG.md` / `CONTRIBUTING.md` / `LICENSE` / `VERSION` | 治理文件 |

## 贡献

改动规则前先读 [`CONTRIBUTING.md`](CONTRIBUTING.md)。提交 issue 请勿粘贴真实未发表论文内容。

## 许可证

[MIT](LICENSE)
