# skill-feishu - 飞书相关技能

这个技能包用于处理飞书相关操作，记录飞书 API 及权限配置。

## 包含模块

- **API** - 飞书 API 文档集合
- **Permission** - 飞书权限配置指南
- **Scripts** - 自动化脚本

## 使用说明

每个模块有自己的 README，可查看详细说明。

## App 配置

⚠️ **安全提示**：应用凭证应存储在环境变量或配置文件中，不要硬编码在代码中。

## 权限链接规范

⚠️ **重要**：所有 API 文档中涉及权限相关的描述，必须包含以下链接：

| 权限类型 | 链接 |
|---------|------|
| 应用权限配置 | [https://open.feishu.cn/document/ugTN1YjL4UTN24CO1UjN/uQzN1YjL0cTN24CN3UjN](https://open.feishu.cn/document/ugTN1YjL4UTN24CO1UjN/uQzN1YjL0cTN24CN3UjN) |
| 用户相关的 ID 概念 | [https://open.feishu.cn/document/home/user-identity-introduction/introduction](https://open.feishu.cn/document/home/user-identity-introduction/introduction) |
| 部门 ID 说明 | [https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/reference/contact-v3/department/field-overview](https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/reference/contact-v3/department/field-overview) |
| 权限范围校验 | [https://open.feishu.cn/document/ukTMukTMukTM/uETNz4SM1MjLxUzM/v3/guides/scope_authority](https://open.feishu.cn/document/ukTMukTMukTM/uETNz4SM1MjLxUzM/v3/guides/scope_authority) |

## 记录规则

1. **API 文档** - 每个 API 文件必须包含权限要求小节
2. **字段权限** - 涉及敏感字段时，必须标注所需权限及链接
3. **错误码** - 权限错误（如 40004, 41050）必须包含权限排查链接
4. **配置说明** - 权限配置步骤必须包含飞书后台操作指引

## 权限字段说明规范（2026-04-12 更新）

### 字段权限要求格式

- **权限标识**：使用飞书开放平台的标准权限标识
- **中文说明**：格式为 `中文内容(权限标识)`
- **超链接**：将权限标识链接到 `PERMISSION/FIELDS.md` 中对应的权限详情

### 字段权限说明示例

```markdown
| 字段 | 所需权限 |
|------|---------|
| `union_id` | 统一用户标识(权限标识) | 统一用户标识 |
| `user_id` | 获取用户 user ID(权限标识) | 用户的 user_id |
```

### 字段权限要求

| 字段 | 所需权限 |
|------|---------|
| `union_id` | [统一用户标识（应用开发商下的用户标识）\(contact:contact:readonly 或 contact:contact:access_as_app\)](./PERMISSION/FIELDS.md#union_id) |
| `user_id` | [获取用户 user ID\(contact:user.employee_id:readonly\)](./PERMISSION/FIELDS.md#user_id) |
| `open_id` | [应用内用户标识\(contact:contact:readonly 或 contact:contact:access_as_app\)](./PERMISSION/FIELDS.md#open_id) |
| `name` | [获取用户基本信息\(contact:user.base:readonly\)](./PERMISSION/FIELDS.md#name) |
| `en_name` | [获取用户基本信息\(contact:user.base:readonly\)](./PERMISSION/FIELDS.md#en_name) |
| `nickname` | [获取用户基本信息\(contact:user.base:readonly\)](./PERMISSION/FIELDS.md#nickname) |
| `email` | [获取用户邮箱信息\(contact:user.email:readonly\)](./PERMISSION/FIELDS.md#email) |
| `mobile` | [获取用户手机号\(contact:user.phone:readonly\)](./PERMISSION/FIELDS.md#mobile) |
| `gender` | [获取用户性别\(contact:user.gender:readonly\)](./PERMISSION/FIELDS.md#gender) |
| `avatar` | [获取用户基本信息\(contact:user.base:readonly\)](./PERMISSION/FIELDS.md#avatar) |
| `status` | [获取用户受雇信息\(contact:user.employee:readonly\)](./PERMISSION/FIELDS.md#status) |
| `department_ids` | [获取用户组织架构信息\(contact:user.department:readonly\)](./PERMISSION/FIELDS.md#department_ids) |
| `leader_user_id` | [获取用户组织架构信息\(contact:user.department:readonly\)](./PERMISSION/FIELDS.md#leader_user_id) |
| `city` | [获取用户受雇信息\(contact:user.employee:readonly\)](./PERMISSION/FIELDS.md#city) |
| `country` | [获取用户受雇信息\(contact:user.employee:readonly\)](./PERMISSION/FIELDS.md#country) |
| `work_station` | [获取用户受雇信息\(contact:user.employee:readonly\)](./PERMISSION/FIELDS.md#work_station) |
| `join_time` | [获取用户受雇信息\(contact:user.employee:readonly\)](./PERMISSION/FIELDS.md#join_time) |
| `is_tenant_manager` | [获取用户受雇信息\(contact:user.employee:readonly\)](./PERMISSION/FIELDS.md#is_tenant_manager) |
| `employee_no` | [查看成员工号\(contact:user.employee_number:read\)](./PERMISSION/FIELDS.md#employee_no) |
| `employee_type` | [获取用户受雇信息\(contact:user.employee:readonly\)](./PERMISSION/FIELDS.md#employee_type) |
| `orders` | [获取用户组织架构信息\(contact:user.department:readonly\)](./PERMISSION/FIELDS.md#orders) |
| `custom_attrs` | [获取用户受雇信息\(contact:user.employee:readonly\)](./PERMISSION/FIELDS.md#custom_attrs) |
| `enterprise_email` | [获取用户受雇信息\(contact:user.employee:readonly\)](./PERMISSION/FIELDS.md#enterprise_email) |
| `job_title` | [获取用户受雇信息\(contact:user.employee:readonly\)](./PERMISSION/FIELDS.md#job_title) |
| `geo` | [查看成员数据驻留地\(contact:user.user_geo\)](./PERMISSION/FIELDS.md#geo) |
| `job_level_id` | [查询用户职级\(contact:user.job_level:readonly\)](./PERMISSION/FIELDS.md#job_level_id) |
| `job_family_id` | [查询用户所属的工作序列\(contact:user.job_family:readonly\)](./PERMISSION/FIELDS.md#job_family_id) |
| `department_path` | [获取成员所在部门路径\(contact:user.department_path:readonly\)](./PERMISSION/FIELDS.md#department_path) |
| `dotted_line_leader_user_ids` | [查看成员的虚线上级 ID\(contact:user.dotted_line_leader_info.read\)](./PERMISSION/FIELDS.md#dotted_line_leader_user_ids) |

## 权限字段说明规范（2026-04-12 更新）

### 收集信息的整理方式

1. **从飞书开放平台 API 调试台**：复制 API 文档内容，整理成 Markdown 格式
2. **从用户提供的文本**：识别出关键信息，结构化整理
3. **权限字段**：按字段分类，添加中文说明和权限标识
4. **权限链接**：所有权限标识必须链接到 `PERMISSION/FIELDS.md` 中对应的权限详情

### 注意事项

- **不要记录敏感信息**：App ID 和 App Secret 不要记录在 API 文档中
- **权限字段说明**：格式为 `中文内容(权限标识)`，权限标识要有超链接
- **API 版本**：标注是否为历史版本，推荐使用新版本 API
- **权限校验**：说明 `user_access_token` 和 `tenant_access_token` 的不同权限校验方式

## 待办

- [ ] 记录更多飞书 API 文档
- [ ] 补充权限配置说明
- [ ] 创建自动化脚本模板