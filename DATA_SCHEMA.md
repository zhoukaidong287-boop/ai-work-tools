# DATA_SCHEMA

本文档记录 `ai-work-tools` 的核心数据结构、字段含义和 `localStorage` key。字段命名以业务语义为准；当前代码中部分字段存在历史别名，修改前必须搜索实际实现。

## 1. CRM 客户数据字段

CRM 客户主数据保存在 `decorationStoreCrmCustomers`。旧版本可能使用 `customers`。

### CRM 主数据与备份规则

- `decorationStoreCrmCustomers` 是 CRM 正式客户主台账 key，后续不得随意改名。
- `customers` 仅作为旧版数据读取兼容 key，新增功能不得继续写入该 key。
- CRM 清空、覆盖导入、全量覆盖导入前必须先自动备份当前数据。
- CRM 清空前备份 key：`crmBackupBeforeClear_YYYYMMDD_HHmmss`。
- CRM 覆盖导入前备份 key：`crmBackupBeforeImport_YYYYMMDD_HHmmss`。
- 全站数据覆盖导入前备份 key：`fullBackupBeforeImport_YYYYMMDD_HHmmss`。
- CRM JSON 导出文件名格式：`crm-backup-YYYYMMDD-HHmmss.json`。
- 全站 JSON 备份文件名格式：`ai-work-tools-full-backup-YYYYMMDD-HHmmss.json`。
- CRM 导入默认必须走合并导入，保留现有客户并跳过重复客户。
- CRM 覆盖导入必须输入确认词 `覆盖导入CRM`。
- CRM 清空必须输入确认词 `清空CRM`。
- 全站覆盖导入必须输入确认词 `覆盖导入全部数据`。
- 重复客户判断优先级：相同电话；无电话时相同姓名 + 小区；再按姓名 + 面积 + 小区兼容判断。
- 导入兼容格式：数组、`{ customers: [...] }`、`{ data: [...] }`。

### 标准业务字段

- `id`：客户唯一 ID。
- `name`：客户姓名。
- `phone`：电话。
- `wechat`：微信，部分页面可能未单独存储。
- `community`：小区。
- `area`：面积。
- `houseType` / `layout`：户型。
- `salesName` / `owner`：所属销售。
- `designer`：配合设计师。
- `customerLevel` / `grade`：客户等级，例如 A 类客户、B 类客户、C 类客户、死单。
- `customerStage` / `status`：客户阶段，例如新线索、已联系、已进店、已量房、已出方案、已报价、已交定金、已签单、沉睡客户、死单。
- `isNewCustomer`：是否新客户，`true` / `false`。
- `newCustomerDate`：新增日期，格式 `YYYY-MM-DD`。
- `source`：客户来源。
- `budget`：预算。
- `style`：风格，部分页面可能未单独存储。
- `needs` / `need`：装修需求或备注。
- `currentProblem` / `blockReason`：当前卡点、死单原因。
- `nextAction`：下一步动作。
- `nextFollowDate`：下次跟进时间，格式 `YYYY-MM-DD`。
- `remark`：备注。
- `followRecords`：跟进记录数组。
- `isDead`：是否死单，当前代码多通过 `grade === "死单"` 或 `status === "死单"` 判断。
- `deadReason`：死单原因，当前代码可能存放在 `blockReason`。
- `createdAt`：创建时间。
- `updatedAt`：更新时间。

### 新客户规则

- `isNewCustomer` 表示是否新客户。
- `newCustomerDate` 表示新增日期。
- 新客户不是客户阶段。
- 一个客户可以同时是“新客户 + 已量房”。
- 一个客户可以同时是“新客户 + 已报价”。
- 今日新增客户按 `newCustomerDate` 统计，不按 `status === "新线索"` 统计。
- 旧客户如果缺少 `isNewCustomer`，默认不能强制视为新客户。
- 旧客户如果缺少 `newCustomerDate`，可以从 `createdAt` 做兼容展示，但不能批量改写旧数据。

## 2. 跟进记录字段

跟进记录通常保存在客户对象的 `followRecords` 数组中。

- `id`：跟进记录 ID。
- `followDate` / `followTime`：跟进时间。
- `method`：跟进方式。
- `content`：跟进内容。
- `stage` / `status`：跟进后阶段。
- `level` / `grade`：跟进后客户等级。
- `problem` / `blockReason`：当前卡点。
- `nextAction`：下一步动作。
- `nextFollowDate`：下次跟进时间。
- `remark`：备注。
- `owner`：跟进人或所属销售。
- `createdAt`：记录创建时间。
- `updatedAt`：记录更新时间。

### 跟进记录规则

- 跟进记录可以编辑。
- 跟进记录可以删除。
- 编辑跟进记录不应该重复新增记录。
- 删除跟进记录不删除客户。
- 删除跟进记录不应自动回退客户阶段。
- 如果编辑跟进记录时修改了客户阶段、等级、下次跟进时间等字段，可以同步更新客户主字段。
- 旧跟进记录缺字段时不能报错。

## 3. 抖音线索池字段

抖音线索池保存在 `douyinLeads`，操作历史保存在 `douyinLeadHistory`。

- `id`：线索 ID。
- `name`：客户姓名。
- `phone`：电话。
- `wechat`：微信。
- `community` / `area`：小区或区域。
- `areaSize`：面积。
- `houseType` / `layout`：户型。
- `sourceType` / `source`：抖音信息流、私信、评论、直播、主页留资等。
- `sourceVideo` / `materialName`：来源视频或素材。
- `keyword` / `keywords`：私信关键词。
- `painPoint` / `pains`：客户痛点。
- `firstQuestion` / `initialQuestion`：客户初始问题。
- `customerLevel` / `grade`：客户等级。
- `salesName` / `assignedSales`：分配销售。
- `isValidLead` / `validity`：是否有效线索。
- `invalidReason`：无效原因。
- `status`：处理状态。
- `transferredToCrm`：是否已转 CRM，当前代码主要通过 `status === "已转入CRM"` 或 `crmCustomerId` 判断。
- `crmCustomerId`：对应 CRM 客户 ID。
- `createdAt`：创建时间。
- `updatedAt`：更新时间。

### 抖音线索转 CRM 规则

- 抖音线索池是前置线索清洗池，不等于正式 CRM。
- 抖音线索转 CRM 时，CRM 客户应自动设置 `isNewCustomer = true`。
- `newCustomerDate` 默认为转入 CRM 当天。
- 转 CRM 后客户阶段可以变成已量房、已报价或已签单，但 `isNewCustomer` 不应被覆盖。
- 重复转 CRM 必须有保护，不能重复创建同一客户。

## 4. 日报/AI 研判相关数据

`report.html` 和 `city-analysis.html` 只读取数据并生成文案，不应直接删除 CRM、客户池复盘或抖音线索池数据。

读取原则：

- 读取 CRM 客户。
- 读取客户池复盘。
- 读取抖音线索池。
- 读取 AI 研判历史。
- 读取活动政策/机制资料。
- 不直接删除这些数据。
- 生成的日报和 AI 研判结果必须允许人工编辑。

## 5. localStorage key

以下 key 以当前代码实现为准，修改前必须先搜索 `localStorage.setItem` / `localStorage.getItem`。

### CRM 与项目信息

- `decorationStoreCrmCustomers`：CRM 客户主台账。
- `customers`：旧版客户数据兼容 key。
- `pointProjectInfo`：当前点将项目、点将周期等项目信息。
- `pointPreJudgeRecords`：点将前置研判或城市研判历史。
- `dynamicAnalysisHistory`：动态研判历史。

### 客户池复盘

- `customerReviewRecords`：客户池复盘历史记录。
- `customerReviewDraft`：当前客户池复盘草稿。

### 抖音线索池

- `douyinLeads`：抖音线索池。
- `douyinLeadHistory`：抖音线索操作历史。

### 日报/周报

- `pointReportRecords`：日报/周报/阶段汇报历史，同一 key 内可能混合日报、周报、阶段汇报等不同记录类型，读取时必须按 `type`、标题或日期字段防御式过滤。
- `pointReportBaseInfo`：日报基础项目信息。
- `reportDataSummaryDraft`：日报读取数据摘要草稿。
- `reportAnalysisSummaryDraft`：日报读取 AI 研判摘要草稿。
- `dailyReportDraft`：日报生成结果草稿。

### AI 每日点将研判

- `dailyAnalysisDrafts`：每日 AI 研判草稿。
- `dailyAnalysisHistory`：每日 AI 研判历史，按日期读取和保存，不能默认只读取系统当天；跨日期读取时必须使用用户选择的日期。
- `activityPolicyTemplates`：活动政策/机制资料模板。
- `currentActivityPolicy`：当前活动政策/机制资料。
- `dailyAnalysisPromptTemplates`：AI 调令模板。

### 信息流素材

- `materialLabHistory`：信息流素材矩阵历史。
- `materialLabAiPromptDraft`：信息流 AI 调令草稿。
- `materialLabAiPromptHistory`：信息流 AI 调令历史。

### 投流测试

- `pointAdTestRecords`：投流测试记录。
