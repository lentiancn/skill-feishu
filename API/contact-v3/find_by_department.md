# 获取用户列表 (contact/v3/users/find_by_department)

调用该接口获取指定部门直属的用户信息列表。用户信息包括用户 ID、名称、邮箱、手机号以及状态等信息。

## 注意事项

- 使用用户身份（`user_access_token`）调用该接口时，接口将根据该用户的组织架构可见范围进行过滤，仅返回组织架构可见范围内的用户数据。
- 使用应用身份（`tenant_access_token`）调用该接口时，接口将根据应用的通讯录权限范围进行过滤。如果请求的部门 ID 为 0（即根部门），则接口会校验应用是否具有全员的通讯录权限；如果请求的是非 0 的部门 ID，则会校验应用是否具有该部门的通讯录权限。无权限时，接口会返回无权限的报错信息；有权限则返回对应部门下的直属用户列表。
- 使用应用身份（`tenant_access_token`）调用本接口时，响应结果中不会返回部门路径字段（`department_path`）。如需获取部门路径字段值，请为应用申请 **获取成员所在部门路径（`contact:user.department_path:readonly`）** API 权限，并使用用户身份（`user_access_token`）调用接口。

关于用户组织架构可见范围和通讯录权限范围的更多信息，可参见[权限范围资源介绍](https://open.feishu.cn/document/ukTMukTMukTM/uETNz4SM1MjLxUzM/v3/guides/scope_authority)。

## 基本信息

| 项目 | 值 |
|------|-----|
| **API 路径** | `https://open.feishu.cn/open-apis/contact/v3/users/find_by_department` |
| **请求方法** | GET |
| **接口频率限制** | 1000 次/分钟、50 次/秒 |
| **支持的应用类型** | 自建应用、商店应用 |
| **文档地址** | [飞书开放平台](https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/reference/contact-v3/user/find_by_department) |

## 权限要求

### 应用级别权限（开启任一即可）

- **获取通讯录基本信息** - `contact:contact.base:readonly`
- **获取通讯录部门组织架构信息** - `contact:department.organize:readonly`
- **以应用身份访问通讯录** - `contact:contact:access_as_app`
- **读取通讯录** - `contact:contact:readonly`
- **以应用身份读取通讯录** - `contact:contact:readonly_as_app`

### 字段权限要求

请查看 [PERMISSION/FIELDS.md](../PERMISSION/FIELDS.md) 获取完整的权限说明和链接。

## 请求参数

### 请求头

| 名称 | 类型 | 必填 | 描述 |
|------|------|------|------|
| `Authorization` | string | 是 | `tenant_access_token` 或 `user_access_token`<br>值格式："Bearer `access_token`"<br>示例值："Bearer u-7f1bcd13fc57d46bac21793a18e560"<br>**了解更多**：[如何选择与获取 access token](https://open.feishu.cn/document/uAjLw4CM/ugTN1YjL4UTN24CO1UjN/trouble-shooting/how-to-choose-which-type-of-token-to-use) |

### 查询参数

| 参数名 | 类型 | 必填 | 描述 |
|--------|------|------|------|
| `user_id_type` | string | 否 | 用户 ID 类型<br>可选值：<br>- `open_id`：标识一个用户在某个应用中的身份<br>- `union_id`：标识一个用户在某个应用开发商下的身份<br>- `user_id`：标识一个用户在某个租户内的身份<br>默认值：`open_id`<br>当值为 `user_id`，字段权限要求：`contact:user.employee_id:readonly` |
| `department_id_type` | string | 否 | 部门 ID 类型<br>可选值：<br>- `department_id`：支持用户自定义配置的部门 ID<br>- `open_department_id`：由系统自动生成的部门 ID<br>默认值：`open_department_id` |
| `department_id` | string | 是 | 部门 ID，ID 类型与 `department_id_type` 的取值保持一致。<br>说明：<br>- 根部门的部门 ID 为 0<br>- 可调用搜索部门接口获取对应的部门 ID |
| `page_size` | int | 否 | 分页大小<br>默认值：`10`<br>数据校验规则：<br>- 最大值：`50` |
| `page_token` | string | 否 | 分页标记，第一次请求不填，表示从头开始遍历 |

## 响应格式

（响应格式内容与之前一致，此处省略以节省空间）

## 请求示例

（请求示例内容与之前一致，此处省略以节省空间）

## Go 请求示例

（Go 示例内容与之前一致，此处省略以节省空间）

## Java 请求示例

（Java 示例内容与之前一致，此处省略以节省空间）

## 错误码

（错误码内容与之前一致，此处省略以节省空间）

## 相关链接

（相关链接内容与之前一致，此处省略以节省空间）
