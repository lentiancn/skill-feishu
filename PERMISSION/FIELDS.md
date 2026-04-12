# 字段权限与所需权限对应表

## 用户基本信息

| 字段 | 所需权限 | 说明 |
|------|---------|------|
| `name` | `contact:user.base:readonly` | 用户名 |
| `en_name` | `contact:user.base:readonly` | 英文名 |
| `gender` | `contact:user.base:readonly` | 性别 |
| `avatar` | `contact:user.base:readonly` | 头像 |

## 联系方式

| 字段 | 所需权限 | 说明 |
|------|---------|------|
| `email` | `contact:user.email:readonly` | 邮箱 |
| `mobile` | `contact:user.mobile:readonly` | 手机号 |
| `mobile_visible` | `contact:user.mobile:readonly` | 手机号可见性 |

## 员工信息

| 字段 | 所需权限 | 说明 |
|------|---------|------|
| `user_id` | `contact:user.employee_id:readonly` | 用户 ID |
| `employee_no` | `contact:user.employee_id:readonly` | 工号 |
| `employee_type` | `contact:user.employee:readonly` | 员工类型 |
| `join_time` | `contact:user.employee:readonly` | 入职时间 |
| `job_title` | `contact:user.employee:readonly` | 职务 |
| `status` | `contact:user:readonly` | 用户状态 |

## 组织架构

| 字段 | 所需权限 | 说明 |
|------|---------|------|
| `department_ids` | `contact:department:readonly` | 所属部门 |
| `leader_user_id` | `contact:user.employee_id:readonly` | 直属主管 |
| `orders` | `contact:department:readonly` | 排序信息 |

## 自定义字段

| 字段 | 所需权限 | 说明 |
|------|---------|------|
| `custom_attrs` | `contact:user.employee:readonly` | 自定义字段 |

## 企业信息

| 字段 | 所需权限 | 说明 |
|------|---------|------|
| `enterprise_email` | `contact:user.enterprise_email:readonly` | 企业邮箱 |

## 部门权限

| 字段 | 所需权限 | 说明 |
|------|---------|------|
| `union_id` | `contact:contact:readonly` | 统一用户标识 |
| `open_id` | `contact:contact:readonly` | 应用内用户标识 |
| `is_tenant_manager` | `contact:user.employee:readonly` | 是否为租户管理员 |
