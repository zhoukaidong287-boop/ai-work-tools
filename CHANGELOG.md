# CHANGELOG

本文档初始化记录当前 `ai-work-tools` 已完成的重要功能和后续维护规则。

## 已完成核心模块

- 首页工具入口。
- CRM 客户台账。
- 销售客户池复盘。
- 抖音线索池。
- AI 每日点将研判台。
- 日报/周报工具。
- 信息流素材矩阵。
- 信息流 AI 调令模式。
- 投流测试工具。

## 已完成关键能力

- CRM 客户新增/编辑/保存。
- 跟进记录新增。
- 跟进记录编辑。
- 跟进记录删除。
- 删除跟进记录不删除客户。
- 死单标记。
- 死单恢复有效。
- 今日待跟进。
- 逾期未跟进。
- 漏斗统计。
- 抖音线索转 CRM。
- `report.html` 读取 CRM、客户池、抖音线索、AI 研判。
- `city-analysis.html` 读取系统数据。
- `material-lab.html` 生成 A/B/C/D 素材矩阵。
- AI 调令可复制/保存。
- 新客户和客户阶段逻辑拆分。

## 最新重要规则

- `isNewCustomer` 表示是否新客户。
- `newCustomerDate` 表示新增日期。
- `customerStage` / `status` 表示推进阶段。
- 新客户可以同时是已量房、已报价、已签单。
- 今日新增客户按 `newCustomerDate` 统计。
- 客户阶段不再作为新客户唯一判断依据。
- CRM 是正式客户主台账。
- 抖音线索池是前置线索池。
- `report.html` 和 `city-analysis.html` 读取数据生成内容，不直接删除业务数据。

## 后续维护建议

- 后续如新增功能，必须同步更新 `CHANGELOG.md`。
- 如新增字段，必须同步更新 `DATA_SCHEMA.md`。
- 如新增页面，必须同步更新 `PAGE_MAP.md`。
- 如改变业务流程，必须同步更新 `WORKFLOW.md`。
- 如新增系统规则，必须同步更新 `SYSTEM_RULES.md`。
- 未经用户确认，Codex 不要默认 Commit / Push。
