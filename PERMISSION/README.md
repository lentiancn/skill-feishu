# permission - 飞书权限配置指南

这个目录存放飞书 API 的权限配置说明。

## 权限分类

| 权限 | 说明 |
|------|------|
| `API_PERMISSIONS.md` | API 权限配置清单 |
| `FIELDS.md` | 字段权限与所需权限对应表 |
| `DEPARTMENT_ACCESS.md` | 部门访问权限配置 |

## App 配置

- **App ID**: `cli_a951a619cc611bef`
- **App Secret**: `Sdo1mO1ekr3WJe5wxsZCwgQ7HZv8NOIL`

## 权限配置步骤

1. 访问 [飞书开放平台](https://open.feishu.cn/)
2. 进入你的应用
3. 在「应用权限」→「通讯录权限」中配置
4. 在「部门可见范围」中配置可访问的部门

## 常见权限

| 权限 | 说明 |
|------|------|
| `contact:user:readonly` | 读取用户信息 |
| `contact:department:readonly` | 读取部门信息 |
| `contact:user.employee_id:readonly` | 读取用户工号 |
| `contact:user.base:readonly` | 读取用户基础信息 |
