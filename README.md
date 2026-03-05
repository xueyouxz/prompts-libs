# prompts-libs

个人 Prompt 模板库 & Skill 文档库。用于集中管理日常使用的提示词模板和技能文档，方便快速复用。

## 目录结构

```
prompts-libs/
├── prompts/               # Prompt 模板（按场景分类）
│   ├── coding/            # 编程相关
│   ├── writing/           # 写作相关
│   ├── analysis/          # 分析与研究
│   └── creative/          # 创意与头脑风暴
├── skills/                # Skill 文档（可复用的能力模块）
│   ├── coding/            # 编程技能
│   ├── writing/           # 写作技能
│   └── productivity/      # 效率工具与方法
└── templates/             # 新建模板时使用的基础框架文件
```

## 如何使用

1. **浏览模板**：进入对应分类目录，找到适合当前场景的 `.md` 文件。
2. **复制使用**：打开文件，将 `{{变量}}` 占位符替换为实际内容后直接粘贴到 AI 对话框。
3. **新增模板**：参考 [`templates/prompt-template.md`](templates/prompt-template.md) 的格式新建文件并提交。
4. **新增 Skill**：参考 [`templates/skill-template.md`](templates/skill-template.md) 的格式新建文件并提交。

## 命名规范

| 类型 | 格式 | 示例 |
|------|------|------|
| Prompt 文件 | `kebab-case.md` | `code-review.md` |
| Skill 文件 | `kebab-case.md` | `python-debugging.md` |
| 占位符 | `{{变量名}}` | `{{代码片段}}` |

## 分类说明

### prompts/

| 目录 | 说明 |
|------|------|
| `coding/` | 代码审查、调试、重构、单元测试生成等 |
| `writing/` | 博客文章、邮件、文档、报告等 |
| `analysis/` | 数据分析、竞品分析、需求分析等 |
| `creative/` | 头脑风暴、创意生成、故事构建等 |

### skills/

| 目录 | 说明 |
|------|------|
| `coding/` | 编程语言技巧、框架使用、最佳实践 |
| `writing/` | 技术写作、商务写作风格指南 |
| `productivity/` | GTD、时间管理、工具使用技巧 |
