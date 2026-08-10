# 输入规范（Input Schema）

## 1. 输入容器
```json
{
  "session_id": "string",
  "timestamp": "ISO8601 字符串",
  "user_profile": "可选对象",
  "request": {
    "text": "string",
    "intent_hint": "可选字符串",
    "urgency": "low|medium|high|critical"
  },
  "context": {
    "language": "zh-CN",
    "previous_messages": [],
    "relationship_context": "可选对象",
    "risk_flags": []
  },
  "mode": "companion|reflection|decision-support|reconciliation|wellbeing"
}
```

## 2. 字段说明
- `session_id`：会话唯一标识，必填。
- `timestamp`：ISO8601 时间戳，必填。
- `request.text`：用户原始输入，必填，非空白。
- `request.intent_hint`：用户意图提示，帮助分流（如“情绪支持”“关系沟通”等）。
- `request.urgency`：默认为 `low`。
- `context.language`：默认 `zh-CN`。
- `context.previous_messages`：可选历史上下文，需保留匿名化敏感处理。
- `context.relationship_context`：可选，用于关系映射与建议路径。
- `context.risk_flags`：安全提示项列表，如 `self-harm`, `violence`, `medical-urgent` 等。
- `mode`：用于触发行为模板选择。

## 3. 校验规则
1. `request.text` 长度 > 0。
2. `timestamp` 可解析为合法时间。
3. `urgency` 与 `mode` 必须为枚举值之一。
4. 风险字段仅允许预定义白名单内值。
5. `session_id` 与 `timestamp` 缺失则拒绝执行，返回缺口提示。

## 4. 处理前匿名与隐私最小化
- 不收集不必要身份证明字段。
- 历史上下文不可包含完整敏感身份信息。
- 输出不应反向推断用户未提供的关系细节。
