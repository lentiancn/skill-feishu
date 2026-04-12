# API 权限配置清单

## 用户相关 API

| API | 所需权限 |
|-----|---------|
| 获取用户列表 | `contact:contact:readonly` 或 `contact:contact:access_as_app` |
| 获取用户详情 | `contact:contact:readonly` 或 `contact:contact:access_as_app` |
| 获取部门用户 | `contact:contact:readonly` 或 `contact:contact:access_as_app` |

## 部门相关 API

| API | 所需权限 |
|-----|---------|
| 获取部门列表 | `contact:department:readonly` |
| 获取部门详情 | `contact:department:readonly` |

## 字段权限

| 字段 | 所需权限 |
|------|---------|
| name | `contact:user.base:readonly` |
| mobile | `contact:user.mobile:readonly` |
| email | `contact:user.email:readonly` |
| user_id | `contact:user.employee_id:readonly` |
| department_ids | `contact:department:readonly` |

## 部门可见范围

在「部门可见范围」中配置要查看的部门 ID，根部门为 `0`。
