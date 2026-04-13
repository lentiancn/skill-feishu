# 获取用户列表 (contact/v3/users/find_by_department)

调用该接口获取指定部门直属的用户信息列表。用户信息包括用户 ID、名称、邮箱、手机号以及状态等信息。

## 注意事项

- 使用用户身份（user_access_token）调用该接口时，接口将根据该用户的组织架构可见范围进行过滤，仅返回组织架构可见范围内的用户数据。
- 使用应用身份（tenant_access_token）调用该接口时，接口将根据应用的通讯录权限范围进行过滤。如果请求的部门 ID 为 0（即根部门），则接口会校验应用是否具有全员的通讯录权限；如果请求的是非 0 的部门 ID，则会校验应用是否具有该部门的通讯录权限。无权限时，接口会返回无权限的报错信息；有权限则返回对应部门下的直属用户列表。
- 使用应用身份（tenant_access_token）调用本接口时，响应结果中不会返回部门路径字段（department_path）。如需获取部门路径字段值，请为应用申请 **获取成员所在部门路径（contact:user.department_path:readonly）** API 权限，并使用用户身份（user_access_token）调用接口。

关于用户组织架构可见范围和通讯录权限范围的更多信息，可参见[权限范围资源介绍](https://open.feishu.cn/document/ukTMukTMukTM/uETNz4SM1MjLxUzM/v3/guides/scope_authority)。

## 权限要求

### 必要权限

| 类型 | 名称 |
|----------|----------|
| 应用权限（开启任一即可） | 获取通讯录基本信息 (contact:contact.base:readonly) |
| 应用权限（开启任一即可） | 获取通讯录部门组织架构信息 (contact:department.organize:readonly) |
| 应用权限（开启任一即可） | 以应用身份访问通讯录 (contact:contact:access_as_app) |
| 应用权限（开启任一即可） | 读取通讯录 (contact:contact:readonly) |
| 应用权限（开启任一即可） | 以应用身份读取通讯录 (contact:contact:readonly_as_app) |

### 可选权限

| 类型 | 名称 |
|----------|----------|
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

> **说明**：敏感字段仅在开启对应权限后才会返回；如无需获取这些字段，不建议申请。

## 接口信息

| API 路径 | `https://open.feishu.cn/open-apis/contact/v3/users/find_by_department` |
|----------|------------------------------------------------------------------------|
| 请求方法 | GET |
| 调用频率限制 | 1000 次/分钟、50 次/秒 |
| 支持的应用类型 | Custom App、Store App |
| 文档地址 | [飞书开放平台](https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/reference/contact-v3/user/find_by_department) |

## 接口请求

### 请求头

| 名称 | 类型 | 必填 | 描述 |
|------|------|------|------|
| `Authorization` | string | 是 | `tenant_access_token` 或 `user_access_token`<br>值格式："Bearer `access_token`"<br>示例值："Bearer u-7f1bcd13fc57d46bac21793a18e560"<br>**了解更多**：[如何选择与获取 access token](https://open.feishu.cn/document/uAjLw4CM/ugTN1YjL4UTN24CO1UjN/trouble-shooting/how-to-choose-which-type-of-token-to-use) |
| `Content-Type` | string | 是 | 固定值："application/json; charset=utf-8" |

### 请求参数

| 参数名 | 类型 | 必填 | 描述 |
|--------|------|------|------|
| `user_id_type` | string | 否 | 用户 ID 类型<br>可选值：<br>- `open_id`：标识一个用户在某个应用中的身份<br>- `union_id`：标识一个用户在某个应用开发商下的身份<br>- `user_id`：标识一个用户在某个租户内的身份<br>默认值：`open_id`<br>**权限要求**：当值为 `user_id` 时，需要获取用户 user ID (contact:user.employee_id:readonly) |
| `department_id_type` | string | 否 | 部门 ID 类型<br>可选值：<br>- `department_id`：支持用户自定义配置的部门 ID<br>- `open_department_id`：由系统自动生成的部门 ID<br>默认值：`open_department_id` |
| `department_id` | string | 是 | 部门 ID，ID 类型与 `department_id_type` 的取值保持一致。<br>说明：<br>- 根部门的部门 ID 为 0<br>- 可调用搜索部门接口获取对应的部门 ID |
| `page_size` | int | 否 | 分页大小<br>默认值：`10`<br>数据校验规则：<br>- 最大值：`50` |
| `page_token` | string | 否 | 分页标记，第一次请求不填，表示从头开始遍历 |

### 请求体

无请求体（GET 请求）

### 请求示例

#### Go 请求示例

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

#### Java 请求示例

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

## 接口响应

### 响应头

| 名称 | 类型 | 描述 |
|------|------|------|
| - | - | 无额外响应头字段 |

### 响应体

| 字段 | 类型 | 描述 |
|------|------|------|
| `code` | int | 错误码，非 0 表示失败 |
| `msg` | string | 错误描述 |
| `data` | object | 响应数据 |

#### data 对象

| 字段 | 类型 | 描述 |
|------|------|------|
| `has_more` | boolean | 是否还有更多项 |
| `page_token` | string | 分页标记，当 has_more 为 true 时，会同时返回新的 page_token，否则不返回 page_token |
| `items` | user[] | 用户信息列表 |

#### data.items 数组中的 user 对象

| 字段 | 类型 | 描述 |
|------|------|------|
| `union_id` | string | 用户的 union_id，是应用开发商发布的不同应用中同一用户的标识<br>**权限要求**：统一用户标识 (contact:user.base:readonly) |
| `user_id` | string | 用户的 user_id，租户内用户的唯一标识<br>**权限要求**：获取用户 user ID (contact:user.employee_id:readonly) |
| `open_id` | string | 用户的 open_id，应用内用户的唯一标识<br>**权限要求**：获取用户基本信息 (contact:user.base:readonly) |
| `name` | string | 用户名<br>**权限要求**：获取用户基本信息 (contact:user.base:readonly) |
| `en_name` | string | 英文名<br>**权限要求**：获取用户基本信息 (contact:user.base:readonly) |
| `nickname` | string | 别名<br>**权限要求**：获取用户基本信息 (contact:user.base:readonly) |
| `email` | string | 邮箱<br>**权限要求**：获取用户邮箱信息 (contact:user.email:readonly) |
| `mobile` | string | 手机号<br>**权限要求**：获取用户手机号 (contact:user.phone:readonly) |
| `mobile_visible` | boolean | 手机号码是否可见<br>- true：可见<br>- false：不可见 |
| `gender` | int | 性别<br>- 0：保密<br>- 1：男<br>- 2：女<br>- 3：其他<br>**权限要求**：获取用户性别 (contact:user.gender:readonly) |
| `avatar_key` | string | 头像的文件 Key |
| `avatar` | object | 用户头像信息<br>**权限要求**：获取用户基本信息 (contact:user.base:readonly) |
| `avatar_72` | string | 72*72 像素头像链接 |
| `avatar_240` | string | 240*240 像素头像链接 |
| `avatar_640` | string | 640*640 �素头像链接 |
| `avatar_origin` | string | 原始头像链接 |
| `status` | object | 用户状态<br>**权限要求**：获取用户受雇信息 (contact:user.employee:readonly) |
| `is_frozen` | boolean | 是否为暂停状态 |
| `is_resigned` | boolean | 是否为离职状态 |
| `is_activated` | boolean | 是否为激活状态 |
| `is_exited` | boolean | 是否为主动退出状态 |
| `is_unjoin` | boolean | 是否为未加入状态 |
| `department_ids` | string[] | 用户所属部门的 ID 列表<br>**权限要求**：获取用户组织架构信息 (contact:user.department:readonly) |
| `leader_user_id` | string | 用户的直接主管的用户ID<br>**权限要求**：获取用户组织架构信息 (contact:user.department:readonly) |
| `city` | string | 工作城市<br>**权限要求**：获取用户受雇信息 (contact:user.employee:readonly) |
| `country` | string | 国家或地区 Code 缩写<br>**权限要求**：获取用户受雇信息 (contact:user.employee:readonly) |
| `work_station` | string | 工位<br>**权限要求**：获取用户受雇信息 (contact:user.employee:readonly) |
| `join_time` | int | 入职时间（秒级时间戳）<br>**权限要求**：获取用户受雇信息 (contact:user.employee:readonly) |
| `is_tenant_manager` | boolean | 用户是否为租户超级管理员<br>**权限要求**：获取用户受雇信息 (contact:user.employee:readonly) |
| `employee_no` | string | 工号<br>**权限要求**：查看成员工号 (contact:user.employee_number:read) |
| `employee_type` | int | 员工类型<br>- 1：正式员工<br>- 2：实习生<br>- 3：外包<br>- 4：劳务<br>- 5：顾问<br>**权限要求**：获取用户受雇信息 (contact:user.employee:readonly) |
| `orders` | object[] | 用户排序信息<br>**权限要求**：获取用户组织架构信息 (contact:user.department:readonly) |
| `custom_attrs` | object[] | 自定义字段<br>**权限要求**：获取用户受雇信息 (contact:user.employee:readonly) |
| `enterprise_email` | string | 企业邮箱<br>**权限要求**：获取用户受雇信息 (contact:user.employee:readonly) |
| `job_title` | string | 职务<br>**权限要求**：获取用户受雇信息 (contact:user.employee:readonly) |
| `geo` | string | 数据驻留地<br>**权限要求**：查看成员数据驻留地 (contact:user.user_geo) |
| `job_level_id` | string | 职级 ID<br>**权限要求**：查询用户职级 (contact:user.job_level:readonly) |
| `job_family_id` | string | 序列 ID<br>**权限要求**：查询用户所属的工作序列 (contact:user.job_family:readonly) |
| `department_path` | object[] | 部门路径（仅 user_access_token 返回）<br>**权限要求**：获取成员所在部门路径 (contact:user.department_path:readonly) |
| `dotted_line_leader_user_ids` | string[] | 虚线上级的用户 ID<br>**权限要求**：查看成员的虚线上级 ID (contact:user.dotted_line_leader_info.read) |

#### user_status 对象

| 字段 | 类型 | 描述 |
|------|------|------|
| `is_frozen` | boolean | 是否为暂停状态 |
| `is_resigned` | boolean | 是否为离职状态 |
| `is_activated` | boolean | 是否为激活状态 |
| `is_exited` | boolean | 是否为主动退出状态 |
| `is_unjoin` | boolean | 是否为未加入状态 |

#### avatar_info 对象

| 字段 | 类型 | 描述 |
|------|------|------|
| `avatar_72` | string | 72*72 像素头像链接 |
| `avatar_240` | string | 240*240 像素头像链接 |
| `avatar_640` | string | 640*640 像素头像链接 |
| `avatar_origin` | string | 原始头像链接 |

#### user_order 对象

| 字段 | 类型 | 描述 |
|------|------|------|
| `department_id` | string | 排序信息对应的部门 ID |
| `user_order` | int | 用户在其直属部门内的排序 |
| `department_order` | int | 用户所属的多个部门间的排序 |
| `is_primary_dept` | boolean | 是否为用户的唯一主部门 |

#### user_custom_attr 对象

| 字段 | 类型 | 描述 |
|------|------|------|
| `type` | string | 自定义字段类型<br>- TEXT：文本<br>- HREF：网页<br>- ENUMERATION：枚举<br>- PICTURE_ENUM：图片<br>- GENERIC_USER：用户 |
| `id` | string | 自定义字段 ID |
| `value` | object | 自定义字段取值 |

#### user_custom_attr_value 对象

| 字段 | 类型 | 描述 |
|------|------|------|
| `text` | string | TEXT 类型返回字段值 |
| `url` | string | HREF 类型返回默认 URL |
| `pc_url` | string | HREF 类型返回 PC 端 URL |
| `option_id` | string | ENUMERATION/PICTURE_ENUM 类型返回选项 ID |
| `option_value` | string | 枚举类型返回选项值 |
| `name` | string | PICTURE_ENUM 类型返回图片名称 |
| `picture_url` | string | PICTURE_ENUM 类型返回图片链接 |
| `generic_user` | object | GENERIC_USER 类型返回引用人员信息 |

#### generic_user 对象

| 字段 | 类型 | 描述 |
|------|------|------|
| `id` | string | 引用人员的用户 ID |
| `type` | int | 用户类型（固定为 1） |

#### department_detail 对象

| 字段 | 类型 | 描述 |
|------|------|------|
| `department_id` | string | 部门 ID |
| `department_name` | object | 部门名称信息 |
| `department_path` | object | 部门路径 |
| `department_ids` | string[] | 部门路径 ID 列表 |

#### department_path_name 对象

| 字段 | 类型 | 描述 |
|------|------|------|
| `name` | string | 部门名 |
| `i18n_name` | object | 部门国际化名 |

#### department_i18n_name 对象

| 字段 | 类型 | 描述 |
|------|------|------|
| `zh_cn` | string | 部门的中文名 |
| `ja_jp` | string | 部门的日文名 |
| `en_us` | string | 部门的英文名 |

#### department_path 对象

| 字段 | 类型 | 描述 |
|------|------|------|
| `department_ids` | string[] | 部门路径 ID 列表 |
| `department_path_name` | object | 部门路径名字信息 |

### 响应示例

```json
{
    "code": 0,
    "msg": "success",
    "data": {
        "has_more": true,
        "page_token": "AQD9/Rn9eij9Pm39ED40/RD/cIFmu77WxpxPB/2oHfQLZ%2BG8JG6tK7%2BZnHiT7COhD2hMSICh/eBl7cpzU6JEC3J7COKNe4jrQ8ExwBCR",
        "items": [
            {
                "union_id": "on_94a1ee5551019f18cd73d9f111898cf2",
                "user_id": "3e3cf96b",
                "open_id": "ou_7dab8a3d3cdcc9da365777c7ad535d62",
                "name": "张三",
                "en_name": "San Zhang",
                "nickname": "Alex Zhang",
                "email": "zhangsan@gmail.com",
                "mobile": "13011111111",
                "mobile_visible": false,
                "gender": 1,
                "avatar_key": "2500c7a9-5fff-4d9a-a2de-3d59614ae28g",
                "avatar": {
                    "avatar_72": "https://foo.icon.com/xxxx",
                    "avatar_240": "https://foo.icon.com/xxxx",
                    "avatar_640": "https://foo.icon.com/xxxx",
                    "avatar_origin": "https://foo.icon.com/xxxx"
                },
                "status": {
                    "is_frozen": false,
                    "is_resigned": false,
                    "is_activated": true,
                    "is_exited": false,
                    "is_unjoin": false
                },
                "department_ids": [
                    "od-4e6ac4d14bcd5071a37a39de902c7141"
                ],
                "leader_user_id": "ou_7dab8a3d3cdcc9da365777c7ad535d62",
                "city": "杭州",
                "country": "CN",
                "work_station": "北楼-H34",
                "join_time": 2147483647,
                "is_tenant_manager": false,
                "employee_no": "1",
                "employee_type": 1,
                "orders": [
                    {
                        "department_id": "od-4e6ac4d14bcd5071a37a39de902c7141",
                        "user_order": 100,
                        "department_order": 100,
                        "is_primary_dept": true
                    }
                ],
                "custom_attrs": [
                    {
                        "type": "TEXT",
                        "id": "DemoId",
                        "value": {
                            "text": "DemoText",
                            "url": "http://www.fs.cn",
                            "pc_url": "http://www.fs.cn",
                            "option_id": "edcvfrtg",
                            "option_value": "option",
                            "name": "name",
                            "picture_url": "https://xxxxxxxxxxxxxxxxxx",
                            "generic_user": {
                                "id": "9b2fabg5",
                                "type": 1
                            }
                        }
                    }
                ],
                "enterprise_email": "demo@mail.com",
                "job_title": "xxxxx",
                "is_frozen": false,
                "geo": "cn",
                "job_level_id": "mga5oa8ayjlp9rb",
                "job_family_id": "mga5oa8ayjlp9rb",
                "department_path": [
                    {
                        "department_id": "od-4e6ac4d14bcd5071a37a39de902c7141",
                        "department_name": {
                            "name": "测试部门名1",
                            "i18n_name": {
                                "zh_cn": "测试部门名1",
                                "ja_jp": "試験部署名 1",
                                "en_us": "Test department name 1"
                            }
                        },
                        "department_path": {
                            "department_ids": [
                                "od-4e6ac4d14bcd5071a37a39de902c7141"
                            ],
                            "department_path_name": {
                                "name": "测试部门名1",
                                "i18n_name": {
                                    "zh_cn": "测试部门名1",
                                    "ja_jp": "試験部署名 1",
                                    "en_us": "Test department name 1"
                                }
                            }
                        }
                    }
                ],
                "dotted_line_leader_user_ids": [
                    "ou_7dab8a3d3cdcc9da365777c7ad535d62"
                ]
            }
        ]
    }
}
```

## 错误码

| HTTP状态码 | 错误码 | 描述 | 排查建议 |
|------------|--------|------|----------|
| 400 | 41050 | no user authority error | 无用户权限。需将当前操作的用户添加到应用或用户的权限范围内 |
| 400 | 40011 | page size is invalid | 无效的分页参数。page_size 的取值上限为 50 |
| 400 | 40012 | page token is invalid error | 无效的分页参数。需要检查传入的 page_token 是否为上次请求返回的 page_token 值 |
| 403 | 40004 | no dept authority error | 无部门权限。当前操作的部门需在应用的通讯录权限范围内 |

### 排查思路

| HTTP状态码 | 错误码 | 描述 | 排查建议 |
|------------|--------|------|----------|
| 400 | 41050 | no user authority error | 无用户权限。需将当前操作的用户添加到应用或用户的权限范围内 |
| 400 | 40011 | page size is invalid | 无效的分页参数。page_size 的取值上限为 50 |
| 400 | 40012 | page token is invalid error | 无效的分页参数。需要检查传入的 page_token 是否为上次请求返回的 page_token 值 |
| 403 | 40004 | no dept authority error | 无部门权限。当前操作的部门需在应用的通讯录权限范围内 |

## 相关链接

| 链接类型 | 链接 |
|----------|------|
| 应用权限配置 | [https://open.feishu.cn/document/ugTN1YjL4UTN24CO1UjN/uQzN1YjL0cTN24CN3UjN](https://open.feishu.cn/document/ugTN1YjL4UTN24CO1UjN/uQzN1YjL0cTN24CN3UjN) |
| 用户相关的 ID 概念 | [https://open.feishu.cn/document/home/user-identity-introduction/introduction](https://open.feishu.cn/document/home/user-identity-introduction/introduction) |
| 部门 ID 说明 | [https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/reference/contact-v3/department/field-overview](https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/reference/contact-v3/department/field-overview) |
| 权限范围校验 | [https://open.feishu.cn/document/ukTMukTMukTM/uETNz4SM1MjLxUzM/v3/guides/scope_authority](https://open.feishu.cn/document/ukTMukTMukTM/uETNz4SM1MjLxUzM/v3/guides/scope_authority) |
| 通用错误码 | [https://open.feishu.cn/document/ukTMukTMukTM/ugjM14COyUjL4ITN](https://open.feishu.cn/document/ukTMukTMukTM/ugjM14COyUjL4ITN) |
