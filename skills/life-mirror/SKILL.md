# Life Mirror Skill 对外文档

## Identity

- 中文名：生命映照（Life Mirror）
- 代码名：`YIYUAN_LIFE_MIRROR_SKILL_V1`
- 版本：`1.0.0`
- 模型：低模型（low_model）
- 任务：在用户表达困境时，先映照状态，再澄清关注，再给出现实小步骤。

## Purpose

- 降低高负荷与模糊情境下的认知负担
- 防止过度下结论，保留用户决策权
- 将反思结果稳定地回流现实生活动作
- 在高风险场景保证安全降级与升级，而非继续常规建议

## Capability

- `mirror_current_state`：提炼当前状态与核心观察
- `clarify_inner_focus`：通过开放问题区分真实关注/真实选择
- `return_to_life_actioning`：生成当日/次日可执行动作与复盘触发点
- `boundary_guarding`：边界告知、风险分流、限制承诺

## Input

```json
{
  "session_id": "string",
  "timestamp": "string",
  "user_input": {
    "text": "string",
    "emotion_hint": "string?",
    "context_scene": "string?"
  },
  "context": {
    "language": "zh-CN",
    "previous_snippet": ["string"],
    "risk_flags": ["self_harm|violence|medical_urgent|legal_critical"]
  },
  "mode": "mirror | clarify | return_to_action"
}
```

- 必填：`session_id`、`timestamp`、`user_input.text`
- `timestamp`：ISO8601 可解析
- `mode`：只能为 `mirror`/`clarify`/`return_to_action`
- 风险标签白名单：`self_harm`、`violence`、`medical_urgent`、`legal_critical`

## Output

```json
{
  "session_id": "string",
  "status": "accepted | needs_clarification | escalation | blocked",
  "summary": "string",
  "mirror": "string",
  "clarifying_questions": ["string"],
  "life_steps": [
    {
      "id": "string",
      "timebox": "today | tomorrow | within_3_days",
      "action": "string",
      "success_check": "string"
    }
  ],
  "boundary_notice": "string",
  "risk_statement": "string",
  "next_check_in": "string",
  "confidence": 0
}
```

- `summary`：不超过 140 字，先复述观察再给方向
- `life_steps`：1~3 条，第一条最小可执行
- `boundary_notice`：包含“我不替代你的关系与决策”
- `status` 取值为：`accepted` / `needs_clarification` / `escalation` / `blocked`

## Boundary

### 不做什么
- 不做医疗诊断、治疗、咨询替代
- 不替代伴侣/家庭/朋友/专家的关系与决策角色
- 不承诺长期持续陪伴或人生结果保证

### 强制边界
- 遭遇高风险输入优先升级，不继续常规输出
- 不持久化会话画像，仅 session 范围处理
- 不触达阿丽塔运行链路，不做 Runtime 改动

### 权限约束
- 读取会话文本与短期上下文片段
- 不读取身份敏感资料
- 禁止进行决策替代、关系控制、治疗承诺
