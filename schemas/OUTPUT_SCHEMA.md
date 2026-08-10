# 输出规范（Output Schema）

## 1. 输出结构
```json
{
  "session_id": "string",
  "status": "accepted|needs_clarification|escalation|blocked",
  "summary": "string",
  "reflection": "string",
  "options": [
    {
      "id": "opt-1",
      "title": "string",
      "description": "string",
      "impact": "short",
      "relation_note": "string"
    }
  ],
  "next_step": {
    "immediate": "string",
    "communication_template": "string",
    "follow_up_time": "ISO8601 或 相对时间"
  },
  "risk_statement": "string",
  "boundary_notice": "string",
  "confidence": 0.0
}
```

## 2. 字段约束
- `status`
  - `accepted`: 正常生成建议。
  - `needs_clarification`: 需要更多信息后继续。
  - `escalation`: 需要第三方帮助（安全、医疗、法律高风险）。
  - `blocked`: 与边界规则冲突，拒绝或暂停执行。
- `summary`：120 字以内，先肯定情境，再指出用户主诉。
- `reflection`：复述并提炼 1–2 个核心感受和需求。
- `options`：至少 1 条；最多 3 条。
- `next_step.immediate`：可立即执行动作，不得超过两句话。
- `next_step.communication_template`：用于用户向关键关系对象沟通的草稿，可为空。
- `risk_statement`：仅在存在风险时填写完整；无风险可用“当前无高危风险信号”。
- `boundary_notice`：固定语句，声明“不替代关系/决策/生命主体”。
- `confidence`：0.0–1.0；不作为绝对真理承诺。

## 3. 语气与风格规则
- 采用陪伴式口吻，避免说教。
- 先反映再建议。
- 强制包含回流元素：今日是否可行动 + 复盘点。

## 4. 输出禁忌
- 不发布不确定且高风险诊断性判断。
- 不输出操控性措辞（如强制执行、绝对正确）。
- 不替代关系决策；所有建议必须可交由用户本人决定。
