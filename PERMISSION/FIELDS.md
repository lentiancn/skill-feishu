# 字段权限与所需权限对应表

## 权限索引

| 权限标识 | 中文说明 | 链接 |
|---------|---------|------|
| `contact:contact.base:readonly` | 获取通讯录基本信息 | [详情](https://open.feishu.cn/document/ugTN1YjL4UTN24CO1UjN/uQzN1YjL0cTN24CN3UjN) |
| `contact:department.organize:readonly` | 获取通讯录部门组织架构信息 | [详情](https://open.feishu.cn/document/ugTN1YjL4UTN24CO1UjN/uQzN1YjL0cTN24CN3UjN) |
| `contact:contact:access_as_app` | 以应用身份访问通讯录 | [详情](https://open.feishu.cn/document/ugTN1YjL4UTN24CO1UjN/uQzN1YjL0cTN24CN3UjN) |
| `contact:contact:readonly` | 读取通讯录 | [详情](https://open.feishu.cn/document/ugTN1YjL4UTN24CO1UjN/uQzN1YjL0cTN24CN3UjN) |
| `contact:contact:readonly_as_app` | 以应用身份读取通讯录 | [详情](https://open.feishu.cn/document/ugTN1YjL4UTN24CO1UjN/uQzN1YjL0cTN24CN3UjN) |

### 用户基本信息

| 字段 | 权限 | 说明 |
|------|------|------|
| `name` | `contact:user.base:readonly` | 用户名 |
| `en_name` | `contact:user.base:readonly` | 英文名 |
| `gender` | `contact:user.base:readonly` | 性别 |
| `avatar` | `contact:user.base:readonly` | 头像 |

### 联系方式

| 字段 | 权限 | 说明 |
|------|------|------|
| `email` | `contact:user.email:readonly` | 邮箱 |
| `mobile` | `contact:user.phone:readonly` | 手机号 |
| `mobile_visible` | - | 手机号可见性（无需权限） |

### 员工信息

| 字段 | 权限 | 说明 |
|------|------|------|
| `user_id` | `contact:user.employee_id:readonly` | 用户 ID |
| `employee_no` | `contact:user.employee_number:read` | 工号 |
| `employee_type` | `contact:user.employee:readonly` | 员工类型 |
| `join_time` | `contact:user.employee:readonly` | 入职时间 |
| `job_title` | `contact:user.employee:readonly` | 职务 |
| `status` | `contact:user.employee:readonly` | 用户状态 |

### 组织架构

| 字段 | 权限 | 说明 |
|------|------|------|
| `department_ids` | `contact:user.department:readonly` | 所属部门 |
| `leader_user_id` | `contact:user.department:readonly` | 直属主管 |
| `orders` | `contact:user.department:readonly` | 排序信息 |

### 通讯录权限（其他应用）

| 字段 | 权限 | 说明 |
|------|------|------|
| `union_id` | `contact:contact:readonly` 或 `contact:contact:access_as_app` | 统一用户标识 |
| `open_id` | `contact:contact:readonly` 或 `contact:contact:access_as_app` | 应用内用户标识 |
