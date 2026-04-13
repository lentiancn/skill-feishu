# API 模板文档

## 说明

这是 API 文档模板。使用此模板创建新的 API 文档时，请严格遵守以下结构和格式。

## 结构

- **注意事项**
- **权限要求**
  - 必要权限
  - 可选权限
- **接口信息**
- **接口请求**
  - 请求头
  - 请求参数
  - 请求体
  - 请求示例
- **接口响应**
  - 响应头
  - 响应体
  - 响应示例
- **错误码**
- **排查思路**
- **相关链接**

## 注意事项

- 所有文档必须保持飞书官方文档的完整性，禁止简化、省略、合并
- 所有示例必须完整展示，禁止省略部分行
- 所有字段必须完整说明权限要求，禁止推算或猜测
- 所有内容必须真实记录，禁止偷懒、失误或简化

##表格格式说明

### 权限要求表格格式

权限要求分为两个表格：**必要权限**和**可选权限**。

#### 必要权限表格格式

```markdown
### 必要权限

| 类型 | 名称 |
|------|------|
| 应用权限（开启任一即可） | 获取通讯录基本信息 (contact:contact.base:readonly) |
| 应用权限（开启任一即可） | 获取通讯录部门组织架构信息 (contact:department.organize:readonly) |
```

#### 可选权限表格格式

```markdown
### 可选权限

| 类型 | 名称 |
|------|------|
| 字段权限（敏感字段） | 统一用户标识 (contact:user.base:readonly) |
| 字段权限（敏感字段） | 获取用户 user ID (contact:user.employee_id:readonly) |
```

### 接口信息表格格式

```markdown
## 接口信息

| 参数名 | 值 |
|--------|-----|
| API 路径 | `https://open.feishu.cn/open-apis/...` |
| 请求方法 | GET |
| 调用频率限制 | 1000 次/分钟、50 次/秒 |
| 支持的应用类型 | Custom App、Store App |
| 文档地址 | [飞书开放平台](https://open.feishu.cn/...) |
```

### 请求头表格格式

```markdown
### 请求头

| 名称 | 类型 | 必填 | 描述 |
|------|------|------|------|
| `Authorization` | string | 是 | `tenant_access_token` 或 `user_access_token`<br>值格式："Bearer `access_token`"<br>示例值："Bearer ..." |
| `Content-Type` | string | 是 | 固定值："application/json; charset=utf-8" |
```

### 请求参数表格格式

```markdown
### 请求参数

| 参数名 | 类型 | 必填 | 描述 |
|--------|------|------|------|
| `param_name` | string | 否 | 参数说明<br>可选值：<br>- `value1`：说明<br>默认值：`default`<br>**权限要求**：当值为 `user_id` 时，需要 xxx (contact:xxx:xxx) |
```

### 响应体表格格式

#### 主数据对象表格

```markdown
### 响应体

| 字段 | 类型 | 描述 |
|------|------|------|
| `code` | int | 错误码，非 0 表示失败 |
| `msg` | string | 错误描述 |
| `data` | object | 响应数据 |
```

#### 嵌套对象表格（用#### 标题）

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
| `union_id` | string | 用户的 union_id...<br>**权限要求**：统一用户标识 (contact:user.base:readonly) |
| `name` | string | 用户名<br>**权限要求**：获取用户基本信息 (contact:user.base:readonly) |
| `email` | string | 邮箱<br>**权限要求**：获取用户邮箱信息 (contact:user.email:readonly) |
```

#### 简单对象表格

```markdown
#### user_status 对象

| 字段 | 类型 | 描述 |
|------|------|------|
| `is_frozen` | boolean | 是否为暂停状态 |
| `is_resigned` | boolean | 是否为离职状态 |
```

### 错误码表格格式

```markdown
## 错误码

| HTTP状态码 | 错误码 | 描述 | 排查建议 |
|------------|--------|------|----------|
| 400 | 41050 | no user authority error | 无用户权限。需将当前操作的用户添加到应用或用户的权限范围内 |
| 400 | 40011 | page size is invalid | 无效的分页参数。page_size 的取值上限为 50 |
```

### 排错思路表格格式

排错思路表格格式与错误码表格格式相同。

### 相关链接表格格式

```markdown
## 相关链接

| 链接类型 | 链接 |
|----------|------|
| 应用权限配置 | [https://open.feishu.cn/...](https://open.feishu.cn/...) |
| 用户相关的 ID 概念 | [https://open.feishu.cn/...](https://open.feishu.cn/...) |
```

## 注意事项（重复规则）

- **禁止简化内容**：任何文档、API 说明、字段描述、权限要求等**必须完整版**，禁止省略、缩写、合并
- **禁止数据推算**：禁止根据已有数据推算出不存在的信息，必须**真实记录**，没有就写"无此信息"
- **禁止省略示例**：请求示例、响应示例、错误码示例等**必须完整**，禁止省略部分行
- **禁止偷懒操作**：不得跳过必填字段说明、参数说明等文档内容
- **禁止模糊处理**：所有字段说明、权限要求、参数说明必须清晰完整，不可模糊

### 权限说明格式规范

#### 在请求参数或响应字段中添加权限要求

```markdown
| 字段 | 类型 | 描述 |
|------|------|------|
| `user_id` | string | 用户的 user_id，租户内用户的唯一标识<br>**权限要求**：获取用户 user ID (contact:user.employee_id:readonly) |
| `email` | string | 邮箱<br>**权限要求**：获取用户邮箱信息 (contact:user.email:readonly) |
```

#### 多个权限（满足任一）的说明格式

```markdown
| 字段 | 类型 | 描述 |
|------|------|------|
| `name` | string | 用户名<br>**权限要求（满足任一）**：<br>获取用户基本信息 (contact:user.base:readonly)<br>以应用身份访问通讯录 (contact:contact:access_as_app)<br>读取通讯录 (contact:contact:readonly)<br>以应用身份读取通讯录 (contact:contact:readonly_as_app) |
```

## 使用规范

- 所有文档必须保持飞书官方文档的完整性，禁止简化、省略、合并
- 所有示例必须完整展示，禁止省略部分行
- 所有字段必须完整说明权限要求，禁止推算或猜测
- 所有内容必须真实记录，禁止偷懒、失误或简化
- **禁止擅自发挥**：不允许对原始内容进行任何未明确要求的修改、改名、结构调整
- **禁止理解偏差**：如有不明确之处，必须向用户确认后再操作
- **必须认真仔细**：每一步操作都要核对原始文档，确保准确无误
