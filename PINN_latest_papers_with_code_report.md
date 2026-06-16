# PINN 方向最新论文与开源代码验证报告（截至 2026-06-16）

## 检索与验证方法

- 检索范围：GitHub、OpenReview、arXiv、会议/项目主页、Papers with Code 相关索引。
- 时间优先级：优先纳入 2025--2026 年论文；为凑足 10 篇“有可验证源码”的高相关 PINN 工作，补充少量 2024 年代表性论文。
- 代码真实性验证：对每个仓库执行 GitHub API 元数据与递归文件树检查，确认仓库可访问、存在实际源码/Notebook/配置文件，而非空仓库或仅 README；同时交叉核对论文页或仓库 README 中的论文题名/会议/引用信息。
- 注意：本报告验证的是“源码仓库真实存在且包含可运行代码结构”，没有完整复现实验结果；部分项目可能需要 GPU、大数据或特定依赖。

## 结论摘要

本次筛选得到 10 篇与 PINN / physics-informed neural networks 高相关、且具有公开源码的最新论文。代码真实性验证均通过，其中 2025 年论文 7 篇，2026 年论文/预印本 1 篇，2024 年论文 2 篇。最推荐优先阅读/复现的前三项是：

1. **Gradient Alignment in Physics-informed Neural Networks**：NeurIPS 2025，聚焦 PINN 训练中的梯度冲突与二阶优化视角；代码在 `PredictiveIntelligenceLab/jaxpi`。
2. **HyPINO**：NeurIPS 2025 Spotlight，将超网络生成 PINN 权重，用于多物理 PDE 的 zero-shot 泛化；代码和模型权重公开。
3. **FP64 is All You Need**：NeurIPS 2025，重新解释 PINN failure modes，强调 FP64/L-BFGS 数值精度问题；代码仓库包含多个 PDE 脚本与模型实现。

## 10 篇论文清单与源码验证

| # | 年份 | 论文/项目 | 方向关键词 | 论文来源 | 源码仓库 | 源码真实性验证 |
|---|---:|---|---|---|---|---|
| 1 | 2026 | Physics-Informed Neural Networks: A Didactic Derivation of the Complete Training Cycle | PINN 训练流程、教学推导 | arXiv:2604.18481；论文引用 Zenodo 与 GitHub 补充代码 | https://github.com/Tahimi/PINN-Didactic-Training-Cycle | ✅ GitHub API 可访问；默认分支 `main`；15 个文件；含 `PINN_Didactic_Notebook.ipynb` 与 `README.txt`；MIT License；最近推送 2026-04-21。 |
| 2 | 2025 | Gradient Alignment in Physics-informed Neural Networks: A Second-Order Optimization Perspective | 梯度冲突、二阶优化、PINN 训练 | OpenReview NeurIPS 2025 poster；项目仓库 README 标注 2025-02 发布相关代码 | https://github.com/PredictiveIntelligenceLab/jaxpi | ✅ GitHub API 可访问；433 stars；默认分支 `main`；216 个文件，约 161 个代码/配置/Notebook 文件；含多组 PDE 示例配置；最近推送 2025-11-14。 |
| 3 | 2025 | FP64 is All You Need: Rethinking Failure Modes in Physics-Informed Neural Networks | PINN failure modes、数值精度、FP64 | OpenReview NeurIPS 2025 poster；仓库 README 标注论文被 NeurIPS 接收 | https://github.com/miniHuiHui/PINN_FP64 | ✅ GitHub API 可访问；27 stars；32 个文件，18 个代码相关文件；含 `convection_fp64.py`、`reaction_fp64.py`、`wave_fp64.py`、`ac_fp64.py` 与 `models/PINN.py`；最近推送 2025-09-18。 |
| 4 | 2025 | Dual-Balancing for Physics-Informed Neural Networks | loss balancing、PINN 优化 | IJCAI 2025；仓库 README 标注 official code | https://github.com/chenhong-zhou/DualBalanced-PINNs | ✅ GitHub API 可访问；16 个文件，10 个 Python 脚本；覆盖 Klein-Gordon、Wave、Helmholtz、Allen-Cahn、Burgers、Navier-Stokes；最近推送 2025-05-12。 |
| 5 | 2025 | Deep Fuzzy Physics-Informed Neural Networks for Forward and Inverse PDE Problems | fuzzy PINN、正/反问题 PDE | Neural Networks 2025；仓库 README 给出正式引用 | https://github.com/siyuancncd/FPINNs | ✅ GitHub API 可访问；10 个文件，4 个代码/数据说明文件；含 `Allen-Cahn_FPINNs_Forward.py`、`Allen-Cahn_FPINNs_Inverse.py`、`FuzzyLayers.py`；最近推送 2025-10-14。 |
| 6 | 2025 | Sub-Sequential Physics-Informed Learning with State Space Model | PINN + State Space Model / Mamba | OpenReview；页面给出 `Link To Code: https://github.com/miniHuiHui/PINNMamba` | https://github.com/miniHuiHui/PINNMamba | ✅ GitHub API 可访问；MIT License；27 个文件，22 个代码相关文件；含 `convection_pinnmamba.py`、`models/PINNMamba.py`、`models/PINN.py`；最近推送 2025-05-05。 |
| 7 | 2025 | PIED: Physics-Informed Experimental Design for Inverse Problems | physics-informed inverse problem、实验设计 | ICLR 2025；仓库 README 标注论文已被 ICLR 2025 接收并链接 OpenReview | https://github.com/apivich-h/pied | ✅ GitHub API 可访问；191 个文件，155 个代码/配置/数据说明文件；含 `pied/` 包与 DeepXDE 相关实现；最近推送 2026-03-01。 |
| 8 | 2025 | HyPINO: Multi-Physics Neural Operators via HyperPINNs and the Method of Manufactured Solutions | HyperPINN、neural operator、zero-shot PDE | NeurIPS 2025 Spotlight；OpenReview 明确说明代码和模型权重公开 | https://github.com/rbischof/hypino | ✅ GitHub API 可访问；MIT License；103 个文件；含 `src/`、`evaluate.py`、4 个 notebooks；仓库说明为 official implementation；最近推送 2025-10-19。 |
| 9 | 2024 | RoPINN: Region Optimized Physics-Informed Neural Networks | region optimization、采样/优化 | NeurIPS 2024；THUML 仓库说明为 Code release | https://github.com/thuml/RoPINN | ✅ GitHub API 可访问；MIT License；32 个文件，26 个代码相关文件；含 point/region optimization 脚本与 `models/PINN.py`；最近推送 2025-07-14。 |
| 10 | 2024 | Dual Cone Gradient Descent for Training Physics-Informed Neural Networks | multi-objective optimization、梯度更新 | NeurIPS 2024；仓库 README 标注 official code repository | https://github.com/youngsikhwang/Dual-Cone-Gradient-Descent | ✅ GitHub API 可访问；MIT License；56 个文件，16 个代码/Notebook 文件；含 Burgers/Helmholtz/Klein-Gordon samplers、DCGD optimizer 与变体实现；最近推送 2025-12-06。 |

## 逐篇简评与复现建议

### 1. Physics-Informed Neural Networks: A Didactic Derivation of the Complete Training Cycle

- **价值**：虽然更偏教学和完整训练周期推导，但发布时间最新（2026），适合作为 PINN 训练机制、自动微分、残差构造、边界条件处理的入门复现材料。
- **代码可信度**：论文/预印本直接引用补充代码与 GitHub 仓库；仓库含 Notebook，可直接检查训练流程。
- **复现建议**：适合 CPU/单机运行；先运行 Notebook 中的最小示例，再对照论文公式检查损失项实现。

### 2. Gradient Alignment in Physics-informed Neural Networks

- **价值**：聚焦 PINN 多目标损失项之间的方向性梯度冲突，是 2025 年 PINN 优化方向的重要工作。
- **代码可信度**：`jaxpi` 是 Predictive Intelligence Lab 维护的活跃仓库；仓库更新说明中明确提到 2025 年发布该论文代码。
- **复现建议**：优先检查对应分支/目录；该项目基于 JAX，需关注 CUDA/JAX 版本和默认精度设置。

### 3. FP64 is All You Need

- **价值**：对 PINN failure modes 给出不同解释：失败可能来自 FP32 与 L-BFGS 停止准则/数值精度，而非传统解释中的损失屏障。
- **代码可信度**：仓库 README 标注 NeurIPS 接收，并提供多个 PDE 的直接运行脚本。
- **复现建议**：强烈建议用 GPU 且开启 FP64；若只能用 CPU，先运行小规模配置验证脚本路径和依赖。

### 4. Dual-Balancing for Physics-Informed Neural Networks

- **价值**：面向 PINN 多损失项平衡问题，覆盖多个经典 PDE，是比较 loss balancing 策略的良好基线。
- **代码可信度**：仓库 README 明确写明 IJCAI 2025 official code，并列出六类 PDE 复现实验。
- **复现建议**：从 `Klein-Gordon/Klein-Gordon.py` 这类单文件脚本开始；注意 Python 3.7 依赖约束。

### 5. Deep Fuzzy Physics-Informed Neural Networks

- **价值**：将 fuzzy neural layers 引入 PINN，用于正问题与反问题，适合关注不确定性、模糊建模或可解释结构的读者。
- **代码可信度**：仓库提供论文正式引用与 Allen-Cahn forward/inverse 示例脚本。
- **复现建议**：代码规模较小，适合快速读源码；建议优先复现 Allen-Cahn forward，再尝试 inverse。

### 6. Sub-Sequential Physics-Informed Learning with State Space Model

- **价值**：把状态空间模型/Mamba 思路引入 physics-informed learning，适合关注长时间序列 PDE 或时序建模的 PINN 研究者。
- **代码可信度**：OpenReview 页面直接给出 GitHub 链接；仓库含 PINN 与 PINNMamba 模型实现。
- **复现建议**：从 convection baseline 与 pinnmamba 两个脚本对比入手；重点检查模型结构与残差损失的耦合方式。

### 7. PIED: Physics-Informed Experimental Design for Inverse Problems

- **价值**：严格说更偏 physics-informed inverse problems / experimental design，不是传统“只训练 PINN 解 PDE”的论文，但与 PINN 生态和 DeepXDE 强相关。
- **代码可信度**：仓库 README 明确标注 ICLR 2025 接收；代码规模完整，含包结构、数据集与 DeepXDE 相关实现。
- **复现建议**：先运行仓库测试/最小示例；由于文件多、任务多，应优先选择一个 inverse problem 数据集验证。

### 8. HyPINO

- **价值**：用超网络生成目标 PINN 参数，把 PINN 与 neural operator 结合，是 2025 年 PINN 方向更前沿的泛化路线之一。
- **代码可信度**：OpenReview 明确说明代码和模型权重公开；项目主页和仓库均声称 official implementation。
- **复现建议**：建议先运行 inference notebook，再尝试 iterative refinement；完整训练可能依赖较大数据和 GPU。

### 9. RoPINN

- **价值**：通过 region optimization 改善 PINN 训练/采样，是 2024 NeurIPS 的代表性工作，仍然是 2025--2026 研究中的重要比较对象。
- **代码可信度**：THUML 组织仓库，README/组织页说明为 NeurIPS 2024 代码发布；包含多个优化脚本。
- **复现建议**：同一 PDE 下分别运行 point optimization 与 region optimization 脚本，观察误差和采样区域差异。

### 10. Dual Cone Gradient Descent

- **价值**：面向 PINN 多目标优化中的梯度冲突/更新方向问题，与 2025 的 gradient alignment 论文有直接关联价值。
- **代码可信度**：仓库 README 标注 NeurIPS 2024 official code；包含 DCGD 优化器、采样器和多个 PINN 变体。
- **复现建议**：先从 Helmholtz 或 Burgers 示例开始；如需与普通 Adam/L-BFGS 对比，固定随机种子和采样点。

## 推荐阅读顺序

1. 入门与公式：2026 didactic PINN training cycle。
2. 训练失败与优化：FP64 is All You Need → Dual Cone Gradient Descent → Gradient Alignment。
3. 损失平衡与采样：Dual-Balancing → RoPINN。
4. 架构扩展：FPINNs → PINNMamba → HyPINO。
5. 应用到反问题设计：PIED。

## 源码真实性验证记录

验证命令使用 GitHub API 获取每个仓库的元数据、默认分支、许可证、最近推送时间、递归文件树，并统计实际源码/Notebook/配置文件数量。所有 10 个候选仓库均满足：

- 仓库 URL 可访问；
- 默认分支存在；
- 文件树可读取；
- 至少包含 Python / Notebook / 配置 / 数据说明等实际项目文件；
- 论文页、项目页或 README 能与论文题名/会议/年份对应。

## 局限性

- 没有逐个安装依赖或完整训练复现实验结果；完整复现可能需要 GPU、CUDA、JAX/PyTorch 版本匹配、大数据或模型权重。
- “最新”按截至 2026-06-16 的公开搜索结果与可验证代码判断；后续可能出现更新论文或新仓库。
- 部分仓库星标数较少，不代表代码无效；PINN 细分研究仓库常见星标较低。
