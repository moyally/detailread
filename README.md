# detailread 论文精读

让 AI 按原文顺序讲清论文：作者提出了什么问题，每一步用了什么证据，如何从证据走向结论，各部分为什么这样衔接。

适合希望理解整篇论文论证过程的读者。它会区分描述事实、统计关联、因果解释和政策推演，并检查图表口径、历史背景与结论边界。核心文件是 [SKILL.md](SKILL.md)；不需要 API 密钥，也不包含执行脚本。

## 先选择你的平台

- **ChatGPT 网页版或 App**：使用项目文件与项目指令复用这套方法。
- **Claude**：通过自定义 Skills 上传技能压缩包。
- **Gemini 网页版或 App**：使用自定义 Gem 的指令复用这套方法，并留意官方向 Skills 的迁移。

三种方式的产品机制不同。项目文件或 Gem 指令不会自动变成原生技能安装；本指南不涉及各平台 API 或命令行工具。

## 下载文件

打开 [SKILL.md](SKILL.md)，通过 Raw 页面保存文件，或在仓库首页选择 Code → Download ZIP 后解压。

如果仓库是私有的，只有已获授权的 GitHub 用户能够访问和下载。把仓库链接贴进聊天，并不等于 AI 已读取或安装了技能。

## 在 ChatGPT 中使用

推荐使用项目保存阅读规则：

1. 在侧边栏新建项目，命名为 `detailread 论文精读`。
2. 将 `SKILL.md` 上传为项目文件。若界面不接受 Markdown 文件，可将内容另存为 TXT 后上传。
3. 在项目设置的指令中填写下方文字。
4. 在该项目的新聊天中上传论文全文，发送后面的示例请求。

```text
当我请求精读或详细理解论文时，请先读取项目文件 SKILL.md，并将其中的 detailread 方法作为我的阅读要求：按原文顺序解释各部分的论点、证据、推论、限制和衔接，最后重建全文逻辑。若无法读取规则或论文全文，请明确说明，不要用摘要冒充全文精读。普通翻译、摘要或其他任务按我当次要求处理。
```

项目指令只作用于该项目。这里采用的是 ChatGPT 的项目功能，不是把本地 Codex 技能目录安装进 ChatGPT。官方说明：[ChatGPT Projects](https://help.openai.com/en/articles/10169521-projects-in-chatgpt)。

## 在 Claude 中安装

将下载的 `SKILL.md` 放进一个准确命名为 `detailread` 的文件夹，再压缩整个文件夹。不要直接使用 GitHub 下载的 `detailread-main.zip`，以免文件夹名称和技能名称不一致。

```text
detailread.zip
└── detailread/
    └── SKILL.md
```

进入 Claude 的 **Customize → Skills**，选择 **+ → Create skill → Upload a skill**，上传 ZIP 并启用该技能。随后在聊天中上传论文，并明确要求使用 `detailread`。

本仓库的 `agents/openai.yaml` 是 Codex 的界面配置，Claude 安装包只需包含 `SKILL.md`。若看不到上传入口，请检查账号功能和组织权限；菜单以实际界面为准。

官方说明：[使用 Skills](https://support.claude.com/en/articles/12512180-use-skills-in-claude)、[创建与打包自定义 Skills](https://support.claude.com/en/articles/12512198-how-to-create-custom-skills)。

## 在 Gemini 中使用

对仍显示 Gems 的界面：

1. 在 Gemini 网页版打开 Gems 或 Explore Gems，选择 New Gem。
2. 命名为 `detailread 论文精读`。
3. 打开本仓库的 `SKILL.md`，跳过开头两条 `---` 之间的元数据，将后面的全部正文复制到 Gem 的 Instructions 中。
4. 测试预览，然后点击 Save；预览不会自动保存。
5. 打开这个 Gem，上传论文并发送精读请求。

这里把技能正文作为 Gem 的固定指令，不要求 Gemini 识别 ZIP 或 Codex 配置。官方说明：[创建 Gem 与设置指令](https://support.google.com/gemini/answer/15235603?hl=en)。

**界面迁移提示：**Google 官方说明个人账号的 Gems 将从2026年11月起逐步迁移到 Skills。若你的账号已显示新入口，请以官方迁移说明和实际界面为准；本文不据此假定它支持导入本仓库 ZIP。[官方 Gems 使用与迁移入口](https://support.google.com/gemini/answer/15146780?hl=en)。

## 所有平台通用的临时用法

如果没有项目、Skills 或 Gems 入口，可在普通聊天中上传 `SKILL.md` 和论文，或直接粘贴技能正文，然后要求本次按该方法解释。此方式不保证新聊天自动保留规则。

## 第一次怎么问

```text
请使用 detailread，帮我详细理解这篇论文。
先说明全文真正要回答的问题和整体路线，再按原文各部分逐点解释：
作者提出什么观点、使用什么证据、推论是否成立、为什么引出下一部分。
请说明图表与方法在论证中的作用，区分作者观点和你的解释，标明可核实的页码。
最后串起完整论证链，并说明文章的贡献和仍需保留判断的地方。
```

聚焦某一部分时，可以问：“用 detailread 详细解释第三节，尤其是它如何承接第二节、怎样为结论提供证据。”

## 怎样检查是否生效

理想回答应当呈现原文章节与整体路线；解释观点背后的证据及限制；说清段落和章节之间的桥梁；最后重建论证，而不只是列出内容概要。

如果只得到简短总结，可补充：“请按 detailread 展开论证步骤，不要只概括每节内容。”模型不同，输出不会完全一致；关键数字、引用和因果判断仍应回查原文。扫描质量差、文件过长或未提供全文时，应先确认模型实际读到了哪些部分。

## 更新

更新仓库文件不会自动同步到各平台。ChatGPT 项目需替换规则文件；Claude 需更新或重新上传技能并确认启用正确版本；Gemini 需更新固定指令并保存。

说明核对日期：2026年11月1日。产品入口可能因账号、地区、组织设置和后续更新而变化，以上链接为各平台官方帮助文档。
