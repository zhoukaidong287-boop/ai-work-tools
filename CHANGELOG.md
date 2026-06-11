# CHANGELOG

本文档初始化记录当前 `ai-work-tools` 已完成的重要功能和后续维护规则。

## P0 数据安全加固

- CRM 清空全部数据增加二次确认和确认词 `清空CRM`。
- CRM 清空前自动保存 `crmBackupBeforeClear_YYYYMMDD_HHmmss` 备份。
- CRM JSON 导出升级为结构化备份文件，文件名格式为 `crm-backup-YYYYMMDD-HHmmss.json`。
- CRM JSON 导入增加预览：导入数量、当前数量、重复数量、新增数量、异常数量和覆盖风险。
- CRM 导入默认走合并导入，保留现有客户并跳过重复客户。
- CRM 覆盖导入必须输入确认词 `覆盖导入CRM`，并先保存 `crmBackupBeforeImport_YYYYMMDD_HHmmss` 备份。
- 首页全站数据备份文件名升级为 `ai-work-tools-full-backup-YYYYMMDD-HHmmss.json`。
- 首页全站数据导入增加 key 预览、覆盖风险提示和确认词 `覆盖导入全部数据`。
- 全站覆盖导入前自动保存 `fullBackupBeforeImport_YYYYMMDD_HHmmss` 备份。
- `city-analysis.html` 的 CRM 高危写操作统一引导到 CRM 页面，保持 AI 研判页只读 CRM 数据。

## 第 2 刀：新增 AGENTS.md 项目约束

- 新增 `AGENTS.md` 作为 Codex 修改项目的入口规则文件。
- 固化项目定位、页面职责、数据安全红线。
- 固化 `localStorage` key 保护规则。
- 固化 Codex 修改范围、Commit/Push、自检验收规则。
- 固化代码屎山治理顺序。
- 明确 Computer Use 和 Skill 的使用原则。

## 第 3 刀：douyin-leads.html 格式化治理

- 整理 `douyin-leads.html` 压缩式代码。
- 保留原 `localStorage` key。
- 保留抖音线索转 CRM 逻辑。
- 保留 `isNewCustomer` / `newCustomerDate` 写入逻辑。
- 保留有效/无效、分配销售、导出、删除等功能。
- 未修改业务逻辑。

## 第 4 刀：统一日期 helper 与业务日期规则

- 统一 `YYYY-MM-DD` 日期 key 规则。
- 明确系统日期与业务日期区别。
- 强化 `report.html` 按日报日期读取。
- 强化 `city-analysis.html` 按研判日期保存/读取。
- 梳理 CRM 新客户日期与跟进日期规则。
- 未修改 `localStorage` key。
- 未迁移旧数据。

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
