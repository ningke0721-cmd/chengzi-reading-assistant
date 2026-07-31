# 配置发现与兼容性

## 查找与基准目录

从当前工作目录开始逐级向父目录查找 `.chengzi-reading.json`，遇到第一个即停止。配置文件所在目录是 `config_dir`。

1. 读取 JSON；解析失败、顶层不是对象或字段类型错误时停止写入，指出文件与错误。
2. `vault_root` 必须是相对路径；相对于 `config_dir` 解析。省略时仅为兼容早期配置而使用 `"."`。
3. 解析后的 Vault 必须存在且包含 `.obsidian/`。若用户明确使用纯 Markdown 工作区，可在本次对话中继续，但要说明 Obsidian 功能不可用。
4. 其他 `*_path` 和 `guide_path` 都必须是相对于解析后 Vault 根目录的相对路径。
5. 规范化每个路径，拒绝绝对路径、`..` 越界和解析后落在 Vault 外的符号链接。路径校验失败时停止写入，不自行修复到其他位置。

不要把路径相对于当前工作目录解析，因为用户可能从 Vault 的子目录启动 Codex。

## Schema 1

必需字段：

- `schema_version`：整数 `1`
- `vault_root`
- `reading_conclusions_path`
- `problems_path`
- `general_knowledge_path`
- `practice_cases_path`
- `reviews_path`
- `guide_path`

可选字段：

- `raw_notes_path`：只在存在原始划线来源时需要。
- `guide_version`：用于判断内置指南是否更新；缺失时视为未知版本，不自动覆盖。配置中的版本低于内置指南时先比较差异，征得用户确认后再更新文件与版本号。
- `business_domains`：字符串数组；缺失时视为空数组。

发现未知的 `schema_version` 时只读配置并停止写入，说明当前 Skill 不支持该版本。保留未知字段，不因更新配置而删除。

## 写入前检查

- 写入、建目录或复制指南前确认目标仍在 Vault 内。
- 使用 UTF-8；Markdown 文件使用 `.md`。
- 已有文件先按同主题搜索并读取必要部分，避免仅靠文件名判断。
- 初始化产生的配置只保存相对路径；不要写设备用户名、主目录或凭证。

## 能力缺失

- 没有微信读书能力：使用本地 Markdown 或请用户导入划线。
- 没有联网能力：不核对版本、目录或短引文；请用户提供可靠材料。
- 没有 Obsidian：仍可生成标准 Markdown，但不声称已验证 Obsidian 展示效果。
- 工作区只读：可以分析和展示拟写内容，不声称文件已经创建或更新。
