# 程子阅读助手

一个面向 Codex 的阅读工作流 Skill：从真实问题或阅读兴趣出发，把书籍划线整理为可追溯的阅读结论、通用知识、实践案例与复盘。

## 主要能力

- 带着真实问题查找书籍与具体章节
- 基于兴趣探索阅读方向
- 整理 Obsidian 或普通 Markdown 中的已有划线
- 区分原文、用户想法、Codex 归纳和业务应用
- 提炼知识卡片，并通过确认机制控制文件数量
- 将阅读结论转化为实践案例、行动与复盘
- 支持从阅读中发现并延伸新的问题线索

## 仓库结构

```text
.
├── README.md
├── LICENSE
└── chengzi-reading-assistant/
    ├── SKILL.md
    ├── agents/
    │   └── openai.yaml
    ├── assets/
    └── references/
```

`chengzi-reading-assistant/` 是可直接安装的 Skill 目录；仓库级说明和许可证保留在根目录，不进入运行上下文。

## 安装

将整个 `chengzi-reading-assistant` 目录复制到 Codex 的 Skills 目录：

- Windows：`%USERPROFILE%\.codex\skills\chengzi-reading-assistant`
- macOS / Linux：`~/.codex/skills/chengzi-reading-assistant`
- 自定义 `CODEX_HOME`：`$CODEX_HOME/skills/chengzi-reading-assistant`

安装后重新启动 Codex，或新开一个任务。

## 使用

在 Codex 中输入：

```text
使用 $chengzi-reading-assistant，我要读书
```

然后选择：

- A：带着问题读书
- B：基于兴趣探索
- C：整理已经读过的内容

也可以从任意阶段进入，例如：

```text
划线已同步
帮我整理这一章
我来复盘了
```

## 可选集成

Skill 只依赖支持 Skills 的 Codex 和可读写的 Markdown 工作区。以下能力均为可选：

- Obsidian：用于浏览、双向链接与知识库管理
- Obsidian 社区插件 `Wechat Reading`（插件 ID：`wechatreading-highlights`）：用于同步微信读书内容
- 联网检索：用于核对书籍版本、目录与引用来源

没有 Obsidian 或微信读书时，也可以使用本地 Markdown 或手动导入的划线。

## 隐私与安全

- 不在 Skill、配置文件或对话中保存微信读书 Cookie、API Key 或其他凭证
- API Key 仅由用户在插件官方界面中输入
- 默认只读取当前任务需要的文件，不扫描整个知识库
- 初始化时不覆盖、移动或删除现有 Obsidian Vault 内容
- 所有配置路径必须位于选定的 Vault 内

## Skill 元数据

- Skill 名称：`chengzi-reading-assistant`
- 显示名称：程子阅读助手
- 适用场景：问题驱动阅读、兴趣探索、划线整理、知识分流、实践与复盘
- 支持平台：Windows、macOS、Linux

## 许可证

本项目采用 [MIT License](LICENSE)。
