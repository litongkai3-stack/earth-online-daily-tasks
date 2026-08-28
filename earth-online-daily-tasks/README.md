# Earth Online Daily Tasks

一个可复用的 Codex Skill：给它一张像素风任务卡参考图和日期，即可生成一张「地球 Online」每日任务卡。它会生成 3 个核心任务、1 个彩蛋任务、温馨提醒，并在调用项目中维护任务记录，避免后续任务重复。

## 安装

将整个 `earth-online-daily-tasks` 文件夹放进 Codex 的 Skills 目录：

```bash
git clone https://github.com/<YOUR-ACCOUNT>/<YOUR-REPOSITORY>.git
mkdir -p "$CODEX_HOME/skills"
cp -R <YOUR-REPOSITORY>/earth-online-daily-tasks "$CODEX_HOME/skills/"
```

重载 Codex 后，使用 `$earth-online-daily-tasks` 调用。也可以在 Codex 中通过 GitHub Skill 安装流程导入这个文件夹。

## 最小调用

```text
使用 $earth-online-daily-tasks。
参考图：<附上一张像素风任务卡图片>
日期：2026-08-28
```

只提供参考图和日期也能运行；Skill 会自行生成温暖、5 分钟内可完成的任务方向。

## 带方向调用

```text
使用 $earth-online-daily-tasks。
参考图：<附图>
日期：2026-08-28
核心任务方向：下班后放松和整理一个小角落
彩蛋任务方向：能让评论区分享各自答案的小怪点子
```

## 每日记录和去重

每个调用项目会自动创建：

```text
.earth-online-daily-tasks/
├── output/     # 最终 PNG
└── records/    # 每日 Markdown 采用记录
```

Skill 在出题前会读取所有 `records/*.md`，避免重复或语义近似的任务。当天只改排版时，会保留任务内容并在该日期记录中追加修订信息。

## 发布到 GitHub 前

请自行选择并添加适合你的开源许可证，然后将此目录推送到公开仓库。Skill 本身不会自动提交或发布任何内容。
