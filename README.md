# prompts-libs

个人 Prompt 库 & Skill 文档库。用于集中管理日常使用的提示词和技能文档，方便快速复用。

## 目录结构

```
prompts-libs/
├── .prompts/              # Prompt 文件
└── .skills/               # Skill 文档（可复用的能力模块）
```

## 如何使用

1. **浏览文件**：进入 `.prompts/` 或 `.skills/` 目录，找到适合当前场景的 `.md` 文件。
2. **复制使用**：打开文件，将内容直接粘贴到 AI 对话框，或按需修改后使用。
3. **新增 Prompt**：在 `.prompts/` 目录下新建 `kebab-case.md` 文件并提交。
4. **新增 Skill**：在 `.skills/` 目录下新建 `kebab-case.md` 文件并提交。

## 命名规范

| 类型 | 格式 | 示例 |
|------|------|------|
| Prompt 文件 | `kebab-case.md` | `code-review.md` |
| Skill 文件 | `kebab-case.md` | `python-debugging.md` |
