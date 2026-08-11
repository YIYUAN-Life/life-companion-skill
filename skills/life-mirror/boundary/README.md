# Boundary 镜像目录（V1）

## 当前边界文件

- [PUBLIC_BOUNDARY_AND_SAFETY_V1.md](/Users/zima/Documents/一元启明/YIYUAN_LIFE_MIRROR_GITHUB_REPOSITORY_FINAL_PREPARATION_V1/PUBLIC_BOUNDARY_AND_SAFETY_V1.md)：公开边界与安全声明。
- [SKILL_MANIFEST.json.boundaries](/Users/zima/Documents/一元启明/YIYUAN_LIFE_COMPANION_SKILL_PUBLIC_RELEASE_PREPARATION_V1/life-companion-skill/skills/life-mirror/SKILL_MANIFEST.json)：可机器读取的边界字段。

## 与 Life Companion Protocol 边界一致性

- 非替代原则（不替代生命、关系、决策）与 `LIFE_MIRROR_MODULE_BOUNDARY_V1.md` 保持一致。
- 高风险触发场景优先走 `escalation/blocked` 路径。
- 仅会话内处理，不承载长期画像或 runtime 调度行为。
