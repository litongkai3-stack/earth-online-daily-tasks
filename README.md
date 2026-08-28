# Earth Online Daily Tasks

一个可复用的 Codex Skill：根据像素风任务卡参考图和日期，生成「地球 Online」每日任务卡，并维护任务历史以避免后续内容重复。

![最终成图示例](earth-online-daily-tasks/assets/examples/final-card-2026-08-28.png)

## 这个 Skill 能做什么

- 生成 3 个五分钟内可完成的核心任务与 1 个有讨论感的彩蛋任务
- 使用必填的参考图和日期；核心/彩蛋方向可选，未提供时自动生成
- 有生图能力时输出 PNG；没有生图能力时输出可离线打开的 HTML 卡片
- 每天创建 Markdown 采用记录，并在下次生成前排除重复或语义近似任务

## 安装与调用

```bash
git clone https://github.com/litongkai3-stack/earth-online-daily-tasks.git
mkdir -p "$CODEX_HOME/skills"
cp -R earth-online-daily-tasks/earth-online-daily-tasks "$CODEX_HOME/skills/"
```

重载 Codex 后，使用：

```text
使用 $earth-online-daily-tasks。
参考图：<附上一张像素风任务卡图片>
日期：2026-08-28
```

完整的输入规则、去重记录格式、HTML 回退方式和质检清单见 [Skill 文档](earth-online-daily-tasks/README.md)。

## 项目结构

```text
earth-online-daily-tasks/
├── SKILL.md
├── agents/openai.yaml
├── assets/
│   ├── fallback-card.html
│   └── examples/final-card-2026-08-28.png
└── references/
```

发布前请自行选择并添加适合的开源许可证。
