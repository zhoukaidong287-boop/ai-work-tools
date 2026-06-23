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

## 第 5 刀：统一客户统计口径

- 区分客户阶段和客户动作：客户当前阶段表示当前推进状态，进店、量房、报价、跟进等作为动作次数单独统计。
- 统一有效客户、死单、新客户、A/B/C 统计口径：有效客户排除死单/明确无效客户，新客户优先按 `newCustomerDate` + 业务日期判断，A/B/C 默认不包含死单。
- 同步 CRM、日报、AI研判、首页统计规则，避免把家装客户强行当作严格线性漏斗。
- 未修改 `localStorage` key。
- 未迁移旧数据。

## 第 6 刀：首页 Growth Command 产品级视觉升级

- 使用 Product Design 能力进行首页视觉方案设计后再落地。
- 首页视觉升级为水面庭院 / 雨后庭院 / 木质空间 / 深灰石材方向。
- 移除黑金、科技蓝、霓虹和假科技大屏倾向。
- 重构 Hero、今日简报、核心能力、增长流程、系统入口与状态区域。
- 增加克制动效：淡入、轻微视差、水面反光、卡片 hover。
- 保留首页统计、跳转入口和数据安全功能。
- 未修改 `localStorage` key。
- 未修改业务统计口径。
- 未修改其他业务页面。

## 第 6-2 刀：首页 Hero 场景热点交互修正

- Hero 增加水面反光、灯光亮起、材质光影三个视觉热点层。
- 鼠标经过水面区域时增强水面反光，经过右侧庭院/窗格区域时轻微提升灯光层。
- 交互集中在 `initHeroSceneInteraction()`，移动端和 `prefers-reduced-motion` 下关闭热点交互。
- 未修改 `localStorage` key。
- 未修改业务统计口径。
- 未修改其他业务页面。

## 第 6-3 刀：首页 AI Studio 动效原型接入准备

- 读取 AI Studio 原型包中的 `index.html` 作为视觉和动效参考，未整包替换项目结构。
- 仅接入首页 Hero 第一屏、Today's Brief 卡片层级和轻量动效。
- Today's Brief 继续使用首页现有真实统计逻辑，不写死假数据。
- 新增右侧克制侧向柔光、Hero 轻微视差、Today's Brief hover 和刷新反馈。
- 未接入 Core Infrastructure、Closed Loop、系统状态等下半部分模块。
- 未引入 React、Vite、TypeScript、npm 依赖、Tailwind CDN、Google Fonts 或外部 CDN。
- 未修改 `localStorage` key。
- 未修改业务统计口径。
- 未修改其他业务页面。

## 第 6-3A 刀：首页 Hero 侧射线可见度修正

- 提升 Hero 侧向柔光层级，使其位于背景与遮罩之上、标题和 Today's Brief 下方。
- 将默认侧射线改为可见的 2-3 条右侧斜向柔光，鼠标靠近右侧玻璃/灯光区域时轻微增强。
- 保持侧射线为克制暖白/雾白，不接入霓虹、Web3、科技扫描线或强光斑。
- 未修改 Today's Brief 数据逻辑。
- 未修改 `localStorage` key。
- 未修改业务统计口径。
- 未修改其他业务页面。

## 第 6-3B 刀：首页 Hero 左上角丁达尔光束修正

- 将 Hero 光束方向从右侧泛光改为左上角斜射到页面中部/右下的丁达尔光束。
- 默认显示 3-5 条克制窄光束，并加入低密度空气尘埃与弱反射亮带。
- 鼠标靠近左上角或 Hero 中部时，光束、尘埃和反射层轻微增强。
- 移动端保留静态弱光，`prefers-reduced-motion` 下关闭尘埃漂浮。
- 未修改 Today's Brief 数据逻辑。
- 未修改 `localStorage` key。
- 未修改业务统计口径。
- 未修改其他业务页面。

## 第 6-3C 刀：首页 Hero 右上角持续丁达尔光束修正

- 将 Hero 丁达尔光源修正为右上角，光束从右上斜向左下/中部洒落。
- 默认保持 3-5 条窄光束持续可见，并加入 14s 的自然慢流动。
- 光束内部保留低密度空气尘埃，尘埃以 18s 周期轻微漂浮。
- 鼠标靠近右上角时仅轻微增强光束，不作为唯一触发条件。
- 未修改 Today's Brief 数据逻辑。
- 未修改 `localStorage` key。
- 未修改业务统计口径。
- 未修改其他业务页面。

## 第 6 刀：首页产品级视觉升级 70%-80% 成型版

- 将首页重构为 Growth Command 产品级入口页，聚焦顶部导航、Hero 主视觉、作战模块矩阵、增长作战流程、底部 CTA 五个区域。
- 视觉方向调整为暖灰白、石墨灰、低饱和蓝灰的高级 AI SaaS / 企业增长作战系统风格。
- 保留现有 CRM、日报/周报、线索管理、AI 经营研判、投流测试、素材实验室等真实工具入口。
- Hero 右上角保留弱版丁达尔窄光束与轻量产品卡片组合，不接入黑金、Web3、霓虹或复杂大屏动效。
- 首页新增 `gc-` 前缀样式命名空间和 `initGrowthCommandHeader` / `initGrowthCommandReveal` / `initGrowthCommandCards` 初始化函数。
- 保留数据安全备份导出/导入入口，未删除已有页面跳转能力。
- 未新增 React、Vue、Tailwind、GSAP、Three.js、Framer Motion 或 npm 依赖。
- 未修改 `localStorage` key。
- 未修改业务统计口径。
- 未修改其他业务页面。

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
