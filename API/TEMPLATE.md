# API 模板文档

## 说明

这是 API 文档模板。使用此模板创建新的 API 文档时，请严格遵守以下结构和格式。

## 结构

- **注意事项**
- **权限要求**
  - **必要权限**
    - 模板说明
    - 模板示例
  - **可选权限**
    - 模板说明
    - 模板示例
- **接口信息**
  - 模板说明
  - 模板示例
- **接口请求**
  - 模板说明
  - 模板示例
- **接口响应**
  - 模板说明
  - 模板示例
- **错误码**
  - 模板说明
  - 模板示例
- **排查思路**
  - 模板说明
  - 模板示例
- **相关链接**
  - 模板说明
  - 模板示例

## 注意事项

### 模板说明

此处说明该接口的使用场景、注意事项等重要信息，特别是：

- 用户身份（user_access_token）调用时的过滤行为
- 应用身份（tenant_access_token）调用时的过滤行为
- 特殊字段的返回条件

### 模板示例

```markdown
## 注意事项

- 使用用户身份（user_access_token）调用该接口时，接口将根据该用户的组织架构可见范围进行过滤，仅返回组织架构可见范围内的用户数据。
- 使用应用身份（tenant_access_token）调用该接口时，接口将根据应用的通讯录权限范围进行过滤。如果请求的部门 ID 为 0（即根部门），则接口会校验应用是否具有全员的通讯录权限；如果请求的是非 0 的部门 ID，则会校验应用是否具有该部门的通讯录权限。无权限时，接口会返回无权限的报错信息；有权限则返回对应部门下的直属用户列表。
- 使用应用身份（tenant_access_token）调用本接口时，响应结果中不会返回部门路径字段（department_path）。如需获取部门路径字段值，请为应用申请 **获取成员所在部门路径（contact:user.department_path:readonly）** API 权限，并使用用户身份（user_access_token）调用接口。

关于用户组织架构可见范围和通讯录权限范围的更多信息，可参见[权限范围资源介绍](https://open.feishu.cn/document/ukTMukTMukTM/uETNz4SM1MjLxUzM/v3/guides/scope_authority)。
```

## 权限要求

### 必要权限

#### 模板说明

调用该 API **必须开启**的权限。开启其中任意一项权限即可调用该接口。

权限类型通常为：
- `应用权限（开启任一即可）` - 应用需要配置的权限

#### 模板示例

```markdown
### 必要权限

| 类型 | 名称 |
|------|------|
| 应用权限（开启任一即可） | 获取通讯录基本信息 (contact:contact.base:readonly) |
| 应用权限（开启任一即可） | 获取通讯录部门组织架构信息 (contact:department.organize:readonly) |
| 应用权限（开启任一即可） | 以应用身份访问通讯录 (contact:contact:access_as_app) |
| 应用权限（开启任一即可） | 读取通讯录 (contact:contact:readonly) |
| 应用权限（开启任一即可） | 以应用身份读取通讯录 (contact:contact:readonly_as_app) |
```

### 可选权限

#### 模板说明

敏感字段的权限要求。如果无需获取这些敏感字段，则不需要申请这些权限。

权限类型通常为：
- `字段权限（敏感字段）` - 敏感字段需要的权限

#### 模板示例

```markdown
### 可选权限

| 类型 | 名称 |
|------|------|
| 字段权限（敏感字段） | 统一用户标识 (contact:user.base:readonly) |
| 字段权限（敏感字段） | 获取用户 user ID (contact:user.employee_id:readonly) |
| 字段权限（敏感字段） | 应用内用户标识 (contact:user.base:readonly) |
| 字段权限（敏感字段） | 获取用户基本信息 (contact:user.base:readonly) |
| 字段权限（敏感字段） | 获取用户邮箱信息 (contact:user.email:readonly) |
| 字段权限（敏感字段） | 获取用户手机号 (contact:user.phone:readonly) |
| 字段权限（敏感字段） | 获取用户性别 (contact:user.gender:readonly) |
| 字段权限（敏感字段） | 获取用户受雇信息 (contact:user.employee:readonly) |
| 字段权限（敏感字段） | 获取用户组织架构信息 (contact:user.department:readonly) |
| 字段权限（敏感字段） | 查看成员工号 (contact:user.employee_number:read) |
| 字段权限（敏感字段） | 查看成员数据驻留地 (contact:user.user_geo) |
| 字段权限（敏感字段） | 查询用户职级 (contact:user.job_level:readonly) |
| 字段权限（敏感字段） | 查询用户所属的工作序列 (contact:user.job_family:readonly) |
| 字段权限（敏感字段） | 获取成员所在部门路径 (contact:user.department_path:readonly) |
| 字段权限（敏感字段） | 查看成员的虚线上级 ID (contact:user.dotted_line_leader_info.read) |
```

```markdown
> **说明**：敏感字段仅在开启对应权限后才会返回；如无需获取这些字段，不建议申请。
```

## 接口信息

### 模板说明

接口信息表格展示接口的基本信息，包括：

- **API 路径**：接口的完整 URL
- **请求方法**：GET/POST/PUT/DELETE 等
- **调用频率限制**：每分钟/每秒的调用次数限制
- **支持的应用类型**：Custom App 或 Store App
- **文档地址**：飞书开放平台的文档链接

### 模板示例

```markdown
## 接口信息

| API 路径 | `https://open.feishu.cn/open-apis/...` |
|----------|----------------------------------------|
| 请求方法 | GET |
| 调用频率限制 | 1000 次/分钟、50 次/秒 |
| 支持的应用类型 | Custom App、Store App |
| 文档地址 | [飞书开放平台](https://open.feishu.cn/document/...) |
```

## 接口请求

### 模板说明

接口请求章节包含：

1. **请求头** - HTTP 请求头字段
2. **请求参数** - URL 查询参数或路径参数
3. **请求体** - POST/PUT 请求的 JSON body
4. **请求示例** - 代码示例（Go/Java 为例）

### 模板示例

#### 请求头示例

```markdown
### 请求头

| 名称 | 类型 | 必填 | 描述 |
|------|------|------|------|
| `Authorization` | string | 是 | `tenant_access_token` 或 `user_access_token`<br>值格式："Bearer `access_token`"<br>示例值："Bearer u-7f1bcd13fc57d46bac21793a18e560"<br>**了解更多**：[如何选择与获取 access token](https://open.feishu.cn/document/...) |
| `Content-Type` | string | 是 | 固定值："application/json; charset=utf-8" |
```

#### 请求参数示例

```markdown
### 请求参数

| 参数名 | 类型 | 必填 | 描述 |
|--------|------|------|------|
| `param_name` | string | 否 | 参数说明<br>可选值：<br>- `open_id`：标识一个用户在某个应用中的身份<br>- `union_id`：标识一个用户在某个应用开发商下的身份<br>- `user_id`：标识一个用户在某个租户内的身份<br>默认值：`open_id`<br>**权限要求**：当值为 `user_id` 时，需要获取用户 user ID (contact:user.employee_id:readonly) |
```

#### 请求体示例

```markdown
### 请求体

无请求体（GET 请求）
```

或者：

```markdown
### 请求体

```json
{
    "field1": "value1",
    "field2": "value2"
}
```
```

#### 请求示例示例

```markdown
### 请求示例

#### Go 请求示例

```go
import (
	"context"

	"github.com/larksuite/oapi-sdk-go/v3"
	"github.com/larksuite/oapi-sdk-go/v3/service/xxx"
)

func main() {
	client := lark.NewClient("appID", "appSecret")
	req := larkxxx.NewRequestBuilder().Build()
	resp, err := client.Xxx.Function(context.Background(), req)
}
```

#### Java 请求示例

```java
import com.lark.oapi.Client;
import com.lark.oapi.service.xxx.model.*;
import com.lark.oapi.core.request.RequestOptions;

public class Main {
    public static void main(String arg[]) throws Exception {
        Client client = Client.newBuilder("appId", "appSecret").build();
        XXXReq req = XXXReq.newBuilder().build();
        XXXResp resp = client.xxx().function(req, RequestOptions.newBuilder().build());
    }
}
```
```

## 接口响应

### 模板说明

接口响应章节包含：

1. **响应头** - HTTP 响应头字段（如有）
2. **响应体** - JSON 响应体结构
3. **响应示例** - 完整的响应 JSON 示例

### 模板示例

#### 响应头示例

```markdown
### 响应头

| 名称 | 类型 | 描述 |
|------|------|------|
| - | - | 无额外响应头字段 |
```

#### 响应体示例

```markdown
### 响应体

| 字段 | 类型 | 描述 |
|------|------|------|
| `code` | int | 错误码，非 0 表示失败 |
| `msg` | string | 错误描述 |
| `data` | object | 响应数据 |
```

#### 响应体嵌套对象示例

```markdown
#### data 对象

| 字段 | 类型 | 描述 |
|------|------|------|
| `has_more` | boolean | 是否还有更多项 |
| `page_token` | string | 分页标记，当 has_more 为 true 时，会同时返回新的 page_token，否则不返回 page_token |
| `items` | user[] | 用户信息列表 |

#### data.items 数组中的 user 对象

| 字段 | 类型 | 描述 |
|------|------|------|
| `user_id` | string | 用户的 user_id，租户内用户的唯一标识<br>**权限要求**：获取用户 user ID (contact:user.employee_id:readonly) |
| `name` | string | 用户名<br>**权限要求（满足任一）**：<br>获取用户基本信息 (contact:user.base:readonly)<br>以应用身份访问通讯录 (contact:contact:access_as_app) |
| `email` | string | 邮箱<br>**权限要求**：获取用户邮箱信息 (contact:user.email:readonly) |
```

#### 简单对象示例

```markdown
#### user_status 对象

| 字段 | 类型 | 描述 |
|------|------|------|
| `is_frozen` | boolean | 是否为暂停状态 |
| `is_resigned` | boolean | 是否为离职状态 |
```

#### 响应示例示例

```markdown
### 响应示例

```json
{
    "code": 0,
    "msg": "success",
    "data": {
        "has_more": false,
        "page_token": "",
        "items": [
            {
                "user_id": "3e3cf96b",
                "name": "张三",
                "email": "zhangsan@example.com"
            }
        ]
    }
}
```
```

## 错误码

### 模板说明

错误码表格列出该接口可能返回的 HTTP 状态码、错误码、错误描述和排查建议。

### 模板示例

```markdown
## 错误码

| HTTP状态码 | 错误码 | 描述 | 排查建议 |
|------------|--------|------|----------|
| 400 | 41050 | no user authority error | 无用户权限。需将当前操作的用户添加到应用或用户的权限范围内 |
| 400 | 40011 | page size is invalid | 无效的分页参数。page_size 的取值上限为 50 |
| 400 | 40012 | page token is invalid error | 无效的分页参数。需要检查传入的 page_token 是否为上次请求返回的 page_token 值 |
| 403 | 40004 | no dept authority error | 无部门权限。当前操作的部门需在应用的通讯录权限范围内 |
```

## 排查思路

### 模板说明

排查思路表格用于提供详细的排查步骤。通常针对特定错误码（如 41050）提供不同调用方式（user_access_token vs tenant_access_token）的排查步骤。

### 模板示例

```markdown
### 排查思路

| HTTP状态码 | 错误码 | 描述 | 排查建议 |
|------------|--------|------|----------|
| 400 | 41050 | no user authority error | **使用 tenant_access_token 调用 API**<br>当前操作的用户需要添加在应用的通讯录权限范围内。由开发者登录[开发者后台](https://open.feishu.cn/app)，在应用详情页的 **开发配置** > **权限管理** > **数据权限** 页面内，配置 **通讯录权限范围**，添加指定用户。已发布的应用企业管理员可在[管理后台](http://feishu.cn/admin) > **工作台** > **应用管理** 页面，修改应用的通讯录权限范围。<br><br>**使用 user_access_token 调用 API**<br>由企业管理员在[管理后台](http://feishu.cn/admin) > **安全** > **成员权限** 页面中，点击 **组织架构可见范围** 进行管理。 |
| 403 | 40004 | no dept authority error | 当前操作的部门需在应用的通讯录权限范围内。通讯录权限范围的介绍与设置方式，参见[权限范围资源介绍](https://open.feishu.cn/document/...)。 |
```

## 相关链接

### 模板说明

相关链接表格列出与该接口相关的飞书官方文档链接。

### 模板示例

```markdown
## 相关链接

| 链接类型 | 链接 |
|----------|------|
| 应用权限配置 | [https://open.feishu.cn/document/...](https://open.feishu.cn/document/...) |
| 用户相关的 ID 概念 | [https://open.feishu.cn/document/...](https://open.feishu.cn/document/...) |
| 部门 ID 说明 | [https://open.feishu.cn/document/...](https://open.feishu.cn/document/...) |
| 权限范围校验 | [https://open.feishu.cn/document/...](https://open.feishu.cn/document/...) |
| 通用错误码 | [https://open.feishu.cn/document/...](https://open.feishu.cn/document/...) |
```
