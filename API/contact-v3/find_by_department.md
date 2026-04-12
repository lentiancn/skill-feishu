# 获取部门直属用户列表 (contact/v3/users/find_by_department)

调用该接口获取指定部门直属的用户信息列表。用户信息包括用户 ID、名称、邮箱、手机号以及状态等信息。

## 注意事项

- 使用用户身份（`user_access_token`）调用该接口时，接口将根据该用户的组织架构可见范围进行过滤，仅返回组织架构可见范围内的用户数据。
- 使用应用身份（`tenant_access_token`）调用该接口时，接口将根据应用的通讯录权限范围进行过滤。 如果请求的部门 ID 为 0（即根部门），则接口会校验应用是否具有全员的通讯录权限；如果请求的是非 0 的部门 ID，则会校验应用是否具有该部门的通讯录权限。无权限时，接口会返回无权限的报错信息；有权限则返回对应部门下的直属用户列表。
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

| 字段 | 所需权限 |
|------|---------|
| union_id | `contact:contact:readonly` 或 `contact:contact:access_as_app` |
| user_id | `contact:user.employee_id:readonly` |
| open_id | `contact:contact:readonly` 或 `contact:contact:access_as_app` |
| name | `contact:user.base:readonly` 或 `contact:contact:access_as_app` 或 `contact:contact:readonly` 或 `contact:contact:readonly_as_app` |
| en_name | `contact:user.base:readonly` 或 `contact:contact:access_as_app` 或 `contact:contact:readonly` 或 `contact:contact:readonly_as_app` |
| nickname | `contact:user.base:readonly` 或 `contact:contact:access_as_app` 或 `contact:contact:readonly` 或 `contact:contact:readonly_as_app` |
| email | `contact:user.email:readonly` |
| mobile | `contact:user.phone:readonly` |
| mobile_visible | - |
| gender | `contact:user.gender:readonly` 或 `contact:contact:access_as_app` 或 `contact:contact:readonly` 或 `contact:contact:readonly_as_app` |
| status | `contact:user.employee:readonly` 或 `contact:contact:access_as_app` 或 `contact:contact:readonly` 或 `contact:contact:readonly_as_app` |
| department_ids | `contact:user.department:readonly` 或 `contact:contact:access_as_app` 或 `contact:contact:readonly` 或 `contact:contact:readonly_as_app` |
| leader_user_id | `contact:user.department:readonly` 或 `contact:contact:access_as_app` 或 `contact:contact:readonly` 或 `contact:contact:readonly_as_app` |
| city | `contact:user.employee:readonly` 或 `contact:contact:access_as_app` 或 `contact:contact:readonly` 或 `contact:contact:readonly_as_app` |
| country | `contact:user.employee:readonly` 或 `contact:contact:access_as_app` 或 `contact:contact:readonly` 或 `contact:contact:readonly_as_app` |
| work_station | `contact:user.employee:readonly` 或 `contact:contact:access_as_app` 或 `contact:contact:readonly` 或 `contact:contact:readonly_as_app` |
| join_time | `contact:user.employee:readonly` 或 `contact:contact:access_as_app` 或 `contact:contact:readonly` 或 `contact:contact:readonly_as_app` |
| is_tenant_manager | `contact:user.employee:readonly` 或 `contact:contact:access_as_app` 或 `contact:contact:readonly` 或 `contact:contact:readonly_as_app` |
| employee_no | `contact:user.employee_number:read` 或 `contact:user.employee:readonly` 或 `contact:contact:access_as_app` 或 `contact:contact:readonly` 或 `contact:contact:readonly_as_app` |
| employee_type | `contact:user.employee:readonly` 或 `contact:contact:access_as_app` 或 `contact:contact:readonly` 或 `contact:contact:readonly_as_app` |
| orders | `contact:user.department:readonly` 或 `contact:contact:access_as_app` 或 `contact:contact:readonly` 或 `contact:contact:readonly_as_app` |
| custom_attrs | `contact:user.employee:readonly` 或 `contact:contact:access_as_app` 或 `contact:contact:readonly` 或 `contact:contact:readonly_as_app` |
| enterprise_email | `contact:user.employee:readonly` 或 `contact:contact:access_as_app` 或 `contact:contact:readonly` 或 `contact:contact:readonly_as_app` |
| job_title | `contact:user.employee:readonly` 或 `contact:contact:access_as_app` 或 `contact:contact:readonly` 或 `contact:contact:readonly_as_app` |
| geo | `contact:user.user_geo` |
| job_level_id | `contact:user.job_level:readonly` |
| job_family_id | `contact:user.job_family:readonly` |
| department_path | `contact:user.department_path:readonly` |
| dotted_line_leader_user_ids | `contact:user.dotted_line_leader_info.read` |

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

### 响应体

| 名称 | 类型 | 描述 |
|------|------|------|
| `code` | int | 错误码，非 0 表示失败 |
| `msg` | string | 错误描述 |
| `data` | object | 响应数据 |
| `has_more` | boolean | 是否还有更多项 |
| `page_token` | string | 分页标记，当 has_more 为 true 时返回 |
| `items` | array | 用户信息列表 |

### user 对象

| 字段 | 类型 | 描述 | 字段权限要求 |
|------|------|------|-------------|
| `union_id` | string | 用户的 union_id | `contact:contact:readonly` 或 `contact:contact:access_as_app` |
| `user_id` | string | 用户的 user_id | `contact:user.employee_id:readonly` |
| `open_id` | string | 用户的 open_id | `contact:contact:readonly` 或 `contact:contact:access_as_app` |
| `name` | string | 用户名 | `contact:user.base:readonly` 或 `contact:contact:access_as_app` 或 `contact:contact:readonly` 或 `contact:contact:readonly_as_app` |
| `en_name` | string | 英文名 | `contact:user.base:readonly` 或 `contact:contact:access_as_app` 或 `contact:contact:readonly` 或 `contact:contact:readonly_as_app` |
| `nickname` | string | 别名 | `contact:user.base:readonly` 或 `contact:contact:access_as_app` 或 `contact:contact:readonly` 或 `contact:contact:readonly_as_app` |
| `email` | string | 邮箱 | `contact:user.email:readonly` |
| `mobile` | string | 手机号 | `contact:user.phone:readonly` |
| `mobile_visible` | boolean | 手机号码是否可见 | - |
| `gender` | int | 性别（0:保密, 1:男, 2:女, 3:其他） | `contact:user.gender:readonly` 或 `contact:contact:access_as_app` 或 `contact:contact:readonly` 或 `contact:contact:readonly_as_app` |
| `avatar_key` | string | 头像的文件 Key | - |
| `avatar` | avatar_info | 用户头像信息 | `contact:user.base:readonly` 或 `contact:contact:access_as_app` 或 `contact:contact:readonly` 或 `contact:contact:readonly_as_app` |
| `status` | user_status | 用户状态 | `contact:user.employee:readonly` 或 `contact:contact:access_as_app` 或 `contact:contact:readonly` 或 `contact:contact:readonly_as_app` |
| `department_ids` | string[] | 用户所属部门的 ID 列表 | `contact:user.department:readonly` 或 `contact:contact:access_as_app` 或 `contact:contact:readonly` 或 `contact:contact:readonly_as_app` |
| `leader_user_id` | string | 用户的直接主管的用户ID | `contact:user.department:readonly` 或 `contact:contact:access_as_app` 或 `contact:contact:readonly` 或 `contact:contact:readonly_as_app` |
| `city` | string | 工作城市 | `contact:user.employee:readonly` 或 `contact:contact:access_as_app` 或 `contact:contact:readonly` 或 `contact:contact:readonly_as_app` |
| `country` | string | 国家或地区 Code 缩写 | `contact:user.employee:readonly` 或 `contact:contact:access_as_app` 或 `contact:contact:readonly` 或 `contact:contact:readonly_as_app` |
| `work_station` | string | 工位 | `contact:user.employee:readonly` 或 `contact:contact:access_as_app` 或 `contact:contact:readonly` 或 `contact:contact:readonly_as_app` |
| `join_time` | int | 入职时间 | `contact:user.employee:readonly` 或 `contact:contact:access_as_app` 或 `contact:contact:readonly` 或 `contact:contact:readonly_as_app` |
| `is_tenant_manager` | boolean | 是否为租户超级管理员 | `contact:user.employee:readonly` 或 `contact:contact:access_as_app` 或 `contact:contact:readonly` 或 `contact:contact:readonly_as_app` |
| `employee_no` | string | 工号 | `contact:user.employee_number:read` 或 `contact:user.employee:readonly` |
| `employee_type` | int | 员工类型 | `contact:user.employee:readonly` 或 `contact:contact:access_as_app` |
| `orders` | user_order[] | 用户排序信息 | `contact:user.department:readonly` 或 `contact:contact:access_as_app` |
| `custom_attrs` | user_custom_attr[] | 自定义字段 | `contact:user.employee:readonly` 或 `contact:contact:access_as_app` |
| `enterprise_email` | string | 企业邮箱 | `contact:user.employee:readonly` 或 `contact:contact:access_as_app` |
| `job_title` | string | 职务 | `contact:user.employee:readonly` 或 `contact:contact:access_as_app` |
| `is_frozen` | boolean | 是否为暂停状态的用户 | - |
| `geo` | string | 数据驻留地 | `contact:user.user_geo` |
| `job_level_id` | string | 职级 ID | `contact:user.job_level:readonly` |
| `job_family_id` | string | 序列 ID | `contact:user.job_family:readonly` |
| `department_path` | department_detail[] | 部门路径 | `contact:user.department_path:readonly` |
| `dotted_line_leader_user_ids` | string[] | 虚线上级的用户 ID | `contact:user.dotted_line_leader_info.read` |

## 请求示例

### 1. 获取指定部门下的所有用户

```bash
curl -X GET 'https://open.feishu.cn/open-apis/contact/v3/users/find_by_department?department_id=0' \
  -H 'Authorization: Bearer tenant_access_token'
```

### 2. 分页获取用户列表

```bash
curl -X GET 'https://open.feishu.cn/open-apis/contact/v3/users/find_by_department?department_id=od_xxx&page_size=10&page_token=AQD9/...' \
  -H 'Authorization: Bearer tenant_access_token'
```

### 3. 获取指定用户类型 ID 的用户

```bash
curl -X GET 'https://open.feishu.cn/open-apis/contact/v3/users/find_by_department?user_id_type=user_id&department_id=0' \
  -H 'Authorization: Bearer tenant_access_token'
```

## Go 请求示例

```go
import (
    "context"
    "github.com/larksuite/oapi-sdk-go/v3"
    "github.com/larksuite/oapi-sdk-go/v3/service/contact/v3"
)

func main() {
    // 创建 Client
    client := lark.NewClient("appID", "appSecret")

    // 创建请求对象
    req := larkcontact.NewFindByDepartmentUserReqBuilder().
        UserIdType(`open_id`).
        DepartmentIdType(`open_department_id`).
        DepartmentId(`od-xxxxxxxxxxxxx`).
        PageSize(10).
        Build()

    // 发起请求
    resp, err := client.Contact.User.FindByDepartment(context.Background(), req)
}
```

## Java 请求示例

```java
import com.lark.oapi.Client;
import com.lark.oapi.service.contact.v3.model.*;
import com.lark.oapi.core.request.RequestOptions;

public class Main {
    public static void main(String arg[]) throws Exception {
        // 构建client
        Client client = Client.newBuilder("appId", "appSecret").build();

        // 创建请求对象
        FindByDepartmentUserReq req = FindByDepartmentUserReq.newBuilder()
                .userIdType("open_id")
                .departmentIdType("open_department_id")
                .departmentId("od-xxxxxxxxxxxxx")
                .pageSize(10)
                .build();

        // 发起请求
        FindByDepartmentUserResp resp = client.contact().user().findByDepartment(req, RequestOptions.newBuilder().build());
    }
}
```

## 错误码

| HTTP 状态码 | 错误码 | 描述 | 排查建议 |
|------------|--------|------|----------|
| 400 | 41050 | no user authority error | 无用户权限 |
| 400 | 40011 | page size is invalid | 无效的分页参数（page_size 上限为 50） |
| 400 | 40012 | page token is invalid error | 无效的分页参数 |
| 403 | 40004 | no dept authority error | 无部门权限 |

## 相关链接

### 权限配置

- [权限范围资源介绍](https://open.feishu.cn/document/ukTMukTMukTM/uETNz4SM1MjLxUzM/v3/guides/scope_authority)
- [用户相关的 ID 概念](https://open.feishu.cn/document/home/user-identity-introduction/introduction)
- [部门 ID 说明](https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/reference/contact-v3/department/field-overview#23857fe0)

### API 文档

- [搜索部门](https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/reference/contact-v3/department/search)
- [获取人员类型](https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/reference/contact-v3/employee_type_enum/list)
- [通用错误码](https://open.feishu.cn/document/ukTMukTMukTM/ugjM14COyUjL4ITN)
