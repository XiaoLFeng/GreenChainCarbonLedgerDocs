# 数据库文档

#### 1、 fy_approve_manage
管理用户认证

| 序号 | 名称 | 描述 | 类型 | 键 | 为空 | 额外 | 默认值 |
| :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: |
| 1 | `id` | 主键 | bigint unsigned | PRI | NO | auto_increment |  |
| 2 | `account_uuid` | 账户UUID | char(36) | MUL | NO |  |  |
| 3 | `account_type` | 如"管理员"、"政府环保部门"、"第三方审核机构" | tinyint unsigned |  | NO |  |  |
| 4 | `organize_name` | 组织名称 | varchar(100) |  | NO |  |  |
| 5 | `organize_authorize_url` | 授权书地址 | varchar(255) |  | NO |  |  |
| 6 | `legal_representative_name` | 代表人名字 | varchar(100) |  | NO |  |  |
| 7 | `legal_representative_id` | 代表人身份证 | char(18) |  | YES |  |  |
| 8 | `certification_status` | 认证状态(0: 未通过，1: 通过，2: 拒绝） | tinyint unsigned |  | NO |  | 0 |
| 9 | `apply_time` | 申请时间 | datetime |  | NO | DEFAULT_GENERATED | CURRENT_TIMESTAMP |
| 10 | `approve_time` | 审批时间 | datetime |  | YES |  |  |
| 11 | `updatedAt` | 修改时间 | timestamp |  | YES |  |  |
| 12 | `remarks` | 备注 | varchar(255) |  | YES |  |  |
| 13 | `approve_uuid` | 审批人 | char(36) | MUL | YES |  |  |
| 14 | `approve_remarks` | 审批人备注 | varchar(255) |  | YES |  |  |


#### 2、 fy_approve_organize
组织账户认证

| 序号 | 名称 | 描述 | 类型 | 键 | 为空 | 额外 | 默认值 |
| :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: |
| 1 | `id` | 主键ID | bigint unsigned | PRI | NO | auto_increment |  |
| 2 | `account_uuid` | 账户的全局唯一标识符UUID  | char(36) | UNI | NO |  |  |
| 3 | `type` | 类型（0：管理员审核、1：支付宝审核、等） | tinyint |  | NO |  | 0 |
| 4 | `organize_name` | 组织名称 | varchar(255) |  | NO |  |  |
| 5 | `organize_license_url` | 营业执照的URL地址 | varchar(255) |  | NO |  |  |
| 6 | `organize_credit_code` | 企业统一社会信用代码，长度18位 | varchar(18) | UNI | NO |  |  |
| 7 | `organize_registered_capital` | 注册资本，支持小数点后两位 | decimal(10,2) |  | NO |  |  |
| 8 | `organize_establishment_date` | 成立日期 | date |  | NO |  |  |
| 9 | `legal_representative_name` | 法人代表姓名 | varchar(100) |  | NO |  |  |
| 10 | `legal_representative_id` | 法人代表身份证 | varchar(18) |  | NO |  |  |
| 11 | `legal_id_card_front_url` | 法人代表身份证正面照片URL地址 | varchar(255) |  | NO |  |  |
| 12 | `legal_id_card_back_url` | 法人代表身份证反面照片URL地址 | varchar(255) |  | NO |  |  |
| 13 | `certification_status` | 认证状态，如0未认证，1已认证，2认证拒绝 | tinyint |  | NO |  | 0 |
| 14 | `apply_time` | 申请时间 | datetime |  | NO | DEFAULT_GENERATED | CURRENT_TIMESTAMP |
| 15 | `approve_time` | 审批时间 | datetime |  | NO |  |  |
| 16 | `updated_at` | 修改时间 | timestamp |  | YES |  |  |
| 17 | `remarks` | 备注信息 | varchar(255) |  | YES |  |  |
| 18 | `approver_uuid` | 审批人 | char(36) | MUL | NO |  |  |
| 19 | `approver_remarks` | 审批人备注 | text |  | YES |  |  |


#### 3、 fy_carbon_accounting
碳核算数据表

| 序号 | 名称 | 描述 | 类型 | 键 | 为空 | 额外 | 默认值 |
| :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: |
| 1 | `id` | 主键 | bigint unsigned | PRI | NO | auto_increment |  |
| 2 | `organize_uuid` | 企业唯一标识符，与企业信息表的organize_uuid字段关联。 | char(46) | MUL | NO |  |  |
| 3 | `emission_source` | 碳排放源，如能源消耗、生产过程、物流等。 | varchar(255) |  | NO |  |  |
| 4 | `emission_amount` | 碳排放量，单位可为吨CO2等价物。 | int |  | NO |  |  |
| 5 | `accounting_period` | 核算周期，通常为一个财年或特定时间段。(20230101-20230120) | varchar(17) |  | NO |  |  |
| 6 | `data_verification_status` | 数据核验状态，可用值：'pending', 'verified', 'rejected'。 | varchar(8) |  | NO |  | pending |
| 7 | `verifier_uuid` | 数据审核员/核验员的唯一标识符，与用户信息表关联。 | char(36) | MUL | YES |  |  |
| 8 | `verification_notes` | 核验备注，核验员填写的关于核验结果的详细说明。 | text |  | YES |  |  |
| 9 | `carbon_report_id` | 生成的碳排放报告ID，与碳排放报告表关联。 | bigint unsigned | MUL | YES |  |  |
| 10 | `blockchain_tx_id` | 碳报告铸造和上链后的区块链交易ID，用于追踪和验证。 | int |  | YES |  |  |
| 11 | `created_at` | 记录创建时间 | timestamp |  | NO | DEFAULT_GENERATED | CURRENT_TIMESTAMP |
| 12 | `updated_at` | 记录最后更新时间 | timestamp |  | YES |  |  |


#### 4、 fy_carbon_quota
碳排放配额

| 序号 | 名称 | 描述 | 类型 | 键 | 为空 | 额外 | 默认值 |
| :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: |
| 1 | `uuid` | 碳排放UUID | char(36) | PRI | NO |  |  |
| 2 | `organize_uuid` | 组织用户UUID | char(36) | MUL | NO |  |  |
| 3 | `quota_year` | 配额年份，表示这个配额分配给企业的年份 | int unsigned |  | NO |  |  |
| 4 | `total_quota` | 总配额量，单位通常为吨CO2等价物。 | decimal(10,0) |  | NO |  |  |
| 5 | `allocated_quota` | 已分配配额量，单位同上。初始时可能与总配额量相等，随后可能因为市场交易而变化。 | decimal(10,0) |  | NO |  |  |
| 6 | `used_quota` | 已使用配额量，表示企业实际消耗的碳配额。 | decimal(10,0) |  | NO |  | 0 |
| 7 | `allocation_date` | 配额分配日期，记录企业配额分配的确切日期。 | date |  | YES |  |  |
| 8 | `compliance_status` | 合规状态，记录企业碳排放是否符合分配的配额。 | tinyint(1) |  | NO |  | 0 |
| 9 | `audit_log` | 审计日志，记录配额分配、使用和交易的详细情况，可用于审计和溯源。 | json |  | YES |  |  |
| 10 | `created_at` | 创建时间 | timestamp |  | NO | DEFAULT_GENERATED | CURRENT_TIMESTAMP |
| 11 | `updated_at` | 修改日期 | timestamp |  | YES |  |  |


#### 5、 fy_carbon_report
碳排放报告数据表

| 序号 | 名称 | 描述 | 类型 | 键 | 为空 | 额外 | 默认值 |
| :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: |
| 1 | `id` | 碳排放报告唯一标识符，主键 | bigint unsigned | PRI | NO | auto_increment |  |
| 2 | `organize_uuid` | 企业唯一标识符，与企业信息表的organize_uuid字段关联 | char(36) | MUL | NO |  |  |
| 3 | `accounting_period` | 报告涵盖的核算周期，通常为一个财年或特定时间段。(20230101-20230120) | varchar(17) |  | NO |  |  |
| 4 | `total_emission` | 报告周期内总碳排放量，单位可为吨CO2等价物。 | decimal(10,0) |  | NO |  |  |
| 5 | `emission_reduction` | 报告周期内实现的碳减排量，单位同上。 | decimal(10,0) |  | NO |  |  |
| 6 | `net_emission` | 净碳排放量，计算得出，= total_emission - emission_reduction | decimal(10,0) |  | NO |  |  |
| 7 | `report_status` | 报告状态，可用值：'draft', 'pending_review', 'approved', 'rejected'。 | varchar(14) |  | NO |  | draft |
| 8 | `verifier_uuid` | 审核员的唯一标识符，与用户信息表关联。 | char(36) | MUL | YES |  |  |
| 9 | `verification_date` | 审核日期。 | date |  | YES |  |  |
| 10 | `report_summary` | 报告摘要，概述关键碳排放和减排信息。 | text |  | YES |  |  |
| 11 | `blockchain_tx_id` | 报告铸造和上链后的区块链交易ID，用于追踪和验证。 | varchar(255) |  | YES |  |  |
| 12 | `created_at` | 记录创建时间 | timestamp |  | NO | DEFAULT_GENERATED | CURRENT_TIMESTAMP |
| 13 | `updated_at` | 修改时间 | timestamp |  | YES |  |  |


#### 6、 fy_carbon_trade
碳交易发布

| 序号 | 名称 | 描述 | 类型 | 键 | 为空 | 额外 | 默认值 |
| :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: |
| 1 | `id` | 列表唯一标识符，主键。 | bigint unsigned | PRI | NO | auto_increment |  |
| 2 | `organize_uuid` | 发布交易的企业唯一标识符，与企业信息表的organize_uuid字段关联。 | char(36) | MUL | NO |  |  |
| 3 | `quota_amount` | 出售的碳排放额度，单位通常为吨CO2等价物。 | decimal(10,0) |  | NO |  |  |
| 4 | `price_per_unit` | 每单位碳排放额度的价格，可根据市场定价。 | decimal(10,0) |  | NO |  |  |
| 5 | `status` | 发布状态，可用值：'draft,'active', 'completed', 'cancelled'。 | varchar(9) |  | NO |  | draft |
| 6 | `description` | 交易详情描述，可以包含额外信息如碳排放额度的来源、有效期等。 | text |  | NO |  |  |
| 7 | `verify_uuid` | 验证人 | char(36) | MUL | NO |  |  |
| 8 | `blockchain_tx_id` | 关联的区块链交易ID，用于在区块链上追踪具体的交易记录。 | varchar(255) |  | NO |  |  |
| 9 | `created_at` | 创建时间 | timestamp |  | NO | DEFAULT_GENERATED | CURRENT_TIMESTAMP |
| 10 | `updated_at` | 修改时间 | timestamp |  | YES |  |  |


#### 7、 fy_invite
邀请

| 序号 | 名称 | 描述 | 类型 | 键 | 为空 | 额外 | 默认值 |
| :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: |
| 1 | `id` | 邀请主键 | bigint unsigned | PRI | NO | auto_increment |  |
| 2 | `uuid` | 用户外键 | char(36) | MUL | NO |  |  |
| 3 | `code` | 邀请码 | char(10) | UNI | NO |  |  |
| 4 | `created_at` | 创建时间 | timestamp |  | NO | DEFAULT_GENERATED | CURRENT_TIMESTAMP |
| 5 | `updated_at` | 修改时间 | timestamp |  | YES |  |  |


#### 8、 fy_permission
权限

| 序号 | 名称 | 描述 | 类型 | 键 | 为空 | 额外 | 默认值 |
| :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: |
| 1 | `pid` | 权限id | bigint unsigned | PRI | NO | auto_increment |  |
| 2 | `name` | 权限名字 | varchar(50) | UNI | NO |  |  |
| 3 | `description` | 权限描述 | varchar(100) |  | YES |  |  |


#### 9、 fy_role
角色列表

| 序号 | 名称 | 描述 | 类型 | 键 | 为空 | 额外 | 默认值 |
| :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: |
| 1 | `id` | 列表id | tinyint unsigned | PRI | NO | auto_increment |  |
| 2 | `uuid` | 列表唯一识别码 | char(36) | UNI | NO |  |  |
| 3 | `name` | 角色名字 | varchar(36) |  | NO |  |  |
| 4 | `display_name` | 展示名字 | varchar(20) |  | NO |  |  |
| 5 | `permission` | 角色权限 | json |  | YES |  |  |
| 6 | `created_at` | 创建时间 | timestamp |  | NO | DEFAULT_GENERATED | CURRENT_TIMESTAMP |
| 7 | `updated_at` | 修改时间 | timestamp |  | YES |  |  |
| 8 | `created_user` | 创建用户uuid | char(36) | MUL | YES |  |  |


#### 10、 fy_user
账户

| 序号 | 名称 | 描述 | 类型 | 键 | 为空 | 额外 | 默认值 |
| :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: |
| 1 | `uid` | 账户序列 | bigint unsigned | PRI | NO | auto_increment |  |
| 2 | `uuid` | 用户唯一识别码 | char(36) | UNI | NO |  |  |
| 3 | `user_name` | 用户名 | varchar(40) | UNI | NO |  |  |
| 4 | `nick_name` | 昵称 | varchar(40) |  | YES |  |  |
| 5 | `real_name` | 真实信息 | varchar(40) | UNI | NO |  |  |
| 6 | `email` | 邮箱 | varchar(100) | UNI | NO |  |  |
| 7 | `phone` | 手机号 | varchar(11) | UNI | YES |  |  |
| 8 | `avatar` | 头像 | text |  | YES |  |  |
| 9 | `password` | 密码 | varchar(255) |  | NO |  |  |
| 10 | `role` | 权限组 | char(36) | MUL | NO |  |  |
| 11 | `permission` | 附加权限 | json |  | YES |  |  |
| 12 | `created_at` | 创建时间 | timestamp |  | NO | DEFAULT_GENERATED | CURRENT_TIMESTAMP |
| 13 | `updated_at` | 修改时间 | timestamp |  | YES |  |  |
| 14 | `ban` | 账户封禁 | tinyint(1) |  | NO |  | 0 |
| 15 | `invite` | 邀请码 | char(10) | MUL | YES |  |  |
| 16 | `deleted_at` | 删除时间 | timestamp |  | YES |  |  |


#### 11、 fy_user_ram
子用户

| 序号 | 名称 | 描述 | 类型 | 键 | 为空 | 额外 | 默认值 |
| :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: |
| 1 | `ruid` | 子用户主键 | bigint unsigned | PRI | NO | auto_increment |  |
| 2 | `uuid` | 主用户唯一识别码 | char(36) | MUL | NO |  |  |
| 3 | `ruuid` | 子用户唯一识别码 | char(36) | UNI | NO |  |  |
| 4 | `user_name` | 子用户名 | varchar(40) | UNI | NO |  |  |
| 5 | `nick_name` | 昵称 | varchar(40) |  | YES |  |  |
| 6 | `real_name` | 真实姓名 | varchar(4) |  | YES |  |  |
| 7 | `email` | 邮箱 | varchar(100) | UNI | NO |  |  |
| 8 | `phone` | 手机号 | varchar(11) | UNI | YES |  |  |
| 9 | `password` | 密码 | varchar(255) |  | NO |  |  |
| 10 | `permission` | 权限（不可超过主用户权限） | json |  | YES |  |  |
| 11 | `created_at` | 创建时间 | timestamp |  | NO | DEFAULT_GENERATED | CURRENT_TIMESTAMP |
| 12 | `updated_at` | 修改时间 | timestamp |  | YES |  |  |


#### 12、 fy_user_verify
账户校验

| 序号 | 名称 | 描述 | 类型 | 键 | 为空 | 额外 | 默认值 |
| :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: |
| 1 | `id` | 主键 | bigint unsigned | PRI | NO | auto_increment |  |
| 2 | `uuid` | 用户uuid | char(36) | MUL | NO |  |  |
| 3 | `phone_verify` | 手机号校验 | tinyint(1) |  | NO |  | 0 |
| 4 | `email_verify` | 邮箱验证 | tinyint(1) |  | NO |  | 0 |
| 5 | `phone_verify_time` | 验证时间 | timestamp |  | YES |  |  |
| 6 | `email_verify_time` | 邮箱验证时间 | timestamp |  | YES |  |  |


----

# 数据库导入文件

> 为方便后期一件操作或恢复出厂，配置Mysql导入文件配置信息

```mysql
-- phpMyAdmin SQL Dump
-- version 5.2.1
-- https://www.phpmyadmin.net/
--
-- 主机： 172.17.0.2
<<<<<<< HEAD
-- 生成日期： 2024-03-13 06:26:44
=======
-- 生成日期： 2024-03-13 08:01:41
>>>>>>> 7af12f3 (Upload)
-- 服务器版本： 8.2.0
-- PHP 版本： 8.2.16

SET SQL_MODE = "NO_AUTO_VALUE_ON_ZERO";
START TRANSACTION;
SET time_zone = "+00:00";


/*!40101 SET @OLD_CHARACTER_SET_CLIENT=@@CHARACTER_SET_CLIENT */;
/*!40101 SET @OLD_CHARACTER_SET_RESULTS=@@CHARACTER_SET_RESULTS */;
/*!40101 SET @OLD_COLLATION_CONNECTION=@@COLLATION_CONNECTION */;
/*!40101 SET NAMES utf8mb4 */;

--
-- 数据库： `fy_carbon`
--

-- --------------------------------------------------------

--
-- 表的结构 `fy_approve_manage`
--

CREATE TABLE `fy_approve_manage` (
  `id` bigint UNSIGNED NOT NULL COMMENT '主键',
  `account_uuid` char(36) NOT NULL COMMENT '账户UUID',
  `account_type` tinyint UNSIGNED NOT NULL COMMENT '如"管理员"、"政府环保部门"、"第三方审核机构"',
  `organize_name` varchar(100) NOT NULL COMMENT '组织名称',
  `organize_authorize_url` varchar(255) NOT NULL COMMENT '授权书地址',
  `legal_representative_name` varchar(100) NOT NULL COMMENT '代表人名字',
  `legal_representative_id` char(18) DEFAULT NULL COMMENT '代表人身份证',
  `certification_status` tinyint UNSIGNED NOT NULL DEFAULT '0' COMMENT '认证状态(0: 未通过，1: 通过，2: 拒绝）',
  `apply_time` datetime NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '申请时间',
  `approve_time` datetime DEFAULT NULL COMMENT '审批时间',
  `updatedAt` timestamp NULL DEFAULT NULL COMMENT '修改时间',
  `remarks` varchar(255) DEFAULT NULL COMMENT '备注',
  `approve_uuid` char(36) DEFAULT NULL COMMENT '审批人',
  `approve_remarks` varchar(255) DEFAULT NULL COMMENT '审批人备注'
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci COMMENT='管理用户认证';

-- --------------------------------------------------------

--
-- 表的结构 `fy_approve_organize`
--

CREATE TABLE `fy_approve_organize` (
  `id` bigint UNSIGNED NOT NULL COMMENT '主键ID',
  `account_uuid` char(36) NOT NULL COMMENT '账户的全局唯一标识符UUID\n \n',
  `type` tinyint NOT NULL DEFAULT '0' COMMENT '类型（0：管理员审核、1：支付宝审核、等）',
  `organize_name` varchar(255) NOT NULL COMMENT '组织名称',
  `organize_license_url` varchar(255) NOT NULL COMMENT '营业执照的URL地址',
  `organize_credit_code` varchar(18) NOT NULL COMMENT '企业统一社会信用代码，长度18位',
  `organize_registered_capital` decimal(10,2) NOT NULL COMMENT '注册资本，支持小数点后两位',
  `organize_establishment_date` date NOT NULL COMMENT '成立日期',
  `legal_representative_name` varchar(100) NOT NULL COMMENT '法人代表姓名',
  `legal_representative_id` varchar(18) NOT NULL COMMENT '法人代表身份证',
  `legal_id_card_front_url` varchar(255) NOT NULL COMMENT '法人代表身份证正面照片URL地址',
  `legal_id_card_back_url` varchar(255) NOT NULL COMMENT '法人代表身份证反面照片URL地址',
  `certification_status` tinyint NOT NULL DEFAULT '0' COMMENT '认证状态，如0未认证，1已认证，2认证拒绝',
  `apply_time` datetime NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '申请时间',
  `approve_time` datetime NOT NULL COMMENT '审批时间',
  `updated_at` timestamp NULL DEFAULT NULL COMMENT '修改时间',
  `remarks` varchar(255) DEFAULT NULL COMMENT '备注信息',
  `approver_uuid` char(36) NOT NULL COMMENT '审批人',
  `approver_remarks` text COMMENT '审批人备注'
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci COMMENT='组织账户认证';

-- --------------------------------------------------------

--
-- 表的结构 `fy_carbon_accounting`
--

CREATE TABLE `fy_carbon_accounting` (
  `id` bigint UNSIGNED NOT NULL COMMENT '主键',
  `organize_uuid` char(46) NOT NULL COMMENT '企业唯一标识符，与企业信息表的organize_uuid字段关联。',
  `emission_source` varchar(255) NOT NULL COMMENT '碳排放源，如能源消耗、生产过程、物流等。',
  `emission_amount` int NOT NULL COMMENT '碳排放量，单位可为吨CO2等价物。',
  `accounting_period` varchar(17) NOT NULL COMMENT '核算周期，通常为一个财年或特定时间段。(20230101-20230120)',
  `data_verification_status` varchar(8) NOT NULL DEFAULT 'pending' COMMENT '数据核验状态，可用值：''pending'', ''verified'', ''rejected''。',
  `verifier_uuid` char(36) DEFAULT NULL COMMENT '数据审核员/核验员的唯一标识符，与用户信息表关联。',
  `verification_notes` text COMMENT '核验备注，核验员填写的关于核验结果的详细说明。',
  `carbon_report_id` bigint UNSIGNED DEFAULT NULL COMMENT '生成的碳排放报告ID，与碳排放报告表关联。',
  `blockchain_tx_id` int DEFAULT NULL COMMENT '碳报告铸造和上链后的区块链交易ID，用于追踪和验证。',
  `created_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '记录创建时间',
  `updated_at` timestamp NULL DEFAULT NULL COMMENT '记录最后更新时间'
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci COMMENT='碳核算数据表';

-- --------------------------------------------------------

--
-- 表的结构 `fy_carbon_quota`
--

CREATE TABLE `fy_carbon_quota` (
  `uuid` char(36) NOT NULL COMMENT '碳排放UUID',
  `organize_uuid` char(36) NOT NULL COMMENT '组织用户UUID',
  `quota_year` int UNSIGNED NOT NULL COMMENT '配额年份，表示这个配额分配给企业的年份',
  `total_quota` decimal(10,0) NOT NULL COMMENT '总配额量，单位通常为吨CO2等价物。',
  `allocated_quota` decimal(10,0) NOT NULL COMMENT '已分配配额量，单位同上。初始时可能与总配额量相等，随后可能因为市场交易而变化。',
  `used_quota` decimal(10,0) NOT NULL DEFAULT '0' COMMENT '已使用配额量，表示企业实际消耗的碳配额。',
  `allocation_date` date DEFAULT NULL COMMENT '配额分配日期，记录企业配额分配的确切日期。',
  `compliance_status` tinyint(1) NOT NULL DEFAULT '0' COMMENT '合规状态，记录企业碳排放是否符合分配的配额。',
  `audit_log` json DEFAULT NULL COMMENT '审计日志，记录配额分配、使用和交易的详细情况，可用于审计和溯源。',
  `created_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
  `updated_at` timestamp NULL DEFAULT NULL COMMENT '修改日期'
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci COMMENT='碳排放配额';

-- --------------------------------------------------------

--
-- 表的结构 `fy_carbon_report`
--

CREATE TABLE `fy_carbon_report` (
  `id` bigint UNSIGNED NOT NULL COMMENT '碳排放报告唯一标识符，主键',
  `organize_uuid` char(36) NOT NULL COMMENT '企业唯一标识符，与企业信息表的organize_uuid字段关联',
  `accounting_period` varchar(17) NOT NULL COMMENT '报告涵盖的核算周期，通常为一个财年或特定时间段。(20230101-20230120)',
  `total_emission` decimal(10,0) NOT NULL COMMENT '报告周期内总碳排放量，单位可为吨CO2等价物。',
  `emission_reduction` decimal(10,0) NOT NULL COMMENT '报告周期内实现的碳减排量，单位同上。',
  `net_emission` decimal(10,0) NOT NULL COMMENT '净碳排放量，计算得出，= total_emission - emission_reduction',
  `report_status` varchar(14) NOT NULL DEFAULT 'draft' COMMENT '报告状态，可用值：''draft'', ''pending_review'', ''approved'', ''rejected''。',
  `verifier_uuid` char(36) DEFAULT NULL COMMENT '审核员的唯一标识符，与用户信息表关联。',
  `verification_date` date DEFAULT NULL COMMENT '审核日期。',
  `report_summary` text COMMENT '报告摘要，概述关键碳排放和减排信息。',
  `blockchain_tx_id` varchar(255) DEFAULT NULL COMMENT '报告铸造和上链后的区块链交易ID，用于追踪和验证。',
  `created_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '记录创建时间',
  `updated_at` timestamp NULL DEFAULT NULL COMMENT '修改时间'
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci COMMENT='碳排放报告数据表';

-- --------------------------------------------------------

--
-- 表的结构 `fy_carbon_trade`
--

CREATE TABLE `fy_carbon_trade` (
  `id` bigint UNSIGNED NOT NULL COMMENT '列表唯一标识符，主键。',
  `organize_uuid` char(36) NOT NULL COMMENT '发布交易的企业唯一标识符，与企业信息表的organize_uuid字段关联。',
  `quota_amount` decimal(10,0) NOT NULL COMMENT '出售的碳排放额度，单位通常为吨CO2等价物。',
  `price_per_unit` decimal(10,0) NOT NULL COMMENT '每单位碳排放额度的价格，可根据市场定价。',
<<<<<<< HEAD
  `status` varchar(9) NOT NULL DEFAULT 'active' COMMENT '发布状态，可用值：''active'', ''completed'', ''cancelled''。',
  `description` text NOT NULL COMMENT '交易详情描述，可以包含额外信息如碳排放额度的来源、有效期等。',
=======
  `status` varchar(9) CHARACTER SET utf8mb4 COLLATE utf8mb4_0900_ai_ci NOT NULL DEFAULT 'draft' COMMENT '发布状态，可用值：''draft,''active'', ''completed'', ''cancelled''。',
  `description` text NOT NULL COMMENT '交易详情描述，可以包含额外信息如碳排放额度的来源、有效期等。',
  `verify_uuid` char(36) NOT NULL COMMENT '验证人',
>>>>>>> 7af12f3 (Upload)
  `blockchain_tx_id` varchar(255) NOT NULL COMMENT '关联的区块链交易ID，用于在区块链上追踪具体的交易记录。',
  `created_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
  `updated_at` timestamp NULL DEFAULT NULL COMMENT '修改时间'
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci COMMENT='碳交易发布';

-- --------------------------------------------------------

--
-- 表的结构 `fy_invite`
--

CREATE TABLE `fy_invite` (
  `id` bigint UNSIGNED NOT NULL COMMENT '邀请主键',
  `uuid` char(36) NOT NULL COMMENT '用户外键',
  `code` char(10) NOT NULL COMMENT '邀请码',
  `created_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
  `updated_at` timestamp NULL DEFAULT NULL COMMENT '修改时间'
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci COMMENT='邀请';

-- --------------------------------------------------------

--
-- 表的结构 `fy_permission`
--

CREATE TABLE `fy_permission` (
  `pid` bigint UNSIGNED NOT NULL COMMENT '权限id',
  `name` varchar(50) NOT NULL COMMENT '权限名字',
  `description` varchar(100) DEFAULT NULL COMMENT '权限描述'
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci COMMENT='权限';

-- --------------------------------------------------------

--
-- 表的结构 `fy_role`
--

CREATE TABLE `fy_role` (
  `id` tinyint UNSIGNED NOT NULL COMMENT '列表id',
  `uuid` char(36) NOT NULL COMMENT '列表唯一识别码',
  `name` varchar(36) NOT NULL COMMENT '角色名字',
  `display_name` varchar(20) NOT NULL COMMENT '展示名字',
  `permission` json DEFAULT NULL COMMENT '角色权限',
  `created_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
  `updated_at` timestamp NULL DEFAULT NULL COMMENT '修改时间',
  `created_user` char(36) DEFAULT NULL COMMENT '创建用户uuid'
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci COMMENT='角色列表';

-- --------------------------------------------------------

--
-- 表的结构 `fy_user`
--

CREATE TABLE `fy_user` (
  `uid` bigint UNSIGNED NOT NULL COMMENT '账户序列',
  `uuid` char(36) NOT NULL COMMENT '用户唯一识别码',
  `user_name` varchar(40) NOT NULL COMMENT '用户名',
  `nick_name` varchar(40) DEFAULT NULL COMMENT '昵称',
  `real_name` varchar(40) NOT NULL COMMENT '真实信息',
  `email` varchar(100) NOT NULL COMMENT '邮箱',
  `phone` varchar(11) DEFAULT NULL COMMENT '手机号',
  `avatar` text COMMENT '头像',
  `password` varchar(255) NOT NULL COMMENT '密码',
  `role` char(36) NOT NULL COMMENT '权限组',
  `permission` json DEFAULT NULL COMMENT '附加权限',
  `created_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
  `updated_at` timestamp NULL DEFAULT NULL COMMENT '修改时间',
  `ban` tinyint(1) NOT NULL DEFAULT '0' COMMENT '账户封禁',
  `invite` char(10) DEFAULT NULL COMMENT '邀请码',
  `deleted_at` timestamp NULL DEFAULT NULL COMMENT '删除时间'
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci COMMENT='账户';

-- --------------------------------------------------------

--
-- 表的结构 `fy_user_ram`
--

CREATE TABLE `fy_user_ram` (
  `ruid` bigint UNSIGNED NOT NULL COMMENT '子用户主键',
  `uuid` char(36) NOT NULL COMMENT '主用户唯一识别码',
  `ruuid` char(36) NOT NULL COMMENT '子用户唯一识别码',
  `user_name` varchar(40) NOT NULL COMMENT '子用户名',
  `nick_name` varchar(40) DEFAULT NULL COMMENT '昵称',
  `real_name` varchar(4) DEFAULT NULL COMMENT '真实姓名',
  `email` varchar(100) NOT NULL COMMENT '邮箱',
  `phone` varchar(11) DEFAULT NULL COMMENT '手机号',
  `password` varchar(255) NOT NULL COMMENT '密码',
  `permission` json DEFAULT NULL COMMENT '权限（不可超过主用户权限）',
  `created_at` timestamp NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
  `updated_at` timestamp NULL DEFAULT NULL COMMENT '修改时间'
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci COMMENT='子用户';

-- --------------------------------------------------------

--
-- 表的结构 `fy_user_verify`
--

CREATE TABLE `fy_user_verify` (
  `id` bigint UNSIGNED NOT NULL COMMENT '主键',
  `uuid` char(36) NOT NULL COMMENT '用户uuid',
  `phone_verify` tinyint(1) NOT NULL DEFAULT '0' COMMENT '手机号校验',
  `email_verify` tinyint(1) NOT NULL DEFAULT '0' COMMENT '邮箱验证',
  `phone_verify_time` timestamp NULL DEFAULT NULL COMMENT '验证时间',
  `email_verify_time` timestamp NULL DEFAULT NULL COMMENT '邮箱验证时间'
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_0900_ai_ci COMMENT='账户校验';

--
-- 转储表的索引
--

--
-- 表的索引 `fy_approve_manage`
--
ALTER TABLE `fy_approve_manage`
  ADD PRIMARY KEY (`id`),
  ADD KEY `fy_approve_manage_fy_user_uuid_fk` (`account_uuid`),
  ADD KEY `fy_approve_manage_fy_user_uuid_fk_2` (`approve_uuid`);

--
-- 表的索引 `fy_approve_organize`
--
ALTER TABLE `fy_approve_organize`
  ADD PRIMARY KEY (`id`),
  ADD UNIQUE KEY `fy_approve_organize_account_uuid_uindex` (`account_uuid`),
  ADD UNIQUE KEY `fy_approve_organize_organize_credit_code_uindex` (`organize_credit_code`),
  ADD KEY `fy_approve_organize_fy_user_uuid_fk_2` (`approver_uuid`);

--
-- 表的索引 `fy_carbon_accounting`
--
ALTER TABLE `fy_carbon_accounting`
  ADD PRIMARY KEY (`id`),
  ADD KEY `fy_carbon_accounting_fy_user_uuid_fk` (`organize_uuid`),
  ADD KEY `fy_carbon_accounting_fy_carbon_report_id_fk` (`carbon_report_id`),
  ADD KEY `fy_carbon_accounting_fy_user_uuid_fk_2` (`verifier_uuid`);

--
-- 表的索引 `fy_carbon_quota`
--
ALTER TABLE `fy_carbon_quota`
  ADD PRIMARY KEY (`uuid`),
  ADD KEY `fy_carbon_quota_fy_user_uuid_fk` (`organize_uuid`);

--
-- 表的索引 `fy_carbon_report`
--
ALTER TABLE `fy_carbon_report`
  ADD PRIMARY KEY (`id`),
  ADD KEY `fy_carbon_report_fy_user_uuid_fk` (`organize_uuid`),
  ADD KEY `fy_carbon_report_fy_user_uuid_fk_2` (`verifier_uuid`);

--
-- 表的索引 `fy_carbon_trade`
--
ALTER TABLE `fy_carbon_trade`
  ADD PRIMARY KEY (`id`),
<<<<<<< HEAD
  ADD KEY `fy_carbon_trade_fy_user_uuid_fk` (`organize_uuid`);
=======
  ADD KEY `fy_carbon_trade_fy_user_uuid_fk` (`organize_uuid`),
  ADD KEY `fy_carbon_trade_fy_user_uuid_fk_2` (`verify_uuid`);
>>>>>>> 7af12f3 (Upload)

--
-- 表的索引 `fy_invite`
--
ALTER TABLE `fy_invite`
  ADD PRIMARY KEY (`id`),
  ADD UNIQUE KEY `fy_invite_code_uindex` (`code`),
  ADD KEY `fy_invite_fy_user_uuid_fk` (`uuid`);

--
-- 表的索引 `fy_permission`
--
ALTER TABLE `fy_permission`
  ADD PRIMARY KEY (`pid`),
  ADD UNIQUE KEY `fy_permission_name_uindex` (`name`);

--
-- 表的索引 `fy_role`
--
ALTER TABLE `fy_role`
  ADD PRIMARY KEY (`id`),
  ADD UNIQUE KEY `fy_role_uuid_uindex` (`uuid`),
  ADD KEY `fy_role_created_user_index` (`created_user`);

--
-- 表的索引 `fy_user`
--
ALTER TABLE `fy_user`
  ADD PRIMARY KEY (`uid`),
  ADD UNIQUE KEY `fy_user_email_uindex` (`email`),
  ADD UNIQUE KEY `fy_user_real_name_uindex` (`real_name`),
  ADD UNIQUE KEY `fy_user_user_name_uindex` (`user_name`),
  ADD UNIQUE KEY `fy_user_uuid_uindex` (`uuid`),
  ADD UNIQUE KEY `fy_user_phone_uindex` (`phone`),
  ADD KEY `fy_user_fy_invite_code_fk` (`invite`),
  ADD KEY `fy_user_fy_role_uuid_fk` (`role`);

--
-- 表的索引 `fy_user_ram`
--
ALTER TABLE `fy_user_ram`
  ADD PRIMARY KEY (`ruid`),
  ADD UNIQUE KEY `fy_user_ram_email_uindex` (`email`),
  ADD UNIQUE KEY `fy_user_ram_ruuid_uindex` (`ruuid`),
  ADD UNIQUE KEY `fy_user_ram_user_name_uindex` (`user_name`),
  ADD UNIQUE KEY `fy_user_ram_phone_uindex` (`phone`),
  ADD KEY `fy_user_ram_fy_user_uuid_fk` (`uuid`);

--
-- 表的索引 `fy_user_verify`
--
ALTER TABLE `fy_user_verify`
  ADD PRIMARY KEY (`id`),
  ADD KEY `fy_verify_fy_user_uuid_fk` (`uuid`);

--
-- 在导出的表使用AUTO_INCREMENT
--

--
-- 使用表AUTO_INCREMENT `fy_approve_manage`
--
ALTER TABLE `fy_approve_manage`
  MODIFY `id` bigint UNSIGNED NOT NULL AUTO_INCREMENT COMMENT '主键';

--
-- 使用表AUTO_INCREMENT `fy_approve_organize`
--
ALTER TABLE `fy_approve_organize`
  MODIFY `id` bigint UNSIGNED NOT NULL AUTO_INCREMENT COMMENT '主键ID';

--
-- 使用表AUTO_INCREMENT `fy_carbon_accounting`
--
ALTER TABLE `fy_carbon_accounting`
  MODIFY `id` bigint UNSIGNED NOT NULL AUTO_INCREMENT COMMENT '主键';

--
-- 使用表AUTO_INCREMENT `fy_carbon_report`
--
ALTER TABLE `fy_carbon_report`
  MODIFY `id` bigint UNSIGNED NOT NULL AUTO_INCREMENT COMMENT '碳排放报告唯一标识符，主键';

--
-- 使用表AUTO_INCREMENT `fy_carbon_trade`
--
ALTER TABLE `fy_carbon_trade`
  MODIFY `id` bigint UNSIGNED NOT NULL AUTO_INCREMENT COMMENT '列表唯一标识符，主键。';

--
-- 使用表AUTO_INCREMENT `fy_invite`
--
ALTER TABLE `fy_invite`
  MODIFY `id` bigint UNSIGNED NOT NULL AUTO_INCREMENT COMMENT '邀请主键';

--
-- 使用表AUTO_INCREMENT `fy_permission`
--
ALTER TABLE `fy_permission`
  MODIFY `pid` bigint UNSIGNED NOT NULL AUTO_INCREMENT COMMENT '权限id';

--
-- 使用表AUTO_INCREMENT `fy_role`
--
ALTER TABLE `fy_role`
  MODIFY `id` tinyint UNSIGNED NOT NULL AUTO_INCREMENT COMMENT '列表id';

--
-- 使用表AUTO_INCREMENT `fy_user`
--
ALTER TABLE `fy_user`
  MODIFY `uid` bigint UNSIGNED NOT NULL AUTO_INCREMENT COMMENT '账户序列';

--
-- 使用表AUTO_INCREMENT `fy_user_ram`
--
ALTER TABLE `fy_user_ram`
  MODIFY `ruid` bigint UNSIGNED NOT NULL AUTO_INCREMENT COMMENT '子用户主键';

--
-- 使用表AUTO_INCREMENT `fy_user_verify`
--
ALTER TABLE `fy_user_verify`
  MODIFY `id` bigint UNSIGNED NOT NULL AUTO_INCREMENT COMMENT '主键';

--
-- 限制导出的表
--

--
-- 限制表 `fy_approve_manage`
--
ALTER TABLE `fy_approve_manage`
  ADD CONSTRAINT `fy_approve_manage_fy_user_uuid_fk` FOREIGN KEY (`account_uuid`) REFERENCES `fy_user` (`uuid`) ON DELETE CASCADE ON UPDATE CASCADE,
  ADD CONSTRAINT `fy_approve_manage_fy_user_uuid_fk_2` FOREIGN KEY (`approve_uuid`) REFERENCES `fy_user` (`uuid`) ON UPDATE CASCADE;

--
-- 限制表 `fy_approve_organize`
--
ALTER TABLE `fy_approve_organize`
  ADD CONSTRAINT `fy_approve_organize_fy_user_uuid_fk` FOREIGN KEY (`account_uuid`) REFERENCES `fy_user` (`uuid`) ON DELETE CASCADE ON UPDATE CASCADE,
  ADD CONSTRAINT `fy_approve_organize_fy_user_uuid_fk_2` FOREIGN KEY (`approver_uuid`) REFERENCES `fy_user` (`uuid`) ON DELETE CASCADE ON UPDATE CASCADE;

--
-- 限制表 `fy_carbon_accounting`
--
ALTER TABLE `fy_carbon_accounting`
  ADD CONSTRAINT `fy_carbon_accounting_fy_carbon_report_id_fk` FOREIGN KEY (`carbon_report_id`) REFERENCES `fy_carbon_report` (`id`),
  ADD CONSTRAINT `fy_carbon_accounting_fy_user_uuid_fk` FOREIGN KEY (`organize_uuid`) REFERENCES `fy_user` (`uuid`) ON UPDATE CASCADE,
  ADD CONSTRAINT `fy_carbon_accounting_fy_user_uuid_fk_2` FOREIGN KEY (`verifier_uuid`) REFERENCES `fy_user` (`uuid`) ON UPDATE CASCADE;

--
-- 限制表 `fy_carbon_quota`
--
ALTER TABLE `fy_carbon_quota`
  ADD CONSTRAINT `fy_carbon_quota_fy_user_uuid_fk` FOREIGN KEY (`organize_uuid`) REFERENCES `fy_user` (`uuid`) ON DELETE CASCADE ON UPDATE CASCADE;

--
-- 限制表 `fy_carbon_report`
--
ALTER TABLE `fy_carbon_report`
  ADD CONSTRAINT `fy_carbon_report_fy_user_uuid_fk` FOREIGN KEY (`organize_uuid`) REFERENCES `fy_user` (`uuid`) ON UPDATE CASCADE,
  ADD CONSTRAINT `fy_carbon_report_fy_user_uuid_fk_2` FOREIGN KEY (`verifier_uuid`) REFERENCES `fy_user` (`uuid`) ON UPDATE CASCADE;

--
-- 限制表 `fy_carbon_trade`
--
ALTER TABLE `fy_carbon_trade`
<<<<<<< HEAD
  ADD CONSTRAINT `fy_carbon_trade_fy_user_uuid_fk` FOREIGN KEY (`organize_uuid`) REFERENCES `fy_user` (`uuid`) ON DELETE CASCADE ON UPDATE CASCADE;
=======
  ADD CONSTRAINT `fy_carbon_trade_fy_user_uuid_fk` FOREIGN KEY (`organize_uuid`) REFERENCES `fy_user` (`uuid`) ON DELETE CASCADE ON UPDATE CASCADE,
  ADD CONSTRAINT `fy_carbon_trade_fy_user_uuid_fk_2` FOREIGN KEY (`verify_uuid`) REFERENCES `fy_user` (`uuid`) ON UPDATE CASCADE;
>>>>>>> 7af12f3 (Upload)

--
-- 限制表 `fy_invite`
--
ALTER TABLE `fy_invite`
  ADD CONSTRAINT `fy_invite_fy_user_uuid_fk` FOREIGN KEY (`uuid`) REFERENCES `fy_user` (`uuid`) ON DELETE CASCADE ON UPDATE CASCADE;

--
-- 限制表 `fy_role`
--
ALTER TABLE `fy_role`
  ADD CONSTRAINT `fy_role_fy_user_uuid_fk` FOREIGN KEY (`created_user`) REFERENCES `fy_user` (`uuid`) ON DELETE CASCADE ON UPDATE CASCADE;

--
-- 限制表 `fy_user`
--
ALTER TABLE `fy_user`
  ADD CONSTRAINT `fy_user_fy_invite_code_fk` FOREIGN KEY (`invite`) REFERENCES `fy_invite` (`code`) ON DELETE CASCADE ON UPDATE CASCADE,
  ADD CONSTRAINT `fy_user_fy_role_uuid_fk` FOREIGN KEY (`role`) REFERENCES `fy_role` (`uuid`) ON UPDATE CASCADE;

--
-- 限制表 `fy_user_ram`
--
ALTER TABLE `fy_user_ram`
  ADD CONSTRAINT `fy_user_ram_fy_user_uuid_fk` FOREIGN KEY (`uuid`) REFERENCES `fy_user` (`uuid`) ON DELETE CASCADE ON UPDATE CASCADE;

--
-- 限制表 `fy_user_verify`
--
ALTER TABLE `fy_user_verify`
  ADD CONSTRAINT `fy_verify_fy_user_uuid_fk` FOREIGN KEY (`uuid`) REFERENCES `fy_user` (`uuid`) ON DELETE CASCADE ON UPDATE CASCADE;
COMMIT;

/*!40101 SET CHARACTER_SET_CLIENT=@OLD_CHARACTER_SET_CLIENT */;
/*!40101 SET CHARACTER_SET_RESULTS=@OLD_CHARACTER_SET_RESULTS */;
/*!40101 SET COLLATION_CONNECTION=@OLD_COLLATION_CONNECTION */;
<<<<<<< HEAD
=======

>>>>>>> 7af12f3 (Upload)
```

