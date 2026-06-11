# 平台控制面设计

平台控制面负责管理通用问数平台的配置、版本、权限和发布能力，是整个平台“可运营、可配置、可隔离”的核心。

## 1. 目标

- 支持多租户接入
- 支持数据源配置
- 支持语义模型配置
- 支持指标定义和版本管理
- 支持权限策略管理
- 支持发布、回滚、冻结

## 2. 核心模块

### 2.1 租户管理

职责：
- 创建和管理租户
- 配置租户隔离策略
- 管理租户级默认配置

关键字段：
- `tenant_id`
- `tenant_name`
- `isolation_mode`
- `status`
- `created_at`

### 2.2 数据源管理

职责：
- 注册客户源库
- 保存连接信息
- 测试连通性
- 控制启停

关键字段：
- `datasource_id`
- `tenant_id`
- `source_type`
- `endpoint`
- `status`

### 2.3 语义模型管理

职责：
- 管理 Wren 模型配置
- 维护模型关系
- 管理模型版本

关键字段：
- `model_id`
- `tenant_id`
- `model_name`
- `version`
- `publish_status`

### 2.4 指标管理

职责：
- 定义指标
- 维护口径版本
- 展示解释卡片

关键字段：
- `metric_code`
- `metric_name`
- `formula`
- `version`
- `owner`

### 2.5 权限管理

职责：
- 管理角色、组织、数据范围
- 管理行级和字段级权限
- 为 SQL 网关提供权限决策

关键字段：
- `policy_id`
- `role_code`
- `scope_type`
- `scope_value`
- `effect`

### 2.6 发布管理

职责：
- 发布模型和配置
- 支持灰度和回滚
- 支持冻结与解冻

关键字段：
- `release_id`
- `resource_type`
- `resource_id`
- `version`
- `status`

## 3. 平台接口边界

- 前端只操作控制面 API
- Agent 不直接改控制面配置
- 数据接入层只读取必要配置
- SQL 网关只消费授权结果和租户上下文

## 4. 一期建议

一期先完成：
- 租户管理
- 数据源管理
- 指标管理
- 权限管理
- 发布记录

语义模型管理可先以文件配置和手工发布为主，后续再升级为全自动发布。
