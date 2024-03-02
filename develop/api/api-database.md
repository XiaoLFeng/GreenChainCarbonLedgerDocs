# 数据库文档

## fy_user

> 账户

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
| 10 | `role` | 权限组 | tinyint unsigned |  | NO |  | 1 |
| 11 | `permission` | 附加权限 | json |  | YES |  |  |
| 12 | `created_at` | 创建时间 | timestamp |  | NO | DEFAULT_GENERATED | CURRENT_TIMESTAMP |
| 13 | `updated_at` | 修改时间 | timestamp |  | YES |  |  |
| 14 | `ban` | 账户封禁 | tinyint(1) |  | NO |  | 0 |
| 15 | `invite` | 邀请码 | char(10) | MUL | YES |  |  |
| 16 | `deleted_at` | 删除时间 | timestamp |  | YES |  |  |

```mysql
-- auto-generated definition
create table fy_user
(
    uid        bigint unsigned auto_increment comment '账户序列'
        primary key,
    uuid       char(36)                                   not null comment '用户唯一识别码',
    user_name  varchar(40)                                not null comment '用户名',
    nick_name  varchar(40)                                null comment '昵称',
    real_name  varchar(40)                                not null comment '真实信息',
    email      varchar(100)                               not null comment '邮箱',
    phone      varchar(11)                                null comment '手机号',
    avatar     text                                       null comment '头像',
    password   varchar(255)                               not null comment '密码',
    role       tinyint unsigned default '1'               not null comment '权限组',
    permission json                                       null comment '附加权限',
    created_at timestamp        default CURRENT_TIMESTAMP not null comment '创建时间',
    updated_at timestamp                                  null comment '修改时间',
    ban        tinyint(1)       default 0                 not null comment '账户封禁',
    invite     char(10)                                   null comment '邀请码',
    deleted_at timestamp                                  null comment '删除时间',
    constraint fy_user_email_uindex
        unique (email),
    constraint fy_user_phone_uindex
        unique (phone),
    constraint fy_user_real_name_uindex
        unique (real_name),
    constraint fy_user_user_name_uindex
        unique (user_name),
    constraint fy_user_uuid_uindex
        unique (uuid),
    constraint fy_user_fy_invite_code_fk
        foreign key (invite) references fy_invite (code)
            on update cascade on delete cascade
)
    comment '账户';
```



## fy_invite

> 邀请

| 序号 | 名称 | 描述 | 类型 | 键 | 为空 | 额外 | 默认值 |
| :--: | :--: | :--: | :--: | :--: | :--: | :--: | :--: |
| 1 | `id` | 邀请主键 | bigint unsigned | PRI | NO | auto_increment |  |
| 2 | `uuid` | 用户外键 | char(36) | MUL | NO |  |  |
| 3 | `code` | 邀请码 | char(10) | UNI | NO |  |  |
| 4 | `created_at` | 创建时间 | timestamp |  | NO | DEFAULT_GENERATED | CURRENT_TIMESTAMP |
| 5 | `updated_at` | 修改时间 | timestamp |  | YES |  |  |

```mysql
-- auto-generated definition
create table fy_invite
(
    id         bigint unsigned auto_increment comment '邀请主键'
        primary key,
    uuid       char(36)                            not null comment '用户外键',
    code       char(10)                            not null comment '邀请码',
    created_at timestamp default CURRENT_TIMESTAMP not null comment '创建时间',
    updated_at timestamp                           null comment '修改时间',
    constraint fy_invite_code_uindex
        unique (code),
    constraint fy_invite_fy_user_uuid_fk
        foreign key (uuid) references fy_user (uuid)
            on update cascade on delete cascade
)
    comment '邀请';
```

----

# 数据库导入文件

> 为方便后期一件操作或恢复出厂，配置Mysql导入文件配置信息

```mysql
-- phpMyAdmin SQL Dump
-- version 5.2.1
-- https://www.phpmyadmin.net/
--
-- 主机： 172.17.0.3
-- 生成日期： 2024-03-02 08:30:47
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

--
-- 转存表中的数据 `fy_permission`
--

INSERT INTO `fy_permission` (`pid`, `name`, `description`) VALUES
(1, 'admin:resetUserPassword', '重置用户密码'),
(2, 'admin:resetUserRole', '重置用户角色'),
(3, 'admin:resetUserPermission', '重置用户权限');

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

--
-- 转存表中的数据 `fy_role`
--

INSERT INTO `fy_role` (`id`, `uuid`, `name`, `display_name`, `permission`, `created_at`, `updated_at`, `created_user`) VALUES
(1, '931e06fb-eb62-4883-8f22-db0f9da409be', 'default', '默认账户', NULL, '2024-03-01 16:22:21', NULL, NULL),
(2, '6a6f44cd-0932-4445-966a-3bbc400e5c41', 'organize', '组织账户', '[]', '2024-03-01 16:22:21', NULL, NULL),
(3, 'c356f874-ef22-4de2-b05b-f7a557132979', 'admin', '管理账户', '[]', '2024-03-01 16:22:21', NULL, NULL),
(4, 'a2992791-ab49-42ef-a559-a36d65943514', 'console', '超级管理员账户', '[\"admin:resetUserPassword\", \"admin:resetUserRole\", \"admin:resetUserPermission\"]', '2024-03-01 16:22:21', NULL, NULL);

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

--
-- 转存表中的数据 `fy_user`
--

INSERT INTO `fy_user` (`uid`, `uuid`, `user_name`, `nick_name`, `real_name`, `email`, `phone`, `avatar`, `password`, `role`, `permission`, `created_at`, `updated_at`, `ban`, `invite`, `deleted_at`) VALUES
(4, '5c9835e6-7599-43fd-b317-890083f07bb7', 'xiao_lfeng', NULL, '曾昶雯', 'lfengzeng@vip.qq.com', '13316569390', NULL, '$2a$10$O4l3ZHgioIi5kGTMMYTWx.whX99hu9uaAmL2eW8rxUswn43EEoG6C', 'c356f874-ef22-4de2-b05b-f7a557132979', NULL, '2024-03-01 08:23:04', NULL, 0, NULL, NULL);

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
-- 使用表AUTO_INCREMENT `fy_invite`
--
ALTER TABLE `fy_invite`
  MODIFY `id` bigint UNSIGNED NOT NULL AUTO_INCREMENT COMMENT '邀请主键';

--
-- 使用表AUTO_INCREMENT `fy_permission`
--
ALTER TABLE `fy_permission`
  MODIFY `pid` bigint UNSIGNED NOT NULL AUTO_INCREMENT COMMENT '权限id', AUTO_INCREMENT=4;

--
-- 使用表AUTO_INCREMENT `fy_role`
--
ALTER TABLE `fy_role`
  MODIFY `id` tinyint UNSIGNED NOT NULL AUTO_INCREMENT COMMENT '列表id', AUTO_INCREMENT=5;

--
-- 使用表AUTO_INCREMENT `fy_user`
--
ALTER TABLE `fy_user`
  MODIFY `uid` bigint UNSIGNED NOT NULL AUTO_INCREMENT COMMENT '账户序列', AUTO_INCREMENT=5;

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
```

