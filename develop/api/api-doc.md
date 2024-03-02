# GreenChainCarbonLedger

Base URLs:

* <a href="http://localhost:8081/api/v1">开发环境: http://localhost:8081/api/v1</a>

# Authentication

- HTTP Authentication, scheme: bearer

# AuthController

## POST 组织账号注册

POST /auth/organize/register

## 接口描述

该接口用于新用户的注册过程。用户需要提供完整的注册信息，包括姓名、电话号码、电子邮件地址以及密码。注册信息将通过接口提交，并进行相应的验证。

## 备注

- 组织名称需保证唯一性，以避免与现有组织冲突。
- 联系邮箱地址将用于验证和后续的通讯，因此需要确认其有效性。
- 密码应进行安全存储，建议采用加密方式（加密方式通过SHA-256后进行BCrypt）。

> Body Parameters

```json
{
  "organize": "string",
  "username": "string",
  "phone": "string",
  "email": "string",
  "code": "string",
  "invite": "string",
  "password": "string"
}
```

### Params

|Name|Location|Type|Required|Title|Description|
|---|---|---|---|---|---|
|X-Timestamp|header|integer| yes ||前端传递的时间戳|
|body|body|[AuthOrganizeRegisterVO1](#schemaauthorganizeregistervo1)| no | 组织用户注册VO|none|

> Response Examples

> 200 Response

```json
{
  "output": "string",
  "code": 0,
  "message": "string",
  "data": {
    "uuid": "string",
    "userName": "string",
    "realName": "string",
    "email": "string",
    "phone": "string"
  }
}
```

> 页面不存在

```json
{
  "output": "PageNotFounded",
  "code": 40401,
  "message": "页面不存在",
  "data": {
    "errorMessage": "页面 / 不存在"
  }
}
```

> 请求方法不支持

```json
{
  "output": "RequestMethodNotSupported",
  "code": 40500,
  "message": "请求方法不支持",
  "data": {
    "errorMessage": "请求方法 [POST] 不支持,受支持的请求方法为 [GET]"
  }
}
```

### Responses

|HTTP Status Code |Meaning|Description|Data schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|Inline|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|页面不存在|[BaseResponse](#schemabaseresponse)|
|405|[Method Not Allowed](https://tools.ietf.org/html/rfc7231#section-6.5.5)|请求方法不支持|[BaseResponse](#schemabaseresponse)|

### Responses Data Schema

HTTP Status Code **200**

|Name|Type|Required|Restrictions|Title|description|
|---|---|---|---|---|---|
|» output|string|true|none|状态名|英文状态描述|
|» code|integer|true|none|状态码|业务状态码（前三位为HTTP状态码）|
|» message|string|true|none|状态描述|对状态的中文描述|
|» data|[BackAuthRegisterVO](#schemabackauthregistervo)|true|none|数据|none|
|»» uuid|string|true|none|用户唯一识别码|none|
|»» userName|string|true|none|用户名|none|
|»» realName|string|true|none|真实信息|none|
|»» email|string|true|none|邮箱|none|
|»» phone|string|true|none|手机号|none|

## POST 管理账号注册

POST /auth/admin/register

## 接口描述

该接口用于管理账号的注册流程。管理员需要填写必要的信息，以建立新的管理账号。这包括管理员的姓名、联系方式、电子邮件地址和密码。提交的信息将经过验证，以确保其满足系统的安全性要求。成功注册后，管理员将获得访问对应管理功能的权限。此过程还将确保每个管理员账号的唯一性，并防止未授权的账号创建。

## 备注

- 管理员用户名应保证唯一性，避免与现有管理员用户名冲突。
- 联系邮箱不仅用作登录凭证的一部分，也用于接收系统通知和密码重置等操作，因此邮箱的有效性至关重要。
- 为了账号安全，密码在存储前应进行加密处理（加密方式通过SHA-256后进行BCrypt）。

> Body Parameters

```json
{
  "username": "易磊",
  "realname": "她持局单造",
  "phone": "18615059169",
  "email": "q.jpyzjvze@qq.com",
  "code": "58",
  "password": "tempor"
}
```

### Params

|Name|Location|Type|Required|Title|Description|
|---|---|---|---|---|---|
|X-Timestamp|header|integer| yes ||前端传递的时间戳|
|body|body|[AuthOrganizeRegisterVO](#schemaauthorganizeregistervo)| no | 管理用户注册VO|none|

> Response Examples

> 200 Response

```json
{
  "output": "string",
  "code": 0,
  "message": "string",
  "data": {
    "uuid": "string",
    "userName": "string",
    "realName": "string",
    "email": "string",
    "phone": "string"
  }
}
```

> 页面不存在

```json
{
  "output": "PageNotFounded",
  "code": 40401,
  "message": "页面不存在",
  "data": {
    "errorMessage": "页面 / 不存在"
  }
}
```

> 请求方法不支持

```json
{
  "output": "RequestMethodNotSupported",
  "code": 40500,
  "message": "请求方法不支持",
  "data": {
    "errorMessage": "请求方法 [POST] 不支持,受支持的请求方法为 [GET]"
  }
}
```

### Responses

|HTTP Status Code |Meaning|Description|Data schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|Inline|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|页面不存在|[BaseResponse](#schemabaseresponse)|
|405|[Method Not Allowed](https://tools.ietf.org/html/rfc7231#section-6.5.5)|请求方法不支持|[BaseResponse](#schemabaseresponse)|

### Responses Data Schema

HTTP Status Code **200**

|Name|Type|Required|Restrictions|Title|description|
|---|---|---|---|---|---|
|» output|string|true|none|状态名|英文状态描述|
|» code|integer|true|none|状态码|业务状态码（前三位为HTTP状态码）|
|» message|string|true|none|状态描述|对状态的中文描述|
|» data|[BackAuthRegisterVO](#schemabackauthregistervo)|true|none|数据|none|
|»» uuid|string|true|none|用户唯一识别码|none|
|»» userName|string|true|none|用户名|none|
|»» realName|string|true|none|真实信息|none|
|»» email|string|true|none|邮箱|none|
|»» phone|string|true|none|手机号|none|

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
|X-Timestamp|header|integer| yes ||前端传递的时间戳|
|body|body|[AuthLoginVO](#schemaauthloginvo)| no | 账户登陆VO|none|

> Response Examples

> 200 Response

```json
{
  "output": "string",
  "code": 0,
  "message": "string",
  "data": {
    "user": {
      "uuid": "string",
      "userName": "string",
      "realName": "string",
      "email": "string",
      "phone": "string"
    },
    "role": "string",
    "token": "string",
    "permission": {
      "rolePermission": [
        "string"
      ],
      "userPermission": [
        "string"
      ]
    },
    "recover": true
  }
}
```

> 用户不存在

```json
{
  "output": "UsernameNotExist",
  "code": 40304,
  "message": "用户不存在"
}
```

> 页面不存在

```json
{
  "output": "PageNotFounded",
  "code": 40401,
  "message": "页面不存在",
  "data": {
    "errorMessage": "页面 / 不存在"
  }
}
```

> 请求方法不支持

```json
{
  "output": "RequestMethodNotSupported",
  "code": 40500,
  "message": "请求方法不支持",
  "data": {
    "errorMessage": "请求方法 [POST] 不支持,受支持的请求方法为 [GET]"
  }
}
```

### Responses

|HTTP Status Code |Meaning|Description|Data schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|Inline|
|403|[Forbidden](https://tools.ietf.org/html/rfc7231#section-6.5.3)|用户不存在|[BaseResponse](#schemabaseresponse)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|页面不存在|[BaseResponse](#schemabaseresponse)|
|405|[Method Not Allowed](https://tools.ietf.org/html/rfc7231#section-6.5.5)|请求方法不支持|[BaseResponse](#schemabaseresponse)|

### Responses Data Schema

HTTP Status Code **200**

|Name|Type|Required|Restrictions|Title|description|
|---|---|---|---|---|---|
|» output|string|true|none|状态名|英文状态描述|
|» code|integer|true|none|状态码|业务状态码（前三位为HTTP状态码）|
|» message|string|true|none|状态描述|对状态的中文描述|
|» data|[BackAuthLoginVO](#schemabackauthloginvo)|true|none|数据|none|
|»» user|object|true|none||none|
|»»» uuid|string|true|none|用户唯一识别码|none|
|»»» userName|string|true|none|用户名|none|
|»»» realName|string|true|none|真实信息|none|
|»»» email|string|true|none|邮箱|none|
|»»» phone|string|true|none|手机号|none|
|»» role|string|true|none|角色组|none|
|»» token|string|true|none|用户登录验证令牌|none|
|»» permission|object|true|none||none|
|»»» rolePermission|[string]|true|none|角色权限组表|none|
|»»» userPermission|[string]|true|none|用户权限组表|none|
|»» recover|boolean¦null|true|none||none|

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
  "email": "string",
  "code": "string",
  "password": "string",
  "confirmPassword": "string"
}
```

### Params

|Name|Location|Type|Required|Title|Description|
|---|---|---|---|---|---|
|X-Timestamp|header|integer| yes ||前端传递的时间戳|
|body|body|[AuthForgetPasswordVO](#schemaauthforgetpasswordvo)| no | 账户忘记密码VO|none|

> Response Examples

> 200 Response

```json
{
  "output": "string",
  "code": 0,
  "message": "string",
  "data": {
    "output": "string",
    "code": 0,
    "message": "string",
    "data": "string"
  }
}
```

> 页面不存在

```json
{
  "output": "PageNotFounded",
  "code": 40401,
  "message": "页面不存在",
  "data": {
    "errorMessage": "页面 / 不存在"
  }
}
```

> 请求方法不支持

```json
{
  "output": "RequestMethodNotSupported",
  "code": 40500,
  "message": "请求方法不支持",
  "data": {
    "errorMessage": "请求方法 [POST] 不支持,受支持的请求方法为 [GET]"
  }
}
```

### Responses

|HTTP Status Code |Meaning|Description|Data schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|Inline|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|页面不存在|[BaseResponse](#schemabaseresponse)|
|405|[Method Not Allowed](https://tools.ietf.org/html/rfc7231#section-6.5.5)|请求方法不支持|[BaseResponse](#schemabaseresponse)|

### Responses Data Schema

HTTP Status Code **200**

|Name|Type|Required|Restrictions|Title|description|
|---|---|---|---|---|---|
|» output|string|true|none|状态名|英文状态描述|
|» code|integer|true|none|状态码|业务状态码（前三位为HTTP状态码）|
|» message|string|true|none|状态描述|对状态的中文描述|
|» data|[BaseResponse](#schemabaseresponse)|true|none|通用返回|none|
|»» output|string|false|none|状态名|英文状态描述|
|»» code|integer|false|none|状态码|业务状态码（前三位为HTTP状态码）|
|»» message|string|false|none|状态描述|对状态的中文描述|
|»» data|string|true|none||none|

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
|X-Timestamp|header|integer| yes ||前端传递的时间戳|
|X-Auth-UUID|header|string| yes ||用户的UUID|
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

> 页面不存在

```json
{
  "output": "PageNotFounded",
  "code": 40401,
  "message": "页面不存在",
  "data": {
    "errorMessage": "页面 / 不存在"
  }
}
```

> 请求方法不支持

```json
{
  "output": "RequestMethodNotSupported",
  "code": 40500,
  "message": "请求方法不支持",
  "data": {
    "errorMessage": "请求方法 [POST] 不支持,受支持的请求方法为 [GET]"
  }
}
```

### Responses

|HTTP Status Code |Meaning|Description|Data schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|[BaseResponse](#schemabaseresponse)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|页面不存在|[BaseResponse](#schemabaseresponse)|
|405|[Method Not Allowed](https://tools.ietf.org/html/rfc7231#section-6.5.5)|请求方法不支持|[BaseResponse](#schemabaseresponse)|

## DELETE 账号注销

DELETE /auth/delete

## 接口描述

此接口用于用户主动注销其账号。用户通过此操作可以永久删除其账户及所有相关数据（请注意，为了避免级联删除导致数据缺失导致数据不完整无法统计，故删除用户为软删除模式）。考虑到操作的不可逆性，接口设计应确保用户明确意愿，并可能需要二次验证用户身份以防止误操作。

## 备注

- 用户在执行注销前应被充分告知其账号和数据将被永久删除，且无法恢复。
- 建议在注销前提示用户备份任何重要数据。
- 可以设计为用户在注销前必须输入密码或进行其他形式的身份验证。
- 应提供一个合理的缓冲期，在此期间用户可以取消注销操作，以防止误操作。
- 注销操作一旦完成，用户的所有必要的隐私数据应从数据库和备份中删除，以符合隐私法规。

> Body Parameters

```json
{
  "password": "string",
  "code": "string"
}
```

### Params

|Name|Location|Type|Required|Title|Description|
|---|---|---|---|---|---|
|X-Timestamp|header|integer| yes ||前端传递的时间戳|
|X-Auth-UUID|header|string| yes ||用户的UUID|
|body|body|[AuthDeleteVO](#schemaauthdeletevo)| no | 账户删除VO|none|

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

> 页面不存在

```json
{
  "output": "PageNotFounded",
  "code": 40401,
  "message": "页面不存在",
  "data": {
    "errorMessage": "页面 / 不存在"
  }
}
```

> 请求方法不支持

```json
{
  "output": "RequestMethodNotSupported",
  "code": 40500,
  "message": "请求方法不支持",
  "data": {
    "errorMessage": "请求方法 [POST] 不支持,受支持的请求方法为 [GET]"
  }
}
```

### Responses

|HTTP Status Code |Meaning|Description|Data schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|[BaseResponse](#schemabaseresponse)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|页面不存在|[BaseResponse](#schemabaseresponse)|
|405|[Method Not Allowed](https://tools.ietf.org/html/rfc7231#section-6.5.5)|请求方法不支持|[BaseResponse](#schemabaseresponse)|

## GET 账户登出

GET /auth/logout

## 接口描述

此接口用于用户的账户登出操作，确保用户能够安全退出应用或网站。当用户调用此接口后，系统将清除用户的会话信息，从而结束用户的登录状态。

## 备注

- 在前端调用此接口前，应确保已经从用户设备中获取到了会话标识（已镫骨）。
- 调用此接口成功后，前端应清除本地存储的会话标识，并引导用户回到登录页面或首页。
- 后端需要对 Redis 进行账户清除工作，避免用户登出后仍然可以使用原有 UUID 与 Token 进行登陆操作

### Params

|Name|Location|Type|Required|Title|Description|
|---|---|---|---|---|---|
|X-Timestamp|header|integer| yes ||前端传递的时间戳|

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

> 页面不存在

```json
{
  "output": "PageNotFounded",
  "code": 40401,
  "message": "页面不存在",
  "data": {
    "errorMessage": "页面 / 不存在"
  }
}
```

> 请求方法不支持

```json
{
  "output": "RequestMethodNotSupported",
  "code": 40500,
  "message": "请求方法不支持",
  "data": {
    "errorMessage": "请求方法 [POST] 不支持,受支持的请求方法为 [GET]"
  }
}
```

### Responses

|HTTP Status Code |Meaning|Description|Data schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|[BaseResponse](#schemabaseresponse)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|页面不存在|[BaseResponse](#schemabaseresponse)|
|405|[Method Not Allowed](https://tools.ietf.org/html/rfc7231#section-6.5.5)|请求方法不支持|[BaseResponse](#schemabaseresponse)|

# RoleController

## GET 角色列表

GET /role/list

## 接口描述

此接口用于查询系统中定义的所有角色及其相关信息。角色通常用于定义用户在系统中的权限和访问级别。通过此接口，管理员可以获取一个角色的列表，包括每个角色的ID、名称和描述等信息，以便于进行角色分配和权限管理。

## 备注

- 此接口不涉及敏感操作，登录用户均可以对接口信息获取。
- 接口返回的角色列表应包括角色的所有基本信息，足够进行角色分配和管理决策。
- 在实际应用中，可能还需要考虑分页或过滤功能，以便于管理大量的角色。

### Params

|Name|Location|Type|Required|Title|Description|
|---|---|---|---|---|---|
|type|query|string| yes ||[search/available/all]|
|search|query|string| no ||当 type 为 search 生效，目的为模糊查找|
|limit|query|number| no ||单页限制个数（默认10个）「不可超过50」|
|page|query|number| no ||第几页|
|order|query|string| yes ||[asc/desc] 顺序/倒序|
|X-Timestamp|header|integer| yes ||前端传递的时间戳|

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

> 页面不存在

```json
{
  "output": "PageNotFounded",
  "code": 40401,
  "message": "页面不存在",
  "data": {
    "errorMessage": "页面 / 不存在"
  }
}
```

> 请求方法不支持

```json
{
  "output": "RequestMethodNotSupported",
  "code": 40500,
  "message": "请求方法不支持",
  "data": {
    "errorMessage": "请求方法 [POST] 不支持,受支持的请求方法为 [GET]"
  }
}
```

### Responses

|HTTP Status Code |Meaning|Description|Data schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|[BaseResponse](#schemabaseresponse)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|页面不存在|[BaseResponse](#schemabaseresponse)|
|405|[Method Not Allowed](https://tools.ietf.org/html/rfc7231#section-6.5.5)|请求方法不支持|[BaseResponse](#schemabaseresponse)|

# UserController

## GET 查询用户信息

GET /user/list

## 接口描述

该接口用于查询用户信息。通过指定的查询类型、搜索关键词、结果限制数量、页码及排序规则，可以灵活地检索用户数据。支持对用户列表进行全文搜索、获取未封禁或已封禁用户列表，以及获取当前可用用户列表等多种功能。

> 该接口返回的用户信息必须经过脱敏处理，不能够包含用户的敏感信息。返回的内容避免数据量过大，返回每个用户的基本信息不过多。
> 该接口仅管理员可用

## 备注

- 确保type参数正确无误，否则将无法正确返回查询结果。
- 对于search参数，如果没有提供或留空，则不会进行关键词搜索。
- limit参数如果设置得过高，可能会影响服务器的响应时间。
- 分页参数page是基于limit的结果数量进行计算的，确保按照实际需求和预期进行设置。
- 排序参数order应当基于可排序的字段，如用户ID、用户名或创建时间等。如果字段不支持排序，将返回错误信息。
- 在处理用户信息时，应当考虑隐私和数据保护法规，确保不泄露敏感信息。

## 管理员接口
是

### Params

|Name|Location|Type|Required|Title|Description|
|---|---|---|---|---|---|
|type|query|string| yes ||[search/unbanlist/banlist/available/all]|
|search|query|string| no ||当 type 为 search 生效，目的为模糊查找|
|limit|query|number| no ||单页限制个数（默认20个）「不可超过100」|
|page|query|number| no ||第几页|
|order|query|string| no ||[asc/desc] 顺序/倒序|
|X-Timestamp|header|integer| yes ||前端传递的时间戳|
|X-Auth-UUID|header|string| yes ||用户的UUID|

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

> 页面不存在

```json
{
  "output": "PageNotFounded",
  "code": 40401,
  "message": "页面不存在",
  "data": {
    "errorMessage": "页面 / 不存在"
  }
}
```

> 请求方法不支持

```json
{
  "output": "RequestMethodNotSupported",
  "code": 40500,
  "message": "请求方法不支持",
  "data": {
    "errorMessage": "请求方法 [POST] 不支持,受支持的请求方法为 [GET]"
  }
}
```

### Responses

|HTTP Status Code |Meaning|Description|Data schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|[BaseResponse](#schemabaseresponse)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|页面不存在|[BaseResponse](#schemabaseresponse)|
|405|[Method Not Allowed](https://tools.ietf.org/html/rfc7231#section-6.5.5)|请求方法不支持|[BaseResponse](#schemabaseresponse)|

## GET 查询当前用户信息

GET /user/current

## 接口描述

该接口提供当前登录用户的个人信息查询。用户在成功登录后，可以请求此接口来获取自己的账户详细信息，包括姓名、联系方式、电子邮件地址等。这通常用于个人资料页面，允许用户查看其信息。

## 备注

- 用户必须提供有效的令牌来验证其身份，令牌通常在用户登录时生成。
- 接口将仅返回请求用户自己的信息，不允许访问其他用户的信息。
- 确保返回的信息中不包含密码或其他敏感认证数据。
- 任何对个人信息的更新请求应通过单独的接口处理，该接口仅用于信息的读取。

### Params

|Name|Location|Type|Required|Title|Description|
|---|---|---|---|---|---|
|X-Timestamp|header|integer| yes ||前端传递的时间戳|
|X-Auth-UUID|header|string| yes ||用户的UUID|

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

> 页面不存在

```json
{
  "output": "PageNotFounded",
  "code": 40401,
  "message": "页面不存在",
  "data": {
    "errorMessage": "页面 / 不存在"
  }
}
```

> 请求方法不支持

```json
{
  "output": "RequestMethodNotSupported",
  "code": 40500,
  "message": "请求方法不支持",
  "data": {
    "errorMessage": "请求方法 [POST] 不支持,受支持的请求方法为 [GET]"
  }
}
```

### Responses

|HTTP Status Code |Meaning|Description|Data schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|[BaseResponse](#schemabaseresponse)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|页面不存在|[BaseResponse](#schemabaseresponse)|
|405|[Method Not Allowed](https://tools.ietf.org/html/rfc7231#section-6.5.5)|请求方法不支持|[BaseResponse](#schemabaseresponse)|

## PUT 修改账户

PUT /user/edit

## 接口描述

此接口用于用户修改自己的账户信息，包括用户名、邮箱和密码等。允许用户在登录状态下更新个人资料，以确保账户信息的最新性和安全性。

## 备注

- 用户身份的验证是通过 currentPassword 来实现的，确保修改请求的安全性。
- 在修改用户名或邮箱时，应检查新值是否已被其他账户使用，以保持唯一性。
- 更新密码时，应对新密码进行加密处理后存储。
- 修改操作成功后，建议发送一封确认邮件到用户的新邮箱地址（如果邮箱地址被修改），以验证新邮箱的有效性。

### Params

|Name|Location|Type|Required|Title|Description|
|---|---|---|---|---|---|
|X-Timestamp|header|integer| yes ||前端传递的时间戳|

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

> 页面不存在

```json
{
  "output": "PageNotFounded",
  "code": 40401,
  "message": "页面不存在",
  "data": {
    "errorMessage": "页面 / 不存在"
  }
}
```

> 请求方法不支持

```json
{
  "output": "RequestMethodNotSupported",
  "code": 40500,
  "message": "请求方法不支持",
  "data": {
    "errorMessage": "请求方法 [POST] 不支持,受支持的请求方法为 [GET]"
  }
}
```

### Responses

|HTTP Status Code |Meaning|Description|Data schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|[BaseResponse](#schemabaseresponse)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|页面不存在|[BaseResponse](#schemabaseresponse)|
|405|[Method Not Allowed](https://tools.ietf.org/html/rfc7231#section-6.5.5)|请求方法不支持|[BaseResponse](#schemabaseresponse)|

# AdminController

## POST 添加账户

POST /user/add

## 接口描述

此接口用于添加新的用户信息到系统中。通过此接口，可以将用户的基本信息注册到系统的数据库中，包括用户名、密码和邮箱等信息。

## 备注

- 确保用户名、邮箱、手机号是唯一的，不允许添加已存在的信息。
- 邮箱地址需要验证格式的正确性。
- 密码存储前需要进行加密处理（加密方式通过SHA-256后进行BCrypt）。

## 管理员标记
是

### Params

|Name|Location|Type|Required|Title|Description|
|---|---|---|---|---|---|
|X-Timestamp|header|integer| yes ||前端传递的时间戳|

> Response Examples

> 200 Response

```json
{}
```

> 页面不存在

```json
{
  "output": "PageNotFounded",
  "code": 40401,
  "message": "页面不存在",
  "data": {
    "errorMessage": "页面 / 不存在"
  }
}
```

> 请求方法不支持

```json
{
  "output": "RequestMethodNotSupported",
  "code": 40500,
  "message": "请求方法不支持",
  "data": {
    "errorMessage": "请求方法 [POST] 不支持,受支持的请求方法为 [GET]"
  }
}
```

### Responses

|HTTP Status Code |Meaning|Description|Data schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|Inline|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|页面不存在|[BaseResponse](#schemabaseresponse)|
|405|[Method Not Allowed](https://tools.ietf.org/html/rfc7231#section-6.5.5)|请求方法不支持|[BaseResponse](#schemabaseresponse)|

### Responses Data Schema

## PATCH 账户密码重置

PATCH /admin/user/reset/password

## 接口描述

此接口用于组织账户或管理员账户的密码。适用于用户忘记密码或需要出于安全考虑更换密码的情况。该操作通常需要用户通过注册时使用的邮箱接收的验证码进行验证，以确保操作的安全性。

## 备注

- 此操作具有较高的安全风险，应确保只有具备相应权限的管理员才能执行此操作。
- 执行密码重置操作前，建议进行必要的身份验证，以确保操作的合法性。
- 新密码应符合系统的密码安全策略，避免使用弱密码（需要自动生成，并且直接邮箱告知用户）。
- 为了用户账户的安全，建议在执行此操作后通知用户密码已被重置，并引导用户在下次登录时更改密码。

## 管理员标记
是

> Body Parameters

```json
{
  "uuid": "string"
}
```

### Params

|Name|Location|Type|Required|Title|Description|
|---|---|---|---|---|---|
|X-Timestamp|header|integer| yes ||前端传递的时间戳|
|X-Auth-UUID|header|string| yes ||用户的UUID|
|body|body|[AdminUserChangeVO](#schemaadminuserchangevo)| no | 管理员重置密码VO|none|

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

> 页面不存在

```json
{
  "output": "PageNotFounded",
  "code": 40401,
  "message": "页面不存在",
  "data": {
    "errorMessage": "页面 / 不存在"
  }
}
```

> 请求方法不支持

```json
{
  "output": "RequestMethodNotSupported",
  "code": 40500,
  "message": "请求方法不支持",
  "data": {
    "errorMessage": "请求方法 [POST] 不支持,受支持的请求方法为 [GET]"
  }
}
```

### Responses

|HTTP Status Code |Meaning|Description|Data schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|[BaseResponse](#schemabaseresponse)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|页面不存在|[BaseResponse](#schemabaseresponse)|
|405|[Method Not Allowed](https://tools.ietf.org/html/rfc7231#section-6.5.5)|请求方法不支持|[BaseResponse](#schemabaseresponse)|

## PUT 修改角色

PUT /role/edit/{roleUuid}

## 接口描述

此接口用于修改系统中已存在角色的属性，如角色名称、角色描述及其权限配置。它允许管理员或具有相应权限的用户更新角色信息，以适应组织结构或权限需求的变化。

## 备注

此接口需要调用者具有修改角色权限。
在修改权限配置时，应确保提供的权限标识符有效且存在。
修改角色信息可能会影响到依赖于这些角色的用户权限配置，操作前应进行充分的影响分析。

## 管理员标记
是

> Body Parameters

```json
{
  "name": "string",
  "displayName": "string",
  "permission": [
    0
  ]
}
```

### Params

|Name|Location|Type|Required|Title|Description|
|---|---|---|---|---|---|
|roleUuid|path|string| yes ||角色唯一序列号|
|X-Timestamp|header|integer| yes ||前端传递的时间戳|
|X-Auth-UUID|header|string| yes ||用户的UUID|
|body|body|[RoleEditVO](#schemaroleeditvo)| no | 编辑角色信息VO|none|

> Response Examples

> 200 Response

```json
{
  "output": "string",
  "code": 0,
  "message": "string",
  "data": {
    "uuid": "string",
    "name": "string",
    "displayName": "string",
    "permission": [
      "string"
    ]
  }
}
```

> 页面不存在

```json
{
  "output": "PageNotFounded",
  "code": 40401,
  "message": "页面不存在",
  "data": {
    "errorMessage": "页面 / 不存在"
  }
}
```

> 请求方法不支持

```json
{
  "output": "RequestMethodNotSupported",
  "code": 40500,
  "message": "请求方法不支持",
  "data": {
    "errorMessage": "请求方法 [POST] 不支持,受支持的请求方法为 [GET]"
  }
}
```

### Responses

|HTTP Status Code |Meaning|Description|Data schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|Inline|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|页面不存在|[BaseResponse](#schemabaseresponse)|
|405|[Method Not Allowed](https://tools.ietf.org/html/rfc7231#section-6.5.5)|请求方法不支持|[BaseResponse](#schemabaseresponse)|

### Responses Data Schema

HTTP Status Code **200**

|Name|Type|Required|Restrictions|Title|description|
|---|---|---|---|---|---|
|» output|string|true|none|状态名|英文状态描述|
|» code|integer|true|none|状态码|业务状态码（前三位为HTTP状态码）|
|» message|string|true|none|状态描述|对状态的中文描述|
|» data|[BackRoleVO](#schemabackrolevo)|true|none|数据|none|
|»» uuid|string|true|none|角色唯一识别码|none|
|»» name|string|true|none|角色名|none|
|»» displayName|string|true|none|角色名描述|none|
|»» permission|[string]|true|none|拥有权限|none|

# MailController

## POST 邮件发送

POST /mail/send/code

> Body Parameters

```json
{
  "email": "string",
  "template": "string"
}
```

### Params

|Name|Location|Type|Required|Title|Description|
|---|---|---|---|---|---|
|X-Timestamp|header|integer| yes ||前端传递的时间戳|
|body|body|[MailSendCodeVO](#schemamailsendcodevo)| no | 发送邮件VO|none|

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

> 页面不存在

```json
{
  "output": "PageNotFounded",
  "code": 40401,
  "message": "页面不存在",
  "data": {
    "errorMessage": "页面 / 不存在"
  }
}
```

> 请求方法不支持

```json
{
  "output": "RequestMethodNotSupported",
  "code": 40500,
  "message": "请求方法不支持",
  "data": {
    "errorMessage": "请求方法 [POST] 不支持,受支持的请求方法为 [GET]"
  }
}
```

### Responses

|HTTP Status Code |Meaning|Description|Data schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|[BaseResponse](#schemabaseresponse)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|页面不存在|[BaseResponse](#schemabaseresponse)|
|405|[Method Not Allowed](https://tools.ietf.org/html/rfc7231#section-6.5.5)|请求方法不支持|[BaseResponse](#schemabaseresponse)|

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

> 页面不存在

```json
{
  "output": "PageNotFounded",
  "code": 40401,
  "message": "页面不存在",
  "data": {
    "errorMessage": "页面 / 不存在"
  }
}
```

> 请求方法不支持

```json
{
  "output": "RequestMethodNotSupported",
  "code": 40500,
  "message": "请求方法不支持",
  "data": {
    "errorMessage": "请求方法 [POST] 不支持,受支持的请求方法为 [GET]"
  }
}
```

### Responses

|HTTP Status Code |Meaning|Description|Data schema|
|---|---|---|---|
|200|[OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)|成功|[BaseResponse](#schemabaseresponse)|
|404|[Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)|页面不存在|[BaseResponse](#schemabaseresponse)|
|405|[Method Not Allowed](https://tools.ietf.org/html/rfc7231#section-6.5.5)|请求方法不支持|[BaseResponse](#schemabaseresponse)|

# Data Schema

<h2 id="tocS_AdminUserChangeVO">AdminUserChangeVO</h2>

<a id="schemaadminuserchangevo"></a>
<a id="schema_AdminUserChangeVO"></a>
<a id="tocSadminuserchangevo"></a>
<a id="tocsadminuserchangevo"></a>

```json
{
  "uuid": "string"
}

```

管理员重置密码VO

### Attribute

|Name|Type|Required|Restrictions|Title|Description|
|---|---|---|---|---|---|
|uuid|string|true|none|用户唯一识别码|none|

<h2 id="tocS_MailSendCodeVO">MailSendCodeVO</h2>

<a id="schemamailsendcodevo"></a>
<a id="schema_MailSendCodeVO"></a>
<a id="tocSmailsendcodevo"></a>
<a id="tocsmailsendcodevo"></a>

```json
{
  "email": "string",
  "template": "string"
}

```

发送邮件VO

### Attribute

|Name|Type|Required|Restrictions|Title|Description|
|---|---|---|---|---|---|
|email|string|true|none|邮件|none|
|template|string|true|none|模板|none|

<h2 id="tocS_AuthDeleteVO">AuthDeleteVO</h2>

<a id="schemaauthdeletevo"></a>
<a id="schema_AuthDeleteVO"></a>
<a id="tocSauthdeletevo"></a>
<a id="tocsauthdeletevo"></a>

```json
{
  "password": "string",
  "code": "string"
}

```

账户删除VO

### Attribute

|Name|Type|Required|Restrictions|Title|Description|
|---|---|---|---|---|---|
|password|string|true|none|用户密码|none|
|code|string|true|none|邮箱验证码|none|

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

<h2 id="tocS_BackUserVO">BackUserVO</h2>

<a id="schemabackuservo"></a>
<a id="schema_BackUserVO"></a>
<a id="tocSbackuservo"></a>
<a id="tocsbackuservo"></a>

```json
{
  "uuid": "string",
  "userName": "string",
  "nickName": "string",
  "realName": "string",
  "email": "string",
  "phone": "string",
  "newPassword": "string",
  "createdAt": "string",
  "updatedAt": "string"
}

```

返回用户VO

### Attribute

|Name|Type|Required|Restrictions|Title|Description|
|---|---|---|---|---|---|
|uuid|string|true|none|用户唯一识别码|none|
|userName|string|true|none|用户名|none|
|nickName|string¦null|true|none|昵称|none|
|realName|string|true|none|真实信息|none|
|email|string|true|none|邮箱|none|
|phone|string¦null|true|none|手机号|none|
|newPassword|string¦null|true|none|新密码|none|
|createdAt|string|true|none|创建时间|none|
|updatedAt|string|true|none|修改时间|none|

<h2 id="tocS_AuthForgetPasswordVO">AuthForgetPasswordVO</h2>

<a id="schemaauthforgetpasswordvo"></a>
<a id="schema_AuthForgetPasswordVO"></a>
<a id="tocSauthforgetpasswordvo"></a>
<a id="tocsauthforgetpasswordvo"></a>

```json
{
  "email": "string",
  "code": "string",
  "password": "string",
  "confirmPassword": "string"
}

```

账户忘记密码VO

### Attribute

|Name|Type|Required|Restrictions|Title|Description|
|---|---|---|---|---|---|
|email|string|true|none|邮箱|none|
|code|string|true|none|校验码|none|
|password|string|true|none|密码|none|
|confirmPassword|string|true|none|确认密码|none|

<h2 id="tocS_RoleEditVO">RoleEditVO</h2>

<a id="schemaroleeditvo"></a>
<a id="schema_RoleEditVO"></a>
<a id="tocSroleeditvo"></a>
<a id="tocsroleeditvo"></a>

```json
{
  "name": "string",
  "displayName": "string",
  "permission": [
    0
  ]
}

```

编辑角色信息VO

### Attribute

|Name|Type|Required|Restrictions|Title|Description|
|---|---|---|---|---|---|
|name|string|true|none|角色名|none|
|displayName|string|true|none|角色名描述|none|
|permission|[integer]|true|none|拥有权限|none|

<h2 id="tocS_BackRoleVO">BackRoleVO</h2>

<a id="schemabackrolevo"></a>
<a id="schema_BackRoleVO"></a>
<a id="tocSbackrolevo"></a>
<a id="tocsbackrolevo"></a>

```json
{
  "uuid": "string",
  "name": "string",
  "displayName": "string",
  "permission": [
    "string"
  ]
}

```

返回角色信息VO

### Attribute

|Name|Type|Required|Restrictions|Title|Description|
|---|---|---|---|---|---|
|uuid|string|true|none|角色唯一识别码|none|
|name|string|true|none|角色名|none|
|displayName|string|true|none|角色名描述|none|
|permission|[string]|true|none|拥有权限|none|

<h2 id="tocS_AuthLoginVO">AuthLoginVO</h2>

<a id="schemaauthloginvo"></a>
<a id="schema_AuthLoginVO"></a>
<a id="tocSauthloginvo"></a>
<a id="tocsauthloginvo"></a>

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

<h2 id="tocS_BackAuthRegisterVO">BackAuthRegisterVO</h2>

<a id="schemabackauthregistervo"></a>
<a id="schema_BackAuthRegisterVO"></a>
<a id="tocSbackauthregistervo"></a>
<a id="tocsbackauthregistervo"></a>

```json
{
  "uuid": "string",
  "userName": "string",
  "realName": "string",
  "email": "string",
  "phone": "string"
}

```

账户注册内容返回VO

### Attribute

|Name|Type|Required|Restrictions|Title|Description|
|---|---|---|---|---|---|
|uuid|string|true|none|用户唯一识别码|none|
|userName|string|true|none|用户名|none|
|realName|string|true|none|真实信息|none|
|email|string|true|none|邮箱|none|
|phone|string|true|none|手机号|none|

<h2 id="tocS_AuthOrganizeRegisterVO">AuthOrganizeRegisterVO</h2>

<a id="schemaauthorganizeregistervo"></a>
<a id="schema_AuthOrganizeRegisterVO"></a>
<a id="tocSauthorganizeregistervo"></a>
<a id="tocsauthorganizeregistervo"></a>

```json
{
  "username": "string",
  "realname": "string",
  "phone": "string",
  "email": "string",
  "code": "string",
  "password": "string"
}

```

管理用户注册VO

### Attribute

|Name|Type|Required|Restrictions|Title|Description|
|---|---|---|---|---|---|
|username|string|true|none|管理员用户名|none|
|realname|string|true|none|真实名字|none|
|phone|string¦null|true|none|手机号|none|
|email|string|true|none|邮箱|none|
|code|string|true|none|验证码|none|
|password|string|true|none|密码|none|

<h2 id="tocS_BackAuthLoginVO">BackAuthLoginVO</h2>

<a id="schemabackauthloginvo"></a>
<a id="schema_BackAuthLoginVO"></a>
<a id="tocSbackauthloginvo"></a>
<a id="tocsbackauthloginvo"></a>

```json
{
  "user": {
    "uuid": "string",
    "userName": "string",
    "realName": "string",
    "email": "string",
    "phone": "string"
  },
  "role": "string",
  "token": "string",
  "permission": {
    "rolePermission": [
      "string"
    ],
    "userPermission": [
      "string"
    ]
  },
  "recover": true
}

```

账户登录内容返回VO

### Attribute

|Name|Type|Required|Restrictions|Title|Description|
|---|---|---|---|---|---|
|user|object|true|none||none|
|» uuid|string|true|none|用户唯一识别码|none|
|» userName|string|true|none|用户名|none|
|» realName|string|true|none|真实信息|none|
|» email|string|true|none|邮箱|none|
|» phone|string|true|none|手机号|none|
|role|string|true|none|角色组|none|
|token|string|true|none|用户登录验证令牌|none|
|permission|object|true|none||none|
|» rolePermission|[string]|true|none|角色权限组表|none|
|» userPermission|[string]|true|none|用户权限组表|none|
|recover|boolean¦null|true|none||none|

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

<h2 id="tocS_AuthOrganizeRegisterVO1">AuthOrganizeRegisterVO1</h2>

<a id="schemaauthorganizeregistervo1"></a>
<a id="schema_AuthOrganizeRegisterVO1"></a>
<a id="tocSauthorganizeregistervo1"></a>
<a id="tocsauthorganizeregistervo1"></a>

```json
{
  "organize": "string",
  "username": "string",
  "phone": "string",
  "email": "string",
  "code": "string",
  "invite": "string",
  "password": "string"
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
|password|string|true|none|密码|none|

