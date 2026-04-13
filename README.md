# README.md - feishu-skill

这个技能用于在 OpenClaw 中集成飞书（Feishu/Lark）平台能力，包括：

- 📝 飞书文档操作（读取、写入、插入表格等）
- 📂 飞书云盘文件管理（列表、创建文件夹、移动、删除、评论）
- 🔐 飞书权限管理（文档和文件的权限配置）
- 📚 飞书知识库操作（空间、节点管理、搜索、移动、重命名）
- 📊 飞书多维表格（Bitable）操作（元数据查询、字段管理、记录CRUD）

## 集成组件

### 文档与协作
- `feishu_doc` - 飞书文档读写操作

### 云存储管理
- `feishu_drive` - 飞书云盘文件管理

### 权限控制
- `feishu_perm` - 飞书权限管理

### 知识库
- `feishu_wiki` - 飞书知识库操作

### 多维表格
- `feishu_bitable_*` - 多维表格相关操作（元数据、字段、记录）

## API 文档来源

技能调用的飞书 OpenAPI 文档存放在 `open-apis/` 目录下，按功能模块组织。

## 许可证

**skill-feishu** 采用 [MIT-0 许可证](https://raw.githubusercontent.com/lentiancn/skill-feishu/refs/heads/main/LICENSE)授权。
