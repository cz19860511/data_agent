# 语义模型管理设计

语义模型管理用于把 Doris 中的物理表转换成 Wren 和 Agent 可理解的业务模型，是通用问数平台的语义入口。

## 1. 目标

- 管理业务实体模型
- 管理指标、维度和关系
- 管理字段别名、说明、同义词
- 管理模型版本和发布状态
- 支持不同客户的模型配置化接入

## 2. 核心对象

### 2.1 模型

关键字段：
- `model_id`
- `tenant_id`
- `model_name`
- `model_type`
- `base_table`
- `version`
- `publish_status`

### 2.2 字段语义

关键字段：
- `field_id`
- `model_id`
- `field_name`
- `alias_name`
- `business_name`
- `description`
- `is_dimension`
- `is_metric`

### 2.3 模型关系

关键字段：
- `relation_id`
- `source_model_id`
- `target_model_id`
- `join_type`
- `join_keys`
- `status`

### 2.4 语义规则

关键字段：
- `rule_id`
- `tenant_id`
- `rule_type`
- `rule_content`
- `version`
- `status`

## 3. 管理能力

- 新建模型
- 编辑字段说明
- 配置同义词
- 配置模型关系
- 发布模型版本
- 回滚模型版本

## 4. 与 Wren 的关系

- 语义模型管理是控制面能力
- Wren 是语义层执行载体
- 模型配置最终要导出到 Wren 项目
- Agent 只读取已发布模型

## 5. 一期建议

一期先支持：
- 手工创建模型
- 手工配置字段语义
- 手工配置模型关系
- 手工发布模型版本

后续再升级为：
- 图形化建模
- 自动 schema 识别
- 语义校验
- 模板市场
