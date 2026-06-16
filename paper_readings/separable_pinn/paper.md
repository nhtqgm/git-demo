# Separable Physics-Informed Neural Networks 中文研读稿

## 抽取状态
- 状态：verified（机器文本抽取可读；公式与图内文字存在排版噪声，详见 `translation_notes.md`）。
- PDF：`01 - Separable Physics-Informed Neural Networks.pdf`
- 全文抽取：`full_text_extract.md`
- 来源映射：`source_map.json`

## p.1 S001 摘要与问题定位
论文研究对象是 Physics-Informed Neural Networks（PINNs）作为数据驱动 PDE 求解器在多维 PDE 与复杂解函数上的训练瓶颈。作者指出，传统 PINN 需要大量 collocation points，但每个点的 PDE residual 计算涉及多次前向/反向传播，导致计算与显存成本严重限制可用点数。作者提出 Separable PINN（SPINN），按坐标轴分别处理输入，并结合 forward-mode automatic differentiation，使单张消费级 GPU 上可使用超过 `10^7` collocation points。原文依据：p.1 S001。

## p.2 S001 引言与核心动机
作者进一步说明：传统 PINN 的坐标 MLP 对每个多维坐标点逐点输入，collocation points 数量随维度和解复杂度显著增长；已有研究显示更大 batch / 更多 collocation points 有利于精度和收敛。SPINN 通过多个一维子网络处理各坐标轴，再聚合成解，从而把网络传播复杂度从约 `O(N^d)` 降低到 `O(Nd)`。原文依据：p.2 S001。

## p.3 S001 相关工作定位
作者把本文放在三条文献线索中：PINN 改进、collocation points 数量影响、科学机器学习中的导数计算。SPINN 与 domain-decomposition 式多 MLP PINN 不同：后者分解输入域，SPINN 分解输入维度，并由所有分离 MLP 协同表示整个域上的解。原文依据：p.3 S001。

## p.4 S001 Forward / Reverse-mode AD 预备知识
论文解释了 forward-mode AD 与 reverse-mode AD 的计算差异：forward-mode 一次 JVP 生成雅可比的一列，适合输出维度大于输入维度的“高”雅可比；reverse-mode 一次 VJP 生成雅可比的一行，适合输入维度大于输出维度的“宽”雅可比。SPINN 的子网络是 `R -> R^r`，因此 forward-mode AD 更自然。原文依据：p.4 S001。

## p.5 S001 SPINN 网络结构
SPINN 对 `d` 维 PDE 使用 `d` 个 body networks，每个网络只接收一个一维坐标分量并输出 `r` 维特征。最终预测解为：

\[
\hat{u}(x_1, x_2, ..., x_d)=\sum_{j=1}^{r}\prod_{i=1}^{d} f_j^{(\theta_i)}(x_i)
\]

其中 `r` 是低秩表示的 rank / feature size，`f_j^(theta_i)` 是第 `i` 个坐标轴子网络输出的第 `j` 个分量。该结构可解释为低秩张量分解形式的解函数表示。原文依据：p.5 S001。

## p.6 S001 Factoriable coordinates 与表达能力风险
SPINN 的 collocation points 是 factorizable coordinates：每个坐标轴独立采样一维点，再形成格点状多维组合。这与传统 PINN 可直接采样非结构化多维点不同。该设计带来计算优势，但也意味着对规则域和格点结构更友好。原文依据：p.6 S001。

## p.7 S001-S002 理论与整体实验概览
论文给出近似能力讨论，并在 Fig. 6 汇总 diffusion、Helmholtz、Klein-Gordon 等实验。作者声称 SPINN 在 runtime 与 GPU memory 上显著优于 baseline PINN，且 modified MLP 版本通常取得最高精度。原文依据：p.7 S001；p.7 S002。

## p.8 S001 主实验结论
作者报告 SPINN 在三维和四维 forward problems 上 wall-clock runtime 显著更低；当 collocation points 指数增长时，SPINN 的 memory usage 与 runtime 近似线性增长。作者还比较了同等 collocation points 下的 FLOPs，称在 3D PDE 中 SPINN 的 FLOPs 可低约 `1394×`。原文依据：p.8 S001。

## p.9 S001 Navier-Stokes 结果
Table 2 比较了 `(2+1)` 维 Navier-Stokes 上 PINN+modified MLP、causal PINN 与 SPINN。作者报告 SPINN 在单 GPU 上约 9 分钟完成，而 causal PINN 约 10 小时；相对 `L2` 误差保持在同一量级。原文依据：p.9 S001。

## p.10 S001 结论与作者自述局限
作者总结 SPINN 是一种利用 separated MLPs 与 forward-mode AD 使用大规模 collocation points 的方法，显著降低空间和计算复杂度。作者也指出对更广函数空间的近似理论、非均匀采样、非矩形域处理仍是未来方向。原文依据：p.10 S001。

## p.17-p.24 附录实验设置与完整表格
附录给出 diffusion、Helmholtz、Klein-Gordon、Navier-Stokes 的 PDE 形式、domain、初始/边界条件、网络层数、hidden/output feature size、optimizer、learning rate、训练步数、loss weights、collocation points 与完整数值结果。原文依据：p.17 S001；p.18 S001；p.19 S001；p.20 S001；p.22 S001；p.23 S001；p.24 S001。
