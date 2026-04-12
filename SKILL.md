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

## 待办

- [ ] 记录更多飞书 API 文档
- [ ] 补充权限配置说明
- [ ] 创建自动化脚本模板