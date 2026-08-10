# YIYUAN Life Companion Protocol Skill Error Model V1

## 1. 输入不足（Input Deficiency）

当以下情况发生时，进入 `needs_clarification`：

- `session_id` 缺失或为空。
- `timestamp` 缺失、格式不可解析。
- `request.text` 空白、长度为 0、或仅包含噪音符号。
- `mode`、`urgency`、`status` 取值不在约定枚举范围内。
- 风险字段不在白名单集合内。

对应动作：
- 明确列出缺失项；
- 请求最小补充字段；
- 保持边界语气，不输出建议或判断。

## 2. 边界触发（Boundary Trigger）

当满足以下任一条件时，进入 `blocked` 或 `escalation`：

- 危机信号：自伤/他伤倾向、明显失控风险。
- 医疗、法律、财务高风险决策类问题，超过支持性范围。
- 明确请求要求 AI 替代关系角色、做诊断/治疗决策或替代用户选择权。
- 与未成年人、受害者隐私相关的过度敏感提问。
- 用户拒绝边界提醒仍坚持越界请求。

触发动作：
- `blocked`：给出替代路径（沟通模板、线下支持、专业援助入口），拒绝越界执行。
- `escalation`：给出安全提示与外部求助建议（必要时鼓励立即离开高风险环境）。

## 3. 异常情况（Runtime Exception）

- 输入解析失败（无法反序列化）。
- 字段类型冲突（例如 `urgency` 非字符串、`timestamp` 格式不可解码）。
- 依赖服务不可达/超时（仅在未来运行时出现）。
- 输出构建失败（字段缺失、JSON 结构异常）。

统一兜底动作：
- 返回 `blocked` 或 `needs_clarification`；
- 包含最小可执行说明与下一步提示；
- 输出尾部固定边界提醒（不替代生命/关系/决策）。

