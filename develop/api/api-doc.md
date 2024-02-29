# GreenChainCarbonLedger

Base URLs:

* <a href="http://localhost:8081/api/v1">开发环境: http://localhost:8081/api/v1</a>

# Authentication

# AuthController

## POST 管理账号注册

POST /auth/organize/register

## 接口描述

该接口用于管理账号的注册流程。管理员需要填写必要的信息，以建立新的管理账号。这包括管理员的姓名、联系方式、电子邮件地址和密码。提交的信息将经过验证，以确保其满足系统的安全性要求。成功注册后，管理员将获得访问对应管理功能的权限。此过程还将确保每个管理员账号的唯一性，并防止未授权的账号创建。

> Body Parameters

```json
{
  "organize": "string",
  "realname": "string",
  "phone": "string",
  "email": "string",
  "code": "string"
}
```

### Params

|Name|Location|Type|Required|Title|Description|
|---|---|---|---|---|---|
|X-Timestamp|header|integer| yes ||none|
|body|body|[UserOrganizeRegisterVO](#schemauserorganizeregistervo)| no | 管理用户注册VO|none|

> Response Examples

> 200 Response

```json
{
  "output": "string",
  "code": 0,
  "message": "string",
  "data": "string"
}
```

### Responses

|HTTP Status Code |Meaning|Description|Data schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|[BaseResponse](#schemabaseresponse)|

## POST 账户登陆

POST /auth/login

## 接口描述
该接口用于账户登录。用户需要提供其注册账户时设置的电子邮件地址、手机号、和密码。系统将验证提交的凭据是否与现有用户记录匹配。如果认证成功，用户将获得对系统的访问权限，并返回一个会话令牌用于维持登录状态。如果认证失败，系统将返回错误信息。

> Body Parameters

```json
{
  "user": "string",
  "password": "string"
}
```

### Params

|Name|Location|Type|Required|Title|Description|
|---|---|---|---|---|---|
|X-Timestamp|header|integer| yes ||none|
|body|body|[UserLoginVO](#schemauserloginvo)| no | 账户登陆VO|none|

> Response Examples

> 200 Response

```json
{}
```

### Responses

|HTTP Status Code |Meaning|Description|Data schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|Inline|

### Responses Data Schema

## PUT 忘记密码

PUT /auth/forget

## 接口描述
该接口用于用户在忘记密码时重置密码。用户需要提供注册时使用的电子邮件地址。系统将验证电子邮件地址，并向其发送一个密码重置链接或验证码。用户通过点击链接或输入验证码来设置新密码，完成密码的重置过程。

## 备注
出于安全考虑，即使输入了不存在的电子邮件地址，系统也会返回“密码重置邮件已发送”的信息，以防止恶意用户试图找出有效的电子邮件账户。如果用户在规定时间内未收到邮件，建议检查垃圾邮件文件夹或重新尝试密码找回操作。

## 是否需要邮件通知
是

> Body Parameters

```json
{
  "email": "string"
}
```

### Params

|Name|Location|Type|Required|Title|Description|
|---|---|---|---|---|---|
|X-Timestamp|header|integer| yes ||none|
|body|body|[UserForgetPasswordVO](#schemauserforgetpasswordvo)| no | 账户忘记密码VO|none|

> Response Examples

> 200 Response

```json
{
  "output": "string",
  "code": 0,
  "message": "string",
  "data": "string"
}
```

### Responses

|HTTP Status Code |Meaning|Description|Data schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|[BaseResponse](#schemabaseresponse)|

## PATCH 修改密码

PATCH /auth/change

## 接口描述
此接口用于已注册用户修改当前密码。用户需通过验证流程后，才能更改其密码。通常这需要用户先登录账户，然后提交当前密码和新密码信息。为保障账户安全，系统将验证用户的当前密码是否正确，且新密码是否满足安全性要求。

## 备注
用户在设置新密码时，应避免使用易于猜测的密码，且新密码不应与前几次使用的密码相同。如果用户尝试使用与当前密码相同的密码作为新密码，系统应返回错误提示。

## 是否需要邮件通知
是

> Body Parameters

```json
{
  "currentPassword": "string",
  "newPassword": "string",
  "newPasswordConfirm": "string"
}
```

### Params

|Name|Location|Type|Required|Title|Description|
|---|---|---|---|---|---|
|X-Timestamp|header|integer| yes ||none|
|body|body|[AuthChangePasswordVO](#schemaauthchangepasswordvo)| no | 账户修改密码VO|none|

> Response Examples

> 200 Response

```json
{
  "output": "string",
  "code": 0,
  "message": "string",
  "data": "string"
}
```

### Responses

|HTTP Status Code |Meaning|Description|Data schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|[BaseResponse](#schemabaseresponse)|

# 信息

## GET 状态查询

GET /info

## 接口描述
该接口用于对服务状态业务的查询，用于检查项目的构建日期等信息。作为自动部署的信息查询

> Response Examples

> 成功

```json
{
  "output": "Success",
  "code": 200,
  "message": "欢迎使用 GreenChainCarbonLedger 系统，当您看到此状态时系统正常运行中",
  "data": {
    "kotlinVersion": "1.9.22",
    "buildTime": "2024-02-26 22:27:25",
    "javaVersion": "17.0.9",
    "version": "1.0.0-SNAPSHOT"
  }
}
```

### Responses

|HTTP Status Code |Meaning|Description|Data schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|[BaseResponse](#schemabaseresponse)|

# Data Schema

<h2 id="tocS_AuthChangePasswordVO">AuthChangePasswordVO</h2>

<a id="schemaauthchangepasswordvo"></a>
<a id="schema_AuthChangePasswordVO"></a>
<a id="tocSauthchangepasswordvo"></a>
<a id="tocsauthchangepasswordvo"></a>

```json
{
  "currentPassword": "string",
  "newPassword": "string",
  "newPasswordConfirm": "string"
}

```

账户修改密码VO

### Attribute

|Name|Type|Required|Restrictions|Title|Description|
|---|---|---|---|---|---|
|currentPassword|string|true|none|当前密码|none|
|newPassword|string|true|none|新密码|none|
|newPasswordConfirm|string|true|none|请在输入一次|none|

<h2 id="tocS_UserForgetPasswordVO">UserForgetPasswordVO</h2>

<a id="schemauserforgetpasswordvo"></a>
<a id="schema_UserForgetPasswordVO"></a>
<a id="tocSuserforgetpasswordvo"></a>
<a id="tocsuserforgetpasswordvo"></a>

```json
{
  "email": "string"
}

```

账户忘记密码VO

### Attribute

|Name|Type|Required|Restrictions|Title|Description|
|---|---|---|---|---|---|
|email|string|true|none|邮箱|none|

<h2 id="tocS_UserLoginVO">UserLoginVO</h2>

<a id="schemauserloginvo"></a>
<a id="schema_UserLoginVO"></a>
<a id="tocSuserloginvo"></a>
<a id="tocsuserloginvo"></a>

```json
{
  "user": "string",
  "password": "string"
}

```

账户登陆VO

### Attribute

|Name|Type|Required|Restrictions|Title|Description|
|---|---|---|---|---|---|
|user|string|true|none|用户名|允许用户名、邮箱、手机号登陆|
|password|string|true|none|密码|用户登陆密码|

<h2 id="tocS_UserOrganizeRegisterVO">UserOrganizeRegisterVO</h2>

<a id="schemauserorganizeregistervo"></a>
<a id="schema_UserOrganizeRegisterVO"></a>
<a id="tocSuserorganizeregistervo"></a>
<a id="tocsuserorganizeregistervo"></a>

```json
{
  "organize": "string",
  "realname": "string",
  "phone": "string",
  "email": "string",
  "code": "string"
}

```

管理用户注册VO

### Attribute

|Name|Type|Required|Restrictions|Title|Description|
|---|---|---|---|---|---|
|organize|string|true|none|管理员用户名|none|
|realname|string|true|none|真实名字|none|
|phone|string¦null|true|none|手机号|none|
|email|string|true|none|邮箱|none|
|code|string|true|none|验证码|none|

<h2 id="tocS_UserDO">UserDO</h2>

<a id="schemauserdo"></a>
<a id="schema_UserDO"></a>
<a id="tocSuserdo"></a>
<a id="tocsuserdo"></a>

```json
{
  "uid": 0,
  "uuid": "string",
  "userName": "string",
  "nickName": "string",
  "realName": "string",
  "email": "string",
  "phone": "string",
  "avatar": "string",
  "password": "string",
  "role": "string",
  "permission": "string",
  "created_at": "string",
  "updated_at": "string",
  "ban": true,
  "deleted_at": "string"
}

```

### Attribute

|Name|Type|Required|Restrictions|Title|Description|
|---|---|---|---|---|---|
|uid|number¦null|true|none|账户序列|none|
|uuid|string|true|none|用户唯一识别码|none|
|userName|string|true|none|用户名|none|
|nickName|string¦null|true|none|昵称|none|
|realName|string|true|none|真实信息|none|
|email|string|true|none|邮箱|none|
|phone|string¦null|true|none|手机号|none|
|avatar|string¦null|true|none|头像|none|
|password|string|true|none|密码|none|
|role|string|true|none|权限组|none|
|permission|string¦null|true|none|附加权限|none|
|created_at|string|true|none|创建时间|none|
|updated_at|string¦null|true|none|修改时间|none|
|ban|boolean|true|none|账户封禁|none|
|deleted_at|string¦null|true|none|删除时间|none|

<h2 id="tocS_BaseResponse">BaseResponse</h2>

<a id="schemabaseresponse"></a>
<a id="schema_BaseResponse"></a>
<a id="tocSbaseresponse"></a>
<a id="tocsbaseresponse"></a>

```json
{
  "output": "string",
  "code": 0,
  "message": "string",
  "data": "string"
}

```

通用返回

### Attribute

|Name|Type|Required|Restrictions|Title|Description|
|---|---|---|---|---|---|
|output|string|true|none|状态名|英文状态描述|
|code|integer|true|none|状态码|业务状态码（前三位为HTTP状态码）|
|message|string|true|none|状态描述|对状态的中文描述|
|data|string|true|none||none|

<h2 id="tocS_UserOrganizeRegisterVO1">UserOrganizeRegisterVO1</h2>

<a id="schemauserorganizeregistervo1"></a>
<a id="schema_UserOrganizeRegisterVO1"></a>
<a id="tocSuserorganizeregistervo1"></a>
<a id="tocsuserorganizeregistervo1"></a>

```json
{
  "organize": "string",
  "username": "string",
  "phone": "string",
  "email": "string",
  "code": "string",
  "invite": "string"
}

```

组织用户注册VO

### Attribute

|Name|Type|Required|Restrictions|Title|Description|
|---|---|---|---|---|---|
|organize|string|true|none|企业名字|none|
|username|string|true|none|用户名|none|
|phone|string¦null|true|none|手机号|none|
|email|string|true|none|邮箱|none|
|code|string|true|none|验证码|none|
|invite|string¦null|true|none|邀请码|none|

