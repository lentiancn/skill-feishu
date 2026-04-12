# 获取部门直属用户列表 (contact/v3/users)

## 基本信息

| 项目 | 值 |
|------|-----|
| **API 路径** | `https://open.feishu.cn/open-apis/contact/v3/users` |
| **请求方法** | GET |
| **支持的应用类型** | 自建应用、商店应用 |
| **最后更新** | 2026-04-07 |
| **状态** | 历史版本，不再维护 |
| **文档地址** | [https://open.feishu.cn/document/server-docs/historic-version//user/list](https://open.feishu.cn/document/server-docs/historic-version//user/list) |

> ⚠️ **注意**：本接口已为历史版本，不再维护更新，不推荐使用。推荐你使用 [获取部门直属用户列表](https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/reference/contact-v3/user/find_by_department) 接口。
> 
> 📚 **文档地址**: [历史版本用户列表 API 文档](https://open.feishu.cn/document/server-docs/historic-version//user/list)
> 
> 🔗 **权限相关链接**：
> - [用户相关的 ID 概念](https://open.feishu.cn/document/home/user-identity-introduction/introduction)
> - [部门 ID 说明](https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/reference/contact-v3/department/field-overview)
> - [权限范围校验](https://open.feishu.cn/document/ukTMukTMukTM/uETNz4SM1MjLxUzM/v3/guides/scope_authority)
> - [通讯录权限配置](https://open.feishu.cn/document/ugTN1YjL4UTN24CO1UjN/uQzN1YjL0cTN24CN3UjN)

## 权限要求

开启任一权限即可：

- **获取部门组织架构信息** - [以应用身份读取通讯录](https://open.feishu.cn/document/ugTN1YjL4UTN24CO1UjN/uQzN1YjL0cTN24CN3UjN)
- **读取通讯录** - [历史版本](https://open.feishu.cn/document/ugTN1YjL4UTN24CO1UjN/uQzN1YjL0cTN24CN3UjN)
- **以应用身份访问通讯录** - [历史版本](https://open.feishu.cn/document/ugTN1YjL4UTN24CO1UjN/uQzN1YjL0cTN24CN3UjN)

### 字段权限要求

| 字段 | 权限要求 | 权限页面链接 |
|------|----------|-------------|
| union_id | [以应用身份读取通讯录](https://open.feishu.cn/document/ugTN1YjL4UTN24CO1UjN/uQzN1YjL0cTN24CN3UjN) | [配置权限](https://open.feishu.cn/document/ugTN1YjL4UTN24CO1UjN/uQzN1YjL0cTN24CN3UjN) |
| user_id | [仅自建应用 - 获取用户 user ID](https://open.feishu.cn/document/ugTN1YjL4UTN24CO1UjN/uQzN1YjL0cTN24CN3UjN) | [配置权限](https://open.feishu.cn/document/ugTN1YjL4UTN24CO1UjN/uQzN1YjL0cTN24CN3UjN) |
| open_id | [以应用身份读取通讯录](https://open.feishu.cn/document/ugTN1YjL4UTN24CO1UjN/uQzN1YjL0cTN24CN3UjN) | [配置权限](https://open.feishu.cn/document/ugTN1YjL4UTN24CO1UjN/uQzN1YjL0cTN24CN3UjN) |
| name | [以应用身份读取通讯录](https://open.feishu.cn/document/ugTN1YjL4UTN24CO1UjN/uQzN1YjL0cTN24CN3UjN) | [配置权限](https://open.feishu.cn/document/ugTN1YjL4UTN24CO1UjN/uQzN1YjL0cTN24CN3UjN) |
| en_name | [以应用身份读取通讯录](https://open.feishu.cn/document/ugTN1YjL4UTN24CO1UjN/uQzN1YjL0cTN24CN3UjN) | [配置权限](https://open.feishu.cn/document/ugTN1YjL4UTN24CO1UjN/uQzN1YjL0cTN24CN3UjN) |
| email | [仅自建应用 - 获取用户邮箱信息](https://open.feishu.cn/document/ugTN1YjL4UTN24CO1UjN/uQzN1YjL0cTN24CN3UjN) | [配置权限](https://open.feishu.cn/document/ugTN1YjL4UTN24CO1UjN/uQzN1YjL0cTN24CN3UjN) |
| mobile | [仅自建应用 - 获取用户手机号](https://open.feishu.cn/document/ugTN1YjL4UTN24CO1UjN/uQzN1YjL0cTN24CN3UjN) | [配置权限](https://open.feishu.cn/document/ugTN1YjL4UTN24CO1UjN/uQzN1YjL0cTN24CN3UjN) |
| gender | [以应用身份读取通讯录](https://open.feishu.cn/document/ugTN1YjL4UTN24CO1UjN/uQzN1YjL0cTN24CN3UjN) | [配置权限](https://open.feishu.cn/document/ugTN1YjL4UTN24CO1UjN/uQzN1YjL0cTN24CN3UjN) |
| avatar | [以应用身份读取通讯录](https://open.feishu.cn/document/ugTN1YjL4UTN24CO1UjN/uQzN1YjL0cTN24CN3UjN) | [配置权限](https://open.feishu.cn/document/ugTN1YjL4UTN24CO1UjN/uQzN1YjL0cTN24CN3UjN) |
| status | [以应用身份读取通讯录](https://open.feishu.cn/document/ugTN1YjL4UTN24CO1UjN/uQzN1YjL0cTN24CN3UjN) | [配置权限](https://open.feishu.cn/document/ugTN1YjL4UTN24CO1UjN/uQzN1YjL0cTN24CN3UjN) |
| department_ids | [以应用身份读取通讯录](https://open.feishu.cn/document/ugTN1YjL4UTN24CO1UjN/uQzN1YjL0cTN24CN3UjN) | [配置权限](https://open.feishu.cn/document/ugTN1YjL4UTN24CO1UjN/uQzN1YjL0cTN24CN3UjN) |
| leader_user_id | [以应用身份读取通讯录](https://open.feishu.cn/document/ugTN1YjL4UTN24CO1UjN/uQzN1YjL0cTN24CN3UjN) | [配置权限](https://open.feishu.cn/document/ugTN1YjL4UTN24CO1UjN/uQzN1YjL0cTN24CN3UjN) |
| city | [以应用身份读取通讯录](https://open.feishu.cn/document/ugTN1YjL4UTN24CO1UjN/uQzN1YjL0cTN24CN3UjN) | [配置权限](https://open.feishu.cn/document/ugTN1YjL4UTN24CO1UjN/uQzN1YjL0cTN24CN3UjN) |
| country | [以应用身份读取通讯录](https://open.feishu.cn/document/ugTN1YjL4UTN24CO1UjN/uQzN1YjL0cTN24CN3UjN) | [配置权限](https://open.feishu.cn/document/ugTN1YjL4UTN24CO1UjN/uQzN1YjL0cTN24CN3UjN) |
| work_station | [以应用身份读取通讯录](https://open.feishu.cn/document/ugTN1YjL4UTN24CO1UjN/uQzN1YjL0cTN24CN3UjN) | [配置权限](https://open.feishu.cn/document/ugTN1YjL4UTN24CO1UjN/uQzN1YjL0cTN24CN3UjN) |
| join_time | [以应用身份读取通讯录](https://open.feishu.cn/document/ugTN1YjL4UTN24CO1UjN/uQzN1YjL0cTN24CN3UjN) | [配置权限](https://open.feishu.cn/document/ugTN1YjL4UTN24CO1UjN/uQzN1YjL0cTN24CN3UjN) |
| is_tenant_manager | [以应用身份读取通讯录](https://open.feishu.cn/document/ugTN1YjL4UTN24CO1UjN/uQzN1YjL0cTN24CN3UjN) | [配置权限](https://open.feishu.cn/document/ugTN1YjL4UTN24CO1UjN/uQzN1YjL0cTN24CN3UjN) |
| employee_no | [以应用身份读取通讯录](https://open.feishu.cn/document/ugTN1YjL4UTN24CO1UjN/uQzN1YjL0cTN24CN3UjN) | [配置权限](https://open.feishu.cn/document/ugTN1YjL4UTN24CO1UjN/uQzN1YjL0cTN24CN3UjN) |
| employee_type | [以应用身份读取通讯录](https://open.feishu.cn/document/ugTN1YjL4UTN24CO1UjN/uQzN1YjL0cTN24CN3UjN) | [配置权限](https://open.feishu.cn/document/ugTN1YjL4UTN24CO1UjN/uQzN1YjL0cTN24CN3UjN) |
| orders | [以应用身份读取通讯录](https://open.feishu.cn/document/ugTN1YjL4UTN24CO1UjN/uQzN1YjL0cTN24CN3UjN) | [配置权限](https://open.feishu.cn/document/ugTN1YjL4UTN24CO1UjN/uQzN1YjL0cTN24CN3UjN) |
| custom_attrs | [以应用身份读取通讯录](https://open.feishu.cn/document/ugTN1YjL4UTN24CO1UjN/uQzN1YjL0cTN24CN3UjN) | [配置权限](https://open.feishu.cn/document/ugTN1YjL4UTN24CO1UjN/uQzN1YjL0cTN24CN3UjN) |
| enterprise_email | [仅自建应用 - 获取用户邮箱信息](https://open.feishu.cn/document/ugTN1YjL4UTN24CO1UjN/uQzN1YjL0cTN24CN3UjN) | [配置权限](https://open.feishu.cn/document/ugTN1YjL4UTN24CO1UjN/uQzN1YjL0cTN24CN3UjN) |
| job_title | [以应用身份读取通讯录](https://open.feishu.cn/document/ugTN1YjL4UTN24CO1UjN/uQzN1YjL0cTN24CN3UjN) | [配置权限](https://open.feishu.cn/document/ugTN1YjL4UTN24CO1UjN/uQzN1YjL0cTN24CN3UjN) |

### 权限配置说明

点击上方的【配置权限】链接，进入飞书开放平台的权限配置页面：
1. 登录 [飞书开放平台](https://open.feishu.cn/)
2. 进入你的应用
3. 在「应用权限」→「通讯录权限」中找到对应权限
4. 开启权限并配置部门可见范围

## 请求参数

| 参数名 | 类型 | 必填 | 描述 |
|--------|------|------|------|
| `Authorization` | string | 是 | `tenant_access_token` 或 `user_access_token`，格式："Bearer access_token" |
| `user_id_type` | string | 否 | 用户 ID 类型（open_id/union_id/user_id），默认：open_id |
| `department_id_type` | string | 否 | 部门 ID 类型（department_id/open_department_id），默认：open_department_id |
| `department_id` | string | 否 | 部门 ID，获取该部门下的用户 |
| `page_token` | string | 否 | 分页标记，第一次请求不填 |
| `page_size` | int | 否 | 分页大小（1-100），默认：10 |

## 响应格式

```json
{
  "code": 0,
  "msg": "success",
  "data": {
    "has_more": false,
    "page_token": "AQD9/...",
    "items": [
      {
        "union_id": "on_xxx",
        "user_id": "xxx",
        "open_id": "ou_xxx",
        "name": "张三",
        "en_name": "San Zhang",
        "email": "zhangsan@gmail.com",
        "mobile": "130xxxx1111",
        "mobile_visible": false,
        "gender": 1,
        "avatar": {
          "avatar_72": "https://...",
          "avatar_240": "https://...",
          "avatar_640": "https://...",
          "avatar_origin": "https://..."
        },
        "status": {
          "is_frozen": false,
          "is_resigned": false,
          "is_activated": true
        },
        "department_ids": ["od_xxx"],
        "leader_user_id": "ou_xxx",
        "city": "杭州",
        "country": "CN",
        "work_station": "北楼-H34",
        "join_time": 2147483647,
        "is_tenant_manager": false,
        "employee_no": "1",
        "employee_type": 1,
        "orders": [
          {
            "department_id": "od_xxx",
            "user_order": 100,
            "department_order": 100
          }
        ],
        "custom_attrs": [...],
        "enterprise_email": "demo@mail.com",
        "job_title": "xxxxx"
      }
    ]
  }
}
```

## 响应字段说明

### data 对象

| 字段 | 类型 | 描述 |
|------|------|------|
| `has_more` | boolean | 是否还有更多项 |
| `page_token` | string | 分页标记，当 has_more 为 true 时返回 |
| `items` | array | 用户列表 |

### user 对象

| 字段 | 类型 | 描述 |
|------|------|------|
| `union_id` | string | 用户的 union_id |
| `user_id` | string | 用户的 user_id |
| `open_id` | string | 用户的 open_id |
| `name` | string | 用户名 |
| `en_name` | string | 英文名 |
| `email` | string | 邮箱 |
| `mobile` | string | 手机号 |
| `mobile_visible` | boolean | 手机号可见性 |
| `gender` | int | 性别（0:保密, 1:男, 2:女） |
| `avatar` | object | 用户头像信息 |
| `status` | object | 用户状态 |
| `department_ids` | array | 用户所属部门 ID 列表 |
| `leader_user_id` | string | 直接主管的 open_id |
| `city` | string | 工作城市 |
| `country` | string | 国家/地区码 |
| `work_station` | string | 工位 |
| `join_time` | int | 入职时间（秒级时间戳） |
| `is_tenant_manager` | boolean | 是否是租户超级管理员 |
| `employee_no` | string | 工号 |
| `employee_type` | int | 员工类型 |
| `orders` | array | 用户排序信息 |
| `custom_attrs` | array | 自定义字段 |
| `enterprise_email` | string | 企业邮箱 |
| `job_title` | string | 职务 |

## 请求示例

### 获取根部门（部门ID=0）下的所有用户

```bash
curl -X GET 'https://open.feishu.cn/open-apis/contact/v3/users?department_id=0' \
  -H 'Authorization: Bearer tenant_access_token'
```

### 分页获取用户列表

```bash
curl -X GET 'https://open.feishu.cn/open-apis/contact/v3/users?department_id=od_xxx&page_size=10&page_token=AQD9/...' \
  -H 'Authorization: Bearer tenant_access_token'
```

## 错误码

| HTTP 状态码 | 错误码 | 描述 | 排查建议 |
|------------|--------|------|----------|
| 400 | 41050 | no user authority error | [操作的用户需在通讯录权限范围中](https://open.feishu.cn/document/ukTMukTMukTM/uETNz4SM1MjLxUzM/v3/guides/scope_authority) |
| 400 | 40011 | page size is invalid | 无效的分页参数 |
| 400 | 40012 | page token is invalid error | page token 无效 |
| 403 | 40004 | no dept authority error | [操作的部门需在通讯录权限范围中](https://open.feishu.cn/document/ukTMukTMukTM/uETNz4SM1MjLxUzM/v3/guides/scope_authority) |

## 相关链接

- [用户相关的 ID 概念](https://open.feishu.cn/document/home/user-identity-introduction/introduction)
- [部门 ID 说明](https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/reference/contact-v3/department/field-overview)
- [权限范围校验](https://open.feishu.cn/document/ukTMukTMukTM/uETNz4SM1MjLxUzM/v3/guides/scope_authority)
- [通讯录权限配置](https://open.feishu.cn/document/ugTN1YjL4UTN24CO1UjN/uQzN1YjL0cTN24CN3UjN)
