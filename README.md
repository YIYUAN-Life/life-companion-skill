# Life Companion Skill Public Package（V1）

这是一个可公开发布的 Skill 包候选，面向低模型的 Life Companion 行为规范化实现。

核心目标：
- 保持行为一致性、边界明确性与可追溯性。
- 支持陪伴、反思与关系沟通引导。
- 严格避免替代决策、关系与生命主体。

发布说明：
- 该包是 **AI行为规范 Skill**。
- 不是 AI 产品。
- 不是 AI 伴侣。
- 不是自治 Agent。

入口文件说明：
- `SKILL.md`：主能力定义与行为流程。
- `SKILL_METADATA_V1.md`：元数据与版本信息。
- `schemas/INPUT_SCHEMA.md`：输入契约。
- `schemas/OUTPUT_SCHEMA.md`：输出契约。
- `docs/BOUNDARY_RULES.md`：边界与禁止行为。
- `ERROR_MODEL_V1.md`：缺失、边界与异常行为响应模型。
- `examples/EXAMPLES.md`：合规示例与反例。

## 模块化索引（执行扩展）

- 已纳入能力：`skills/life-mirror`
  - `SKILL.md`
  - `SKILL_MANIFEST.json`
  - `schemas/INPUT_SCHEMA.json`
  - `schemas/OUTPUT_SCHEMA.json`
  - `examples/`
  - `boundary/README.md`

新增模块说明：
- `life-mirror` 为 `low_model` 输入下的生命映照入口。
- 保留现有仓库边界，不引入额外 runtime 与 protocol 依赖。

本仓库不包含运行代码，也不包含 MCP 设计、原型、治理实现。仅发布规范化文档资产。
