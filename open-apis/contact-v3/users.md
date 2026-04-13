# 获取用户列表 (contact/v3/users)

基于部门ID获取部门下直属用户列表。

**注意事项**：
- 本接口已为历史版本，不再维护更新，不推荐使用。推荐使用 [获取部门直属用户列表](https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/reference/contact-v3/user/find_by_department) 接口。
- [常见问题答疑](https://open.feishu.cn/document/ugTN1YjL4UTN24CO1UjN/uQzN1YjL0cTN24CN3UjN)。

## 重要提示

### 权限说明

#### 两种 token 的权限校验方式不同：

1. **user_access_token**
   - 根据个人组织架构的通讯录可见范围进行权限过滤
   - 返回个人组织架构通讯录范围（[登陆企业管理后台进行权限配置](https://www.feishu.cn/admin/security/permission/visibility)）内可见的用户数据

2. **tenant_access_token**
   - 基于应用通讯录范围进行权限鉴定
   - `department_id` 是非必填参数，填与不填存在**两种数据权限校验与返回情况**：
     - **情况1**：请求设置了 `department_id`（根部门为0），会检验所带部门ID是否具有通讯录权限（如果带上 `department_id=0` 会校验是否有全员权限），有则返回部门下直属的成员列表，否则提示无部门权限的错误码返回
     - **情况2**：请求未带 `department_id` 参数，则会返回权限范围内的独立用户（权限范围直接包含了某用户，则该用户视为权限范围内的独立用户）

## 基本信息

| 项目 | 值 |
|------|-----|
| **API 路径** | `https://open.feishu.cn/open-apis/contact/v3/users` |
| **请求方法** | GET |
| **支持的应用类型** | 自建应用、商店应用 |
| **最后更新** | 2026-04-07 |
| **状态** | 历史版本，不再维护 |
| **文档地址** | [https://open.feishu.cn/document/server-docs/historic-version//user/list](https://open.feishu.cn/document/server-docs/historic-version//user/list) |

## 权限要求

### 应用级别权限（开启任一即可）

- **获取部门组织架构信息** - `contact:department.organize:readonly`
- **以应用身份读取通讯录** - `contact:contact:readonly_as_app`
- **读取通讯录** - `contact:contact:readonly`
- **以应用身份访问通讯录** - `contact:contact:access_as_app`

### 字段权限要求

| 字段 | 所需权限 |
|------|---------|
| union_id | `contact:contact:readonly` 或 `contact:contact:access_as_app` |
| user_id | `contact:user.employee_id:readonly` |
| open_id | `contact:contact:readonly` 或 `contact:contact:access_as_app` |
| name | `contact:user.base:readonly` 或 `contact:contact:readonly_as_app` 或 `contact:contact:readonly` 或 `contact:contact:access_as_app` |
| en_name | `contact:user.base:readonly` 或 `contact:contact:readonly_as_app` 或 `contact:contact:readonly` 或 `contact:contact:access_as_app` |
| email | `contact:user.email:readonly` |
| mobile | `contact:user.phone:readonly` |
| gender | `contact:user.gender:readonly` 或 `contact:contact:readonly_as_app` 或 `contact:contact:readonly` 或 `contact:contact:access_as_app` |
| avatar | `contact:user.base:readonly` 或 `contact:contact:readonly_as_app` 或 `contact:contact:readonly` 或 `contact:contact:access_as_app` |
| status | `contact:user.employee:readonly` 或 `contact:contact:readonly_as_app` 或 `contact:contact:readonly` 或 `contact:contact:access_as_app` |
| department_ids | `contact:user.department:readonly` 或 `contact:contact:readonly_as_app` 或 `contact:contact:readonly` 或 `contact:contact:access_as_app` |
| leader_user_id | `contact:user.department:readonly` 或 `contact:contact:readonly_as_app` 或 `contact:contact:readonly` 或 `contact:contact:access_as_app` |
| city | `contact:user.employee:readonly` 或 `contact:contact:readonly_as_app` 或 `contact:contact:readonly` 或 `contact:contact:access_as_app` |
| country | `contact:user.employee:readonly` 或 `contact:contact:readonly_as_app` 或 `contact:contact:readonly` 或 `contact:contact:access_as_app` |
| work_station | `contact:user.employee:readonly` 或 `contact:contact:readonly_as_app` 或 `contact:contact:readonly` 或 `contact:contact:access_as_app` |
| join_time | `contact:user.employee:readonly` 或 `contact:contact:readonly_as_app` 或 `contact:contact:readonly` 或 `contact:contact:access_as_app` |
| is_tenant_manager | `contact:user.employee:readonly` 或 `contact:contact:readonly_as_app` 或 `contact:contact:readonly` 或 `contact:contact:access_as_app` |
| employee_no | `contact:user.employee:readonly` 或 `contact:contact:readonly_as_app` 或 `contact:contact:readonly` 或 `contact:contact:access_as_app` |
| employee_type | `contact:user.employee:readonly` 或 `contact:contact:readonly_as_app` 或 `contact:contact:readonly` 或 `contact:contact:access_as_app` |
| orders | `contact:user.department:readonly` 或 `contact:contact:readonly_as_app` 或 `contact:contact:readonly` 或 `contact:contact:access_as_app` |
| custom_attrs | `contact:user.employee:readonly` 或 `contact:contact:readonly_as_app` 或 `contact:contact:readonly` 或 `contact:contact:access_as_app` |
| enterprise_email | `contact:user.employee:readonly` 或 `contact:contact:readonly_as_app` 或 `contact:contact:readonly` 或 `contact:contact:access_as_app` |
| job_title | `contact:user.employee:readonly` 或 `contact:contact:readonly_as_app` 或 `contact:contact:readonly` 或 `contact:contact:access_as_app` |

## 请求参数

### 请求头

| 名称 | 类型 | 必填 | 描述 |
|------|------|------|------|
| `Authorization` | string | 是 | `tenant_access_token` 或 `user_access_token`<br>值格式："Bearer `access_token`"<br>示例值："Bearer u-7f1bcd13fc57d46bac21793a18e560"<br>**了解更多**：[如何选择与获取 access token](https://open.feishu.cn/document/uAjLw4CM/ugTN1YjL4UTN24CO1UjN/trouble-shooting/how-to-choose-which-type-of-token-to-use) |

### 查询参数

| 参数名 | 类型 | 必填 | 描述 |
|--------|------|------|------|
| `user_id_type` | string | 否 | 用户 ID 类型<br>可选值：<br>- `open_id`：用户的 open id<br>- `union_id`：用户的 union id<br>- `user_id`：用户的 user id<br>默认值：`open_id`<br>当值为 `user_id`，字段权限要求：`contact:user.employee_id:readonly` |
| `department_id_type` | string | 否 | 此次调用中使用的部门ID的类型<br>可选值：<br>- `department_id`：以自定义department_id来标识部门<br>- `open_department_id`：以open_department_id来标识部门<br>默认值：`open_department_id` |
| `department_id` | string | 否 | 填写该字段表示获取部门下所有用户，选填。<br>示例值："od-xxxxxxxxxxxxx" |
| `page_token` | string | 否 | 分页标记，第一次请求不填，表示从头开始遍历；分页查询结果还有更多项时会同时返回新的 page_token，下次遍历可采用该 page_token 获取查询结果 |
| `page_size` | int | 否 | 分页大小<br>数据校验规则：<br>- 最大值：`100` |

## 响应格式

### 响应体

| 名称 | 类型 | 描述 |
|------|------|------|
| `code` | int | 错误码，非 0 表示失败 |
| `msg` | string | 错误描述 |
| `data` | object | 响应数据 |

### data 对象

| 名称 | 类型 | 描述 |
|------|------|------|
| `has_more` | boolean | 是否还有更多项 |
| `page_token` | string | 分页标记，当 has_more 为 true 时，会同时返回新的 page_token，否则不返回 page_token |
| `items` | array | 用户列表，每个元素为一个 user 对象 |

### user 对象

| 名称 | 类型 | 描述 | 字段权限要求 |
|------|------|------|-------------|
| `union_id` | string | 用户的 union_id，应用开发商发布的不同应用中同一用户的标识。关于用户 ID 的说明可参见 [用户相关的 ID 概念](https://open.feishu.cn/document/home/user-identity-introduction/introduction) | `contact:contact:readonly` 或 `contact:contact:access_as_app` |
| `user_id` | string | 用户的 user_id，租户内用户的唯一标识 | `contact:user.employee_id:readonly` |
| `open_id` | string | 用户的 open_id，应用内用户的唯一标识 | `contact:contact:readonly` 或 `contact:contact:access_as_app` |
| `name` | string | 用户名 | `contact:user.base:readonly` 或 `contact:contact:readonly_as_app` 或 `contact:contact:readonly` 或 `contact:contact:access_as_app` |
| `en_name` | string | 英文名 | `contact:user.base:readonly` 或 `contact:contact:readonly_as_app` 或 `contact:contact:readonly` 或 `contact:contact:access_as_app` |
| `email` | string | 邮箱 | `contact:user.email:readonly` |
| `mobile` | string | 手机号 | `contact:user.phone:readonly` |
| `mobile_visible` | boolean | 手机号码可见性，true 为可见，false 为不可见，目前默认为 true。不可见时，组织员工将无法查看该员工的手机号码 | - |
| `gender` | int | 性别。可选值：<br>- `0`：保密<br>- `1`：男<br>- `2`：女 | `contact:user.gender:readonly` 或 `contact:contact:readonly_as_app` 或 `contact:contact:readonly` 或 `contact:contact:access_as_app` |
| `avatar` | avatar_info | 用户头像信息 | `contact:user.base:readonly` 或 `contact:contact:readonly_as_app` 或 `contact:contact:readonly` 或 `contact:contact:access_as_app` |
| `status` | user_status | 用户状态。通过 is_frozen、is_resigned、is_activated、is_exited 布尔值类型参数进行展示。用户状态的流转逻辑可参见 [用户资源介绍](https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/reference/contact-v3/user/field-overview#4302b5a1) | `contact:user.employee:readonly` 或 `contact:contact:readonly_as_app` 或 `contact:contact:readonly` 或 `contact:contact:access_as_app` |
| `department_ids` | string[] | 用户所属部门的ID列表，一个用户可属于多个部门。ID值的类型与查询参数中的department_id_type 对应。不同 ID 的说明与department_id的获取方式参见 [部门ID说明](https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/reference/contact-v3/department/field-overview#23857fe0) | `contact:user.department:readonly` 或 `contact:contact:readonly_as_app` 或 `contact:contact:readonly` 或 `contact:contact:access_as_app` |
| `leader_user_id` | string | 用户的直接主管的 open_id。关于用户 ID 的说明可参见 [用户相关的 ID 概念](https://open.feishu.cn/document/home/user-identity-introduction/introduction) | `contact:user.department:readonly` 或 `contact:contact:readonly_as_app` 或 `contact:contact:readonly` 或 `contact:contact:access_as_app` |
| `city` | string | 工作城市 | `contact:user.employee:readonly` 或 `contact:contact:readonly_as_app` 或 `contact:contact:readonly` 或 `contact:contact:access_as_app` |
| `country` | string | 国家或地区 Code 缩写。具体格式可参见 [国家/地区码表](https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/reference/contact-v3/user/country-code-description) | `contact:user.employee:readonly` 或 `contact:contact:readonly_as_app` 或 `contact:contact:readonly` 或 `contact:contact:access_as_app` |
| `work_station` | string | 工位 | `contact:user.employee:readonly` 或 `contact:contact:readonly_as_app` 或 `contact:contact:readonly` 或 `contact:contact:access_as_app` |
| `join_time` | int | 入职时间。秒级时间戳格式，表示从 1970 年 1 月 1 日开始所经过的秒数 | `contact:user.employee:readonly` 或 `contact:contact:readonly_as_app` 或 `contact:contact:readonly` 或 `contact:contact:access_as_app` |
| `is_tenant_manager` | boolean | 是否是租户超级管理员 | `contact:user.employee:readonly` 或 `contact:contact:readonly_as_app` 或 `contact:contact:readonly` 或 `contact:contact:access_as_app` |
| `employee_no` | string | 工号 | `contact:user.employee:readonly` 或 `contact:contact:readonly_as_app` 或 `contact:contact:readonly` 或 `contact:contact:access_as_app` |
| `employee_type` | int | 员工类型。可能值：<br>- `1`：正式员工<br>- `2`：实习生<br>- `3`：外包<br>- `4`：劳务<br>- `5`：顾问<br><br>同时可读取到自定义员工类型的 int 值，通过 int 值调用 [获取人员类型](https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/reference/contact-v3/employee_type_enum/list) 接口，进而获取到该租户的自定义员工类型的名称 | `contact:user.employee:readonly` 或 `contact:contact:readonly_as_app` 或 `contact:contact:readonly` 或 `contact:contact:access_as_app` |
| `orders` | user_order[] | 用户排序信息。用于标记通讯录下组织架构的人员顺序，人员可能存在多个部门中，且有不同的排序 | `contact:user.department:readonly` 或 `contact:contact:readonly_as_app` 或 `contact:contact:readonly` 或 `contact:contact:access_as_app` |
| `custom_attrs` | user_custom_attr[] | 自定义字段。如果企业管理员已在管理后台 > 组织架构 > 成员字段管理 > 自定义字段管理 > 全局设置中开启了 **允许开放平台 API 调用**，则该字段生效。更多信息可参见 [用户接口相关问题](https://open.feishu.cn/document/ugTN1YjL4UTN24CO1UjN/uQzN1YjL0cTN24CN3UjN#77061525) | `contact:user.employee:readonly` 或 `contact:contact:readonly_as_app` 或 `contact:contact:readonly` 或 `contact:contact:access_as_app` |
| `enterprise_email` | string | 企业邮箱。如果企业管理员已在管理后台启用飞书邮箱服务，则会返回该值 | `contact:user.employee:readonly` 或 `contact:contact:readonly_as_app` 或 `contact:contact:readonly` 或 `contact:contact:access_as_app` |
| `job_title` | string | 职务 | `contact:user.employee:readonly` 或 `contact:contact:readonly_as_app` 或 `contact:contact:readonly` 或 `contact:contact:access_as_app` |

### avatar_info 对象

| 名称 | 类型 | 描述 |
|------|------|------|
| `avatar_72` | string | 72*72 像素头像链接 |
| `avatar_240` | string | 240*240 像素头像链接 |
| `avatar_640` | string | 640*640 像素头像链接 |
| `avatar_origin` | string | 原始头像链接 |

### user_status 对象

| 名称 | 类型 | 描述 |
|------|------|------|
| `is_frozen` | boolean | 是否为暂停状态 |
| `is_resigned` | boolean | 是否为离职状态 |
| `is_activated` | boolean | 是否为激活状态 |

### user_order 对象

| 名称 | 类型 | 描述 |
|------|------|------|
| `department_id` | string | 排序信息对应的部门 ID，表示用户所在的、且需要排序的部门。该 ID 均包含在用户所属部门 ID 列表（department_ids）的参数值当中 |
| `user_order` | int | 用户在其直属部门内的排序，数值越大，排序越靠前 |
| `department_order` | int | 用户所属的多个部门间的排序，数值越大，排序越靠前 |

### user_custom_attr 对象

| 名称 | 类型 | 描述 |
|------|------|------|
| `type` | string | 自定义字段类型。可能值：<br>- `TEXT`：文本<br>- `HREF`：网页<br>- `ENUMERATION`：枚举<br>- `PICTURE_ENUM`：图片<br>- `GENERIC_USER`：用户 |
| `id` | string | 自定义字段 ID |
| `value` | user_custom_attr_value | 自定义字段取值 |

### user_custom_attr_value 对象

| 名称 | 类型 | 描述 |
|------|------|------|
| `text` | string | 字段类型为 TEXT 时，该参数返回定义的字段值 |
| `url` | string | 字段类型为 HREF 时，该参数返回定义的默认 URL |
| `pc_url` | string | 字段类型为 HREF 时，如果为 PC 端设置了 URL，则该参数返回定义的 PC 端 URL |
| `option_value` | string | 选项类型的值，即用户详情或自定义字段中选中的选项值 |
| `name` | string | 选项类型为图片时，图片的名称 |
| `picture_url` | string | 选项类型为图片时，图片的链接 |
| `generic_user` | custom_attr_generic_user | 字段类型为 `GENERIC_USER` 时，该参数返回定义的引用人员信息 |

### custom_attr_generic_user 对象

| 名称 | 类型 | 描述 |
|------|------|------|
| `id` | string | 引用人员的 user_id。关于用户 ID 的具体说明可参见 [用户相关的 ID 概念](https://open.feishu.cn/document/home/user-identity-introduction/introduction) |
| `type` | int | 用户类型。目前固定取值为 1，表示用户 |

## 请求示例

### 1. 获取根部门（部门ID=0）下的所有用户

```bash
curl -X GET 'https://open.feishu.cn/open-apis/contact/v3/users?department_id=0' \
  -H 'Authorization: Bearer tenant_access_token'
```

### 2. 分页获取用户列表

```bash
curl -X GET 'https://open.feishu.cn/open-apis/contact/v3/users?department_id=od_xxx&page_size=10&page_token=AQD9/...' \
  -H 'Authorization: Bearer tenant_access_token'
```

### 3. 不带 department_id 参数（返回权限范围内的独立用户）

```bash
curl -X GET 'https://open.feishu.cn/open-apis/contact/v3/users' \
  -H 'Authorization: Bearer tenant_access_token'
```

### 4. 获取指定用户类型 ID 的用户

```bash
curl -X GET 'https://open.feishu.cn/open-apis/contact/v3/users?user_id_type=user_id' \
  -H 'Authorization: Bearer tenant_access_token'
```

## 响应体示例

```json
{
    "code": 0,
    "msg": "success",
    "data": {
        "has_more": false,
        "page_token": "AQD9/Rn9eij9Pm39ED40/RD/cIFmu77WxpxPB/2oHfQLZ%2BG8JG6tK7%2BZnHiT7COhD2hMSICh/eBl7cpzU6JEC3J7COKNe4jrQ8ExwBCR",
        "items": [
            {
                "union_id": "on_94a1ee5551019f18cd73d9f111898cf2",
                "user_id": "3e3cf96b",
                "open_id": "ou_7dab8a3d3cdcc9da365777c7ad535d62",
                "name": "张三",
                "en_name": "San Zhang",
                "email": "zhangsan@gmail.com",
                "mobile": "130xxxx1111",
                "mobile_visible": false,
                "gender": 1,
                "avatar": {
                    "avatar_72": "https://foo.icon.com/xxxx",
                    "avatar_240": "https://foo.icon.com/xxxx",
                    "avatar_640": "https://foo.icon.com/xxxx",
                    "avatar_origin": "https://foo.icon.com/xxxx"
                },
                "status": {
                    "is_frozen": false,
                    "is_resigned": false,
                    "is_activated": true
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
                        "department_order": 100
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
                "job_title": "xxxxx"
            }
        ]
    }
}
```

## 错误码

| HTTP 状态码 | 错误码 | 描述 | 排查建议 |
|------------|--------|------|----------|
| 400 | 41050 | no user authority error | 操作的用户需在通讯录权限范围中，[了解更多](https://open.feishu.cn/document/ukTMukTMukTM/uETNz4SM1MjLxUzM/v3/guides/scope_authority) |
| 400 | 40011 | page size is invalid | 无效的分页参数 |
| 400 | 40012 | page token is invalid error | page token无效。 |
| 403 | 40004 | no dept authority error | 操作的部门需在通讯录权限范围中，[了解更多](https://open.feishu.cn/document/ukTMukTMukTM/uETNz4SM1MjLxUzM/v3/guides/scope_authority) |

## 相关链接

### 权限配置

- [通讯录权限配置](https://open.feishu.cn/document/ugTN1YjL4UTN24CO1UjN/uQzN1YjL0cTN24CN3UjN)
- [企业后台权限管理](https://www.feishu.cn/admin/security/permission/visibility)
- [用户相关 ID 概念](https://open.feishu.cn/document/home/user-identity-introduction/introduction)

### API 文档

- [获取部门直属用户列表（推荐）](https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/reference/contact-v3/user/find_by_department)
- [部门 ID 说明](https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/reference/contact-v3/department/field-overview#23857fe0)
- [国家/地区码表](https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/reference/contact-v3/user/country-code-description)
- [获取人员类型](https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/reference/contact-v3/employee_type_enum/list)
- [用户接口相关问题](https://open.feishu.cn/document/ugTN1YjL4UTN24CO1UjN/uQzN1YjL0cTN24CN3UjN#77061525)
