# 数据源管理设计

数据源管理是通用问数平台接入客户底层数据的入口，负责把客户源库、文件源、API 源统一注册到平台中。

## 1. 目标

- 统一注册各类数据源
- 保存连接信息和接入方式
- 支持连通性测试
- 支持启停、重试和状态管理
- 为 Doris ODS 接入提供标准配置

## 2. 数据源类型

- MySQL
- PostgreSQL
- SQL Server
- Oracle
- Doris
- CSV / Excel 文件
- HTTP API

## 3. 核心对象

### 3.1 数据源定义

关键字段：
- `datasource_id`
- `tenant_id`
- `datasource_name`
- `datasource_type`
- `endpoint`
- `port`
- `database_name`
- `username`
- `status`

### 3.2 表映射定义

关键字段：
- `mapping_id`
- `source_table`
- `target_table`
- `field_mapping`
- `primary_key`
- `update_time_field`
- `sync_mode`

### 3.3 同步任务定义

关键字段：
- `task_id`
- `datasource_id`
- `task_type`
- `schedule_type`
- `status`
- `last_run_at`

## 4. 接入流程

1. 注册数据源
2. 测试连接
3. 选择表或文件
4. 配置字段映射
5. 配置同步策略
6. 生成 ODS 落地任务
7. 监控同步结果

## 5. 一期建议

一期先支持：
- 关系型数据库接入
- 文件导入接入
- 手工字段映射
- 全量同步

后续再补：
- CDC 增量同步
- 自动 schema 识别
- 连接池管理
- 接入模板市场
