# 获取单个用户信息 (contact/v3/users/:user_id)

调用该接口获取通讯录中某一用户的信息，包括用户 ID、名称、邮箱、手机号、状态以及所属部门等信息。

## 注意事项

使用应用身份（`tenant_access_token`）调用本接口时，响应结果中不会返回部门路径字段（`department_path`）。因此，如需获取部门路径字段值，请为应用申请 **获取成员所在部门路径** API 权限，并使用用户身份（`user_access_token`）调用接口。

## 基本信息

| 项目 | 值 |
|------|-----|
| **API 路径** | `https://open.feishu.cn/open-apis/contact/v3/users/:user_id` |
| **请求方法** | GET |
| **接口频率限制** | 1000 次/分钟、50 次/秒 |
| **支持的应用类型** | 自建应用、商店应用 |
| **文档地址** | [飞书开放平台](https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/reference/contact-v3/user/get) |

## 权限要求

### 应用级别权限（开启任一即可）

- **获取通讯录基本信息** - `contact:contact.base:readonly`
- **以应用身份访问通讯录** - `contact:contact:access_as_app`
- **读取通讯录** - `contact:contact:readonly`
- **以应用身份读取通讯录** - `contact:contact:readonly_as_app`

### 字段权限要求

| 字段 | 所需权限 | 中文说明 |
|------|---------|---------|
| `union_id` | `contact:contact:readonly` 或 `contact:contact:access_as_app` | 统一用户标识 |
| `user_id` | `contact:user.employee_id:readonly` | 获取用户 user ID |
| `open_id` | `contact:contact:readonly` 或 `contact:contact:access_as_app` | 应用内用户标识 |
| `name` | `contact:user.base:readonly` | 获取用户基本信息 |
| `en_name` | `contact:user.base:readonly` | 获取用户基本信息 |
| `nickname` | `contact:user.base:readonly` | 获取用户基本信息 |
| `email` | `contact:user.email:readonly` | 获取用户邮箱信息 |
| `mobile` | `contact:user.phone:readonly` | 获取用户手机号 |
| `mobile_visible` | - | 手机号可见性（无需权限） |
| `gender` | `contact:user.gender:readonly` | 获取用户性别 |
| `avatar` | `contact:user.base:readonly` | 获取用户基本信息 |
| `status` | `contact:user.employee:readonly` | 获取用户受雇信息 |
| `department_ids` | `contact:user.department:readonly` | 获取用户组织架构信息 |
| `leader_user_id` | `contact:user.department:readonly` | 获取用户组织架构信息 |
| `city` | `contact:user.employee:readonly` | 获取用户受雇信息 |
| `country` | `contact:user.employee:readonly` | 获取用户受雇信息 |
| `work_station` | `contact:user.employee:readonly` | 获取用户受雇信息 |
| `join_time` | `contact:user.employee:readonly` | 获取用户受雇信息 |
| `is_tenant_manager` | `contact:user.employee:readonly` | 获取用户受雇信息 |
| `employee_no` | `contact:user.employee_number:read` | 查看成员工号 |
| `employee_type` | `contact:user.employee:readonly` | 获取用户受雇信息 |
| `orders` | `contact:user.department:readonly` | 获取用户组织架构信息 |
| `custom_attrs` | `contact:user.employee:readonly` | 获取用户受雇信息 |
| `enterprise_email` | `contact:user.employee:readonly` | 获取用户受雇信息 |
| `job_title` | `contact:user.employee:readonly` | 获取用户受雇信息 |
| `geo` | `contact:user.user_geo` | 查看成员数据驻留地 |
| `job_level_id` | `contact:user.job_level:readonly` | 查询用户职级 |
| `job_family_id` | `contact:user.job_family:readonly` | 查询用户所属的工作序列 |
| `assign_info` | `contact:user.assign_info:read` | 查询用户席位信息 |
| `department_path` | `contact:user.department_path:readonly` | 获取成员所在部门路径 |
| `dotted_line_leader_user_ids` | `contact:user.dotted_line_leader_info.read` | 查看成员的虚线上级 ID |

## 请求参数

### 请求头

| 名称 | 类型 | 必填 | 描述 |
|------|------|------|------|
| `Authorization` | string | 是 | `tenant_access_token` 或 `user_access_token`<br>值格式："Bearer `access_token`"<br>示例值："Bearer u-7f1bcd13fc57d46bac21793a18e560"<br>**了解更多**：[如何选择与获取 access token](https://open.feishu.cn/document/uAjLw4CM/ugTN1YjL4UTN24CO1UjN/trouble-shooting/how-to-choose-which-type-of-token-to-use) |

### 路径参数

| 名称 | 类型 | 描述 |
|------|------|------|
| `user_id` | string | 用户ID。ID 类型与查询参数 `user_id_type` 保持一致。<br>示例值："7be5fg9a" |

### 查询参数

| 参数名 | 类型 | 必填 | 描述 |
|--------|------|------|------|
| `user_id_type` | string | 否 | 用户 ID 类型<br>可选值：<br>- `open_id`：标识一个用户在某个应用中的身份<br>- `union_id`：标识一个用户在某个应用开发商下的身份<br>- `user_id`：标识一个用户在某个租户内的身份<br>默认值：`open_id`<br>当值为 `user_id`，字段权限要求：`contact:user.employee_id:readonly` |
| `department_id_type` | string | 否 | 指定查询结果中的部门 ID 类型<br>可选值：<br>- `department_id`：支持用户自定义配置的部门 ID<br>- `open_department_id`：由系统自动生成的部门 ID<br>默认值：`open_department_id` |

## 响应格式

### 响应体

| 名称 | 类型 | 描述 |
|------|------|------|
| `code` | int | 错误码，非 0 表示失败 |
| `msg` | string | 错误描述 |
| `data` | object | 响应数据 |
| `data.user` | object | 用户信息 |

### user 对象

| 字段 | 类型 | 描述 | 字段权限要求 |
|------|------|------|-------------|
| `union_id` | string | 用户的 union_id | `contact:contact:readonly` 或 `contact:contact:access_as_app` |
| `user_id` | string | 用户的 user_id | `contact:user.employee_id:readonly` |
| `open_id` | string | 用户的 open_id | `contact:contact:readonly` 或 `contact:contact:access_as_app` |
| `name` | string | 用户名称（默认名称） | `contact:user.base:readonly` |
| `en_name` | string | 英文名 | `contact:user.base:readonly` |
| `nickname` | string | 别名 | `contact:user.base:readonly` |
| `email` | string | 邮箱 | `contact:user.email:readonly` |
| `mobile` | string | 手机号 | `contact:user.phone:readonly` |
| `mobile_visible` | boolean | 手机号码是否可见 | - |
| `gender` | int | 性别（0:保密, 1:男, 2:女, 3:其他） | `contact:user.gender:readonly` |
| `avatar` | avatar_info | 用户头像信息 | `contact:user.base:readonly` |
| `status` | user_status | 用户状态 | `contact:user.employee:readonly` |
| `department_ids` | string[] | 用户所属部门的 ID 列表 | `contact:user.department:readonly` |
| `leader_user_id` | string | 用户的直接主管的用户ID | `contact:user.department:readonly` |
| `city` | string | 工作城市 | `contact:user.employee:readonly` |
| `country` | string | 国家或地区 Code 缩写 | `contact:user.employee:readonly` |
| `work_station` | string | 工位 | `contact:user.employee:readonly` |
| `join_time` | int | 入职时间 | `contact:user.employee:readonly` |
| `is_tenant_manager` | boolean | 是否为租户超级管理员 | `contact:user.employee:readonly` |
| `employee_no` | string | 工号 | `contact:user.employee_number:read` |
| `employee_type` | int | 员工类型 | `contact:user.employee:readonly` |
| `orders` | user_order[] | 用户排序信息 | `contact:user.department:readonly` |
| `custom_attrs` | user_custom_attr[] | 自定义字段 | `contact:user.employee:readonly` |
| `enterprise_email` | string | 企业邮箱 | `contact:user.employee:readonly` |
| `job_title` | string | 职务 | `contact:user.employee:readonly` |
| `geo` | string | 数据驻留地 | `contact:user.user_geo` |
| `job_level_id` | string | 职级 ID | `contact:user.job_level:readonly` |
| `job_family_id` | string | 序列 ID | `contact:user.job_family:readonly` |
| `assign_info` | user_assign_info[] | 用户席位列表 | `contact:user.assign_info:read` |
| `department_path` | department_detail[] | 部门路径列表 | `contact:user.department_path:readonly` |
| `dotted_line_leader_user_ids` | string[] | 虚线上级的用户 ID | `contact:user.dotted_line_leader_info.read` |

## 请求示例

### 获取指定用户

```bash
curl -X GET 'https://open.feishu.cn/open-apis/contact/v3/users/7be5fg9a' \
  -H 'Authorization: Bearer tenant_access_token'
```

### 使用 user_id 类型获取用户

```bash
curl -X GET 'https://open.feishu.cn/open-apis/contact/v3/users/7be5fg9a?user_id_type=user_id' \
  -H 'Authorization: Bearer tenant_access_token'
```

### 获取指定部门 ID 类型的部门信息

```bash
curl -X GET 'https://open.feishu.cn/open-apis/contact/v3/users/7be5fg9a?department_id_type=department_id' \
  -H 'Authorization: Bearer tenant_access_token'
```

## 响应体示例

```json
{
    "code": 0,
    "msg": "success",
    "data": {
        "user": {
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
            "geo": "cn",
            "job_level_id": "mga5oa8ayjlp9rb",
            "job_family_id": "mga5oa8ayjlp9rb",
            "assign_info": [
                {
                    "subscription_id": "7079609167680782300",
                    "license_plan_key": "suite_enterprise_e5",
                    "product_name": "旗舰版 E5",
                    "i18n_name": {
                        "zh_cn": "zh_cn_name",
                        "ja_jp": "ja_jp_name",
                        "en_us": "en_name"
                    },
                    "start_time": "1674981000",
                    "end_time": "1674991000"
                }
            ],
            "department_path": [
                {
                    "department_id": "od-4e6ac4d14bcd5071a37a39de902c7141",
                    "department_name": {
                        "name": "测试部门名1",
                        "i18n_name": {
                            "zh_cn": "测试部门名1",
                            "ja_jp": "試験部署名 1",
                            "en_us": "Testing department name 1"
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
                                "en_us": "Testing department name 1"
                            }
                        }
                    }
                }
            ],
            "dotted_line_leader_user_ids": [
                "ou_7dab8a3d3cdcc9da365777c7ad535d62"
            ]
        }
    }
}
```

## 错误码

| HTTP 状态码 | 错误码 | 描述 | 排查建议 |
|------------|--------|------|----------|
| 400 | 41050 | no user authority | 无用户权限 |
| 400 | 40001 | invalid parameter | 参数错误 |
| 400 | 41012 | user id invalid error | 用户 ID 无效 |
| 400 | 40003 | internal error | 内部错误 |

## 相关链接

### 权限配置

- [用户相关的 ID 概念](https://open.feishu.cn/document/home/user-identity-introduction/introduction)
- [部门 ID 说明](https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/reference/contact-v3/department/field-overview)
- [权限范围校验](https://open.feishu.cn/document/ukTMukTMukTM/uETNz4SM1MjLxUzM/v3/guides/scope_authority)

### API 文档

- [搜索用户](https://open.feishu.cn/document/ukTMukTMukTM/uMTM4UjLzEDO14yMxgTN)
- [通过手机号或邮箱获取用户 ID](https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/reference/contact-v3/user/batch_get_id)
- [获取人员类型](https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/reference/contact-v3/employee_type_enum/list)
- [自定义字段资源介绍](https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/reference/contact-v3/custom_attr/overview)
- [通用错误码](https://open.feishu.cn/document/ukTMukTMukTM/ugjM14COyUjL4ITN)
