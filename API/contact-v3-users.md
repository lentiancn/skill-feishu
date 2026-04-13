# 获取用户列表

## 注意事项

- 本接口已为历史版本，不再维护更新，不推荐使用。推荐你使用[获取部门直属用户列表](https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/reference/contact-v3/user/find_by_department)接口。
- 使用 user_access_token 情况下根据个人组织架构的通讯录可见范围进行权限过滤，返回个人组织架构通讯录范围（[登陆企业管理后台进行权限配置](https://www.feishu.cn/admin/security/permission/visibility)）内可见的用户数据。
- 使用 tenant_access_token 基于应用通讯录范围进行权限鉴定：
  - 请求设置了 department_id（根部门为0），会检验所带部门ID是否具有通讯录权限（如果带上 department_id=0 会校验是否有全员权限），有则返回部门下直属的成员列表，否则提示无部门权限的错误码返回。
  - 请求未带 department_id 参数，则会返回权限范围内的独立用户。

## 权限要求

### 必要权限

| 类型 | 名称 |
|----------|----------|
| 应用权限（开启任一即可） | 获取部门组织架构信息 (contact:department.organize:readonly) |
| 应用权限（开启任一即可） | 以应用身份读取通讯录 (contact:contact:readonly_as_app) |
| 应用权限（开启任一即可） | 读取通讯录 (contact:contact:readonly) |
| 应用权限（开启任一即可） | 以应用身份访问通讯录 (contact:contact:access_as_app) |

### 可选权限

| 类型 | 名称 |
|----------|----------|
| 字段权限（敏感字段） | 获取用户基本信息 (contact:user.base:readonly) |
| 字段权限（敏感字段） | 以应用身份读取通讯录 (contact:contact:readonly_as_app) |
| 字段权限（敏感字段） | 获取用户雇佣信息 (contact:user.employee:readonly) |
| 字段权限（敏感字段） | 获取用户组织架构信息 (contact:user.department:readonly) |
| 字段权限（敏感字段） | 获取用户性别 (contact:user.gender:readonly) |
| 字段权限（敏感字段） | 获取用户邮箱信息 (contact:user.email:readonly) |
| 字段权限（敏感字段） | 获取用户手机号 (contact:user.phone:readonly) |
| 字段权限（敏感字段） | 获取用户 user ID (contact:user.employee_id:readonly) |

> **说明**：敏感字段仅在开启对应权限后才会返回；如无需获取这些字段，不建议申请。

## 接口信息

| API 路径 | `https://open.feishu.cn/open-apis/contact/v3/users` |
|----------|-----------------------------------------------------|
| 请求方法 | GET |
| 调用频率限制 | 1000 次/分钟、50 次/秒 |
| 支持的应用类型 | Custom App、Store App |
| 文档地址 | [飞书开放平台](https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/reference/contact-v3/user/list) |

## 接口请求

### 请求头

HTTP 请求头字段，用于身份认证和内容类型声明。

| 名称 | 类型 | 必填 | 描述 |
|------|------|------|------|
| `Authorization` | string | 是 | `tenant_access_token` 或 `user_access_token`<br>值格式："Bearer `access_token`"<br>示例值："Bearer u-7f1bcd13fc57d46bac21793a18e560"<br>**了解更多**：[如何选择与获取 access token](https://open.feishu.cn/document/uAjLw4CM/ugTN1YjL4UTN24CO1UjN/trouble-shooting/how-to-choose-which-type-of-token-to-use) |

### 请求参数

| 参数名 | 类型 | 必填 | 描述 |
|--------|------|------|------|
| `user_id_type` | string | 否 | 用户 ID 类型<br>可选值：<br>- `open_id`：用户的 open id<br>- `union_id`：用户的 union id<br>- `user_id`：用户的 user id<br>默认值：`open_id`<br>**字段权限**：当值为 `user_id` 时，需要获取用户 user ID (contact:user.employee_id:readonly) |
| `department_id_type` | string | 否 | 此次调用中使用的部门ID的类型<br>可选值：<br>- `department_id`：以自定义department_id来标识部门<br>- `open_department_id`：以open_department_id来标识部门<br>默认值：`open_department_id` |
| `department_id` | string | 否 | 填写该字段表示获取部门下所有用户<br>示例值："od-xxxxxxxxxxxxx" |
| `page_token` | string | 否 | 分页标记，第一次请求不填，表示从头开始遍历<br>示例值："AQD9/Rn9eij9Pm39ED40/dk53s4Ebp882DYfFaPFbz00L4CMZJrqGdzNyc8BcZtDbwVUvRmQTvyMYicnGWrde9X56TgdBuS%2BJKiSIkdexPw=" |
| `page_size` | integer | 否 | 分页大小<br>数据校验规则：<br>- 最大值：`100`<br>示例值：10 |

### 请求体

无请求体（GET 请求）

### 请求示例

```bash
curl -X GET 'https://open.feishu.cn/open-apis/contact/v3/users?department_id=od_xxx&page_size=10&page_token=AQD9/...' \
  -H 'Authorization: Bearer tenant_access_token' \
  -H 'Content-Type: application/json; charset=utf-8'
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
| `data` | object | 响应数据，根据接口类型动态变化 |

### 响应示例

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

## 响应码定义

### 成功码

| HTTP状态码 | 错误码 | 描述 |
|------------|--------|------|
| 200 | 0 | 请求成功 |

### 客户端错误码 (4xx)

| HTTP状态码 | 错误码 | 描述 |
|------------|--------|------|
| 400 | 41050 | no user authority error |
| 400 | 40011 | page size is invalid |
| 400 | 40012 | page token is invalid error |
| 403 | 40004 | no dept authority error |

## 附录

### 按需定义章节标题，例如：相关链接

| 链接类型 | 链接 |
|----------|------|
| 常见问题答疑 | [https://open.feishu.cn/document/ugTN1YjL4UTN24CO1UjN/uQzN1YjL0cTN24CN3UjN](https://open.feishu.cn/document/ugTN1YjL4UTN24CO1UjN/uQzN1YjL0cTN24CN3UjN) |
| 用户相关的 ID 概念 | [https://open.feishu.cn/document/home/user-identity-introduction/introduction](https://open.feishu.cn/document/home/user-identity-introduction/introduction) |
| 权限范围校验 | [https://open.feishu.cn/document/ukTMukTMukTM/uETNz4SM1MjLxUzM/v3/guides/scope_authority](https://open.feishu.cn/document/ukTMukTMukTM/uETNz4SM1MjLxUzM/v3/guides/scope_authority) |
| 用户接口相关问题 | [https://open.feishu.cn/document/ugTN1YjL4UTN24CO1UjN/uQzN1YjL0cTN24CN3UjN#77061525](https://open.feishu.cn/document/ugTN1YjL4UTN24CO1UjN/uQzN1YjL0cTN24CN3UjN#77061525) |
| 部门ID说明 | [https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/reference/contact-v3/department/field-overview](https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/reference/contact-v3/department/field-overview) |
| 国家/地区码表 | [https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/reference/contact-v3/user/country-code-description](https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/reference/contact-v3/user/country-code-description) |

## 许可证

### 模板说明

固定值：参考模板示例。

### 模板示例

**skill-feishu** 采用 [MIT-0 许可证](https://raw.githubusercontent.com/lentiancn/skill-feishu/refs/heads/main/LICENSE)授权。
