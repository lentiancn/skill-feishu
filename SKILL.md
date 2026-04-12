# skill-feishu - 飞书相关技能

这个技能包用于处理飞书相关操作，记录飞书 API 及权限配置。

## 包含模块

- **API** - 飞书 API 文档集合
  - README.md
  - REFERENCES.md
  - TEMPLATE.md
  - contact-v3/ - 飞书联系人 v3 API
    - README.md
    - find_by_department.md
    - get_user.md
    - users.md
  - department-v3/ - 飞书部门 API
  - user-v3/ - 飞书用户 API
- **PERMISSION** - 飞书权限配置指南
  - README.md
  - API_PERMISSIONS.md
  - DEPARTMENT_ACCESS.md
  - FIELDS.md
  - TEMPLATE.md

## 重要规则（必读）

### 🚫 严格禁止的操作

以下操作在任何情况下都**绝对禁止**，否则视为严重 BUG 和错误：

| 禁止操作 | 说明 |
|---------|------|
| **简化内容** | 任何文档、API 说明、字段描述、权限要求等**必须完整版**，禁止省略、缩写、合并 |
| **数据推算** | 禁止根据已有数据推算出不存在的信息，必须**真实记录**，没有就写"无此信息" |
| **省略示例** | 请求示例、响应示例、错误码示例等**必须完整**，禁止省略部分行 |
| **偷懒操作** | 不得跳过必填字段说明、参数说明等文档内容 |
| **模糊处理** | 所有字段说明、权限要求、参数说明必须清晰完整，不可模糊 |

### 违反规则的严重性

违反上述任何一条规则，均视为：
- ❌ **严重 BUG**
- ❌ **错误**
- ❌ **过错**
- ❌ **偷懒**
- ❌ **失误**

这些操作在任何情况下都不允许发生。

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
- **中文说明**：格式为 `中文内容 (权限标识)`
- **超链接**：将权限标识链接到 `PERMISSION/FIELDS.md` 中对应的权限详情
- **必须完整**：权限说明、字段说明、示例等**禁止简化**，必须保持飞书官方文档的完整性

### 字段权限说明示例

```markdown
| 字段 | 所需权限 |
|------|---------|
| `union_id` | 统一用户标识 (contact:contact:readonly) |
| `user_id` | 获取用户 user ID (contact:user.employee_id:readonly) |
```

### 字段权限要求

请查看 [PERMISSION/FIELDS.md](../PERMISSION/FIELDS.md) 获取完整的权限说明和链接。

## 权限字段说明规范（2026-04-12 更新）

### 收集信息的整理方式

1. **从飞书开放平台 API 调试台**：复制 API 文档内容，整理成 Markdown 格式
2. **从用户提供的文本**：识别出关键信息，结构化整理
3. **权限字段**：按字段分类，添加中文说明和权限标识
4. **权限链接**：所有权限标识必须链接到 `PERMISSION/FIELDS.md` 中对应的权限详情

### 注意事项

- **不要记录敏感信息**：App ID 和 App Secret 不要记录在 API 文档中
- **权限字段说明**：格式为 `中文内容 (权限标识)`，权限标识要有超链接
- **API 版本**：标注是否为历史版本，推荐使用新版本 API
- **权限校验**：说明 `user_access_token` 和 `tenant_access_token` 的不同权限校验方式
- **必须完整**：文档、示例、字段说明、权限要求等**禁止简化**，必须保持完整版

## 使用规范

- 所有文档必须保持飞书官方文档的完整性，禁止简化、省略、合并
- 所有示例必须完整展示，禁止省略部分行
- 所有字段必须完整说明权限要求，禁止推算或猜测
- 所有内容必须真实记录，禁止偷懒、失误或简化
- 避免 AI 味道：用直接、简洁、实用的表达方式，不浮夸、不玩花样、不加多余说明