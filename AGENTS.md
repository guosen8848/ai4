# AGENTS.md

## 整体规则
1. 当docs/目录为空时，调用 `skills/init-control-docs/init-control-docs.md` 
2. 整体规则加载 `docs/CLOUD.md`
3. 注释，说明，文档使用中文

## 修改文件后操作
在修改代码后
1. 技术栈添加，接口更改，目录更改同步至 `docs/ARCHITECTURE.md`
2. 操作记录记录至 `docs/SCHEDULE.md`

## 每次与用户对话后操作
每次与用户对话后，判断是否会对整个项目产生影响，如果会，就将对话压缩后，保存至 `docs/CHAT.md`

## 提交更新计划时
在读到用户的更新计划时，调用 `skills/scope_gate.md` skill处理


## AI控制文档说明
`skills/init-control-docs/templates/` 只存放初始化模板；`docs/` 存放正式控制文档。项目运行过程中，以 `docs/` 下的正式文件为准。

### 1、ARCHITECTURE.md

1. 功能：记录项目当前事实，包括技术栈、目录结构、模块清单、页面清单、接口清单、数据模型清单、配置和部署现状。
2. 维护规则：当架构事实、技术栈、目录、接口清单或模块清单发生变化时，AI 应同步更新本文档。
3. 边界：稳定规则、长期约束、接口约定、命名约定不写入本文档，应放入 `docs/RULE.md`。
4. 模板文件：`skills/init-control-docs/templates/temp_ARCHITECTURE.md`
5. 实际控制文件：`docs/ARCHITECTURE.md`

### 2、SCHEDULE.md
1. 功能：项目推进短日志，只记录已经发生的项目变更和验证结果。
2. 边界：不记录讨论过程、未执行计划和未确认设想。
3. 模板文件：`skills/init-control-docs/templates/temp_SCHEDULE.md`
4. 实际控制文件：`docs/SCHEDULE.md`

### 3、CHAT.md
1. 功能：项目级对话决策摘要。
2. 记录条件：只有当用户明确确认新的项目规则、需求、计划或架构决策时，才写入 `docs/CHAT.md`。
3. 边界：未确认的评估意见、普通问答和过程性讨论不得写入，只在对话中输出。
4. 模板文件：`skills/init-control-docs/templates/temp_CHAT.md`
5. 实际控制文件：`docs/CHAT.md`

### 4、CLOUD.md
1. 功能：控制 AI 在本项目中的整体执行逻辑和行为原则。
2. 模板文件：`skills/init-control-docs/templates/temp_CLOUD.md`
3. 实际控制文件：`docs/CLOUD.md`

### 5、RULE.md
1. 功能：记录稳定规则和长期约束，例如项目目标、分层架构、接口约定、命名约定和 AI 编码禁区。
2. 维护规则：本文档由用户手动维护，AI 不得主动修改。
3. 建议规则：如果 AI 认为需要新增或调整 `RULE.md` 中的规则，只能在对话中明确提出原因、影响和建议，等待用户手动修改或明确授权。
4. 模板文件：`skills/init-control-docs/templates/temp_RULE.md`
5. 实际控制文件：`docs/RULE.md`

## 开发流程

### 第一步：初始化规则

当docs/目录为空时，调用 `skills/init-control-docs/init-control-docs.md`，初始化项目控制文档

### 第二步：判断是否为最小功能
在读取更新计划后，加载`skills/scope_gate.md`处理，判断是否为最小功能
通过后开始第三步

### 第三步：制定更新计划
在最小功能通过后，加载`skills/update-plan-review/update-plan-review.md`处理，生成开发文档

### 第四步：根据文档进行开发
调用`/superpowers:test-driven-development`，进行TDD开发，将变更同步至ARCHITECTURE.md，SCHEDULE.md
