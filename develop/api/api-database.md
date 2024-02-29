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
```

