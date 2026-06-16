# Separable Physics-Informed Neural Networks 抽取/OCR/图表不确定性说明

## 1. 技能库状态
- 用户指定的本地技能组合：Nature Reader + PDF + Source Material Ingestion + Paper Parse。
- 本地 `/opt/codex/skills` 中未发现这些技能；已改用本地 `pypdf` 进行全文抽取。
- 额外按用户要求尝试检索 GitHub 上相关技能名称，但未获得可直接安装/调用的本地技能结果；因此本篇交付不声称使用了这些技能。

## 2. 抽取工具与质量
- 工具：`pypdf`。
- PDF 页数：28。
- `pdfinfo` / `pdftotext` 不在环境中，因此未使用 Poppler 系工具。
- 文本总体可读，标题、摘要、正文、实验设置、表格内容可抽取。

## 3. needs verification 项
- 公式中的上下标、希腊字母、矩阵排版存在 PDF 文本抽取噪声；已尽量按论文上下文恢复，但严谨复现公式应核对 PDF 原版。
- 图内文字和多列表格被 `pypdf` 合并为连续文本，图表精确单元格位置需要人工核对 PDF。
- 代码链接来自论文摘要页原文，代码仓库当前可访问性与版本状态未外部验证，标记为 needs verification。
- DOI/arXiv 标识未在 PDF 抽取文本中明确出现，标记为 not found / needs verification。

## 4. 信息分类规则
- verified：可在 `source_map.json` 的页码/段落锚点中找到直接原文支持。
- inferred：由 verified 信息进行的合理推断，例如“更适合规则域”。
- needs verification：需要查看 PDF 图像、补充材料、代码仓库或外部来源才能确认的信息。
