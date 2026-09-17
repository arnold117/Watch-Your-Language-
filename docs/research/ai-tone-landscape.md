# 去 AI 味 /「人味写作」项目版图勘察

- 勘察日期：**2026-09-17（UTC）**。文中所有 star/fork 数、commit SHA、页面 revision 均为该日实测值。
- 目的：为 Watch-Your-Language 的方案议题摸底——同类东西都有谁、各自解决什么问题、依据是什么，以及**有没有人在约束「从零起草」而不是事后润色**。
- 取数方式：起点两仓直接 `git clone` 读原文；其余 GitHub 元数据与文件用已登录的 `gh api`；网页与 raw 文件用 `curl -sL --max-time 30`（本机 `web_fetch` 被 DNS 代理拦死）。搜索引擎只用于发现线索，**所有结论都回到原文核对过**，核对命令见 §7。

---

## 1. 一句话结论

这个版图在 2026 年 1 月被 Agent Skill 形态引爆，头部高度集中且**几乎全部是「事后改写」**；**约束起草的项目确实存在（≥6 个），但都不是把规则做成不可绕过的起草前硬门禁**——最接近的只有中文网文垂直项目 oh-story（写正文前大纲门禁 + 8 个 hook + 确定性 lint 脚本）和中文通用项目 human-writing（动笔前材料门禁 + 第一稿写法）。**统计实证与热度严重反相关**：四个最高热项目（49k / 17.4k / 17.3k / 10.2k ★）全部是经验清单，唯一基于 283 万字对照语料实测的中文项目只有 1.7k ★。

---

## 2. 总览表

| # | 项目 | 形态 | 解决什么 | 依据 | 语言 | 许可 | ★ / fork | 审的版本 |
|---|---|---|---|---|---|---|---|---|
| 1 | [lieflat-less-ai-tone](https://github.com/larashero3-dotcom/lieflat-less-ai-tone) | Agent Skill + py 脚本 | 事后清理（自述仅成稿） | **统计实证**：283 万字对照语料 | 中文 | MIT | 1673 / 113 | `27d2923` 2026-08-24 |
| 2 | [KKKKhazix/human-writing](https://github.com/KKKKhazix/human-writing) | Agent Skill + references | **起草 + 改稿** | 经验清单（无语料、无引用） | 中文 | MIT | 3676 / 281 | `4fda173` 2026-08-05 |
| 3 | [blader/humanizer](https://github.com/blader/humanizer) | Agent Skill（+CC 插件） | 事后改写 | 维基百科观察清单 + 自撰成因理论 | 英文 | MIT | **49306** / 3998 | `9862685` 2026-09-06 |
| 4 | [op7418/Humanizer-zh](https://github.com/op7418/Humanizer-zh) | Claude Skill | 事后改写 / 审阅 | 3 号的中译 + stop-slop 工具部分 | 中文 | MIT | 17414 / 1152 | `91f3d39` 2026-01-19 |
| 5 | [hardikpandya/stop-slop](https://github.com/hardikpandya/stop-slop) | Skill 文件 | 改写（自述含 drafting） | 经验清单（8 条 + 词表 + 速查） | 英文 | MIT | 17250 / 1256 | `8da1f03` 2026-03-17 |
| 6 | [petergyang/no-ai-slop](https://github.com/petergyang/no-ai-slop) | Agent Skill（+ChatGPT 插件） | 事后改写 + 检测 | 经验清单（20+ 模式） | 英文 | MIT | 10197 / 712 | `000650b` 2026-09-02 |
| 7 | [slivenred/no-ai-slop-zh-TW](https://github.com/slivenred/no-ai-slop-zh-TW) | Agent Skill | 事后改写 + 检测 | 6 号的繁中本地化 | 繁中 | MIT | 14 / 3 | `4dc7e1b` 2026-07-23 |
| 8 | [Nanako0129/sepia](https://github.com/Nanako0129/sepia) | Agent Skill + 4 平台原生插件 | **write / review / refactor / recreate 四操作** | **统计实证**：StoryScope（arXiv:2604.03136，61608 篇） | 英为主 + zh-CN/zh-TW + 中文校准文件 | MIT | 2650 / 170 | `4bf02fe` 2026-09-16 |
| 9 | [zenstory-ai/oh-story-claudecode](https://github.com/zenstory-ai/oh-story-claudecode) | 13 个 Agent Skill + hooks | **网文全流程**：起草 + 去 AI 味 | 行业方法论 + 自建确定性 lint | 中文（有 EN README） | MIT | 6926 / 986 | `fe1c133` 2026-09-16 |
| 10 | [OUBIGFA/De-AI-Prompt-Enhancer-Writer-Booster-SKILL](https://github.com/OUBIGFA/De-AI-Prompt-Enhancer-Writer-Booster-SKILL) | 提示词 / SKILL | **两模式：风格复现 + 去 AI 味**，支持从零生成 | 小样本经验：7 篇真实作者文章 | 中文 | **无许可证** | 791 / 84 | `59eafed` 2026-09-17 |
| 11 | [wei125775-lab/deai](https://github.com/wei125775-lab/deai) | 单文件 SKILL + references | **清理/重构/检测/新写 四档** | 二次综合（合并 4 家规则）+ A/B/C 分级仲裁 | 中文 | MIT | 3 / 0 | `c53d22e` 2026-09-06 |
| 12 | [harshaneel/humanize](https://github.com/harshaneel/humanize) | Agent Skill | 事后改写 + **含「从零生成」章（连解码参数都给）** | 自称 50+ 同行评审来源（下文有核验） | 英文 | MIT | 468 / 49 | `4ec7973` 2026-07-10 |
| 13 | [kylehughes/writing-prose-like-a-human-for-agents](https://github.com/kylehughes/writing-prose-like-a-human-for-agents) | Claude 插件：skill + subagent | 写作 + 编辑（subagent 只编辑） | 经验清单（五条规则 + 词表） | 英文 | NOASSERTION | 20 / 0 | `87233cb` 2026-02-23 |
| 14 | [Wikipedia:Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing)（WikiProject AI Cleanup） | 维基页面（事实上的公共知识库） | 检测/标注，不改写 | 自述「observations, not rules」+ 真实编辑案例 + 引用研究 | 英文 | CC BY-SA 4.0 | 不适用 | revid **1374941330**，2026-09-14 |
| 15 | [vale-cli/vale](https://github.com/vale-cli/vale) | Go CLI + YAML 规则包 | 把风格指南做成可执行 lint（起草时/CI 约束） | 人工规则，非统计 | 规则语言无关 | MIT | 6109 / 225 | `0194fbb` 2026-09-17 |
| 16 | [Hello-SimpleAI/chatgpt-comparison-detection](https://github.com/Hello-SimpleAI/chatgpt-comparison-detection)（HC3） | 数据集 + 检测器 + Demo | 文本检测 | **统计实证**：人机对照语料 + 分类器评测 | **中英双语** | 数据 CC-BY-SA（各子集另有许可） | 1460 / 128 | `1f8c15c` 2023-06-27 |
| 17 | 零样本检测器群体（见 §3.17） | Python 库 / 论文代码 | 文本检测 | 统计实证 | 英文为主 | MIT / BSD-3 | 477 / 433 / 416 | 见表 |
| 18 | 传统风格指南仓：Microsoft / 18F（见 §3.18） | 文档仓 | 风格规范，非去 AI 味 | 机构规范 | 英文 | CC-BY-4.0 / NOASSERTION | 192 / 84 | 均于 2023–2024 停更 |

---

## 3. 逐项详述

### 3.1 larashero3-dotcom/lieflat-less-ai-tone（起点之一）

1. **名称 + 链接**：lieflat-less-ai-tone — https://github.com/larashero3-dotcom/lieflat-less-ai-tone
2. **解决什么问题**：**纯事后改写**。SKILL.md frontmatter 自己写明「适用于写作完成后的成稿清理」，并声明采用**白名单式**改写：「没有命中任何规则的句子必须逐字保留」「不得顺便润色」「文章结构不在处理范围内」。
3. **依据**：**统计实证**，且是本版图里方法最透明的。`RESEARCH.md` 的「方法」节给出对照设计：AI 侧 300 篇（5 个模型各 60 篇：claude-opus-4-6、deepseek-v4-pro、gemini-3.1-pro、gpt-5.6-sol、kimi-k3）1,179,105 汉字 vs 人类侧 329 篇 1,647,867 汉字，合计 **2,826,972 字 / 95,551 句 / 45,721 段**；判定用倍率门槛，并按「每千汉字 / 每百段 / 占同类元素比例」三种分母分别选型；另有「六次测量失误」与「局限」自陈章节。**11 条改写规则**（SKILL.md「改写规则」1–11）对应实测成立的项；**15 条被否掉的流行特征**列在 RESEARCH.md「不成立，已删除」表内（含「AI 句长均匀度是人类 50 倍」被证伪为切句缺陷造成的假象，实测 0.87×；「问句小标题」的每千字 32 倍是分母陷阱，换成占小标题比例后差异消失）。
4. **语言覆盖**：中文（另有 `README.en.md` / `RESEARCH.en.md` 英文版文档，规则本体是中文）。
5. **打包与调用形态**：Agent Skill（`SKILL.md`）+ 三个可自测脚本 `scripts/compare-human-ai.py`、`check-translationese.py`、`check-structure.py`。用户自带语料即可复现倍率。
6. **许可证**：MIT。
7. **热度**：1673 ★ / 113 fork（2026-09-17）。
8. **审的版本**：`27d29232f10124db904ca9c0536d0b67cb3b2833`，2026-08-24（提交信息「冒号规则重测：新增空转句形态，修正数据与改法」）。
9. **勘察备注**：RESEARCH.md 定义「倍率 = AI 频率 ÷ 人类频率」，而同仓 `compare-human-ai.py` 的文档字符串写「倍率 = 人类频率 / AI 频率（<1 表示 AI 用得更多）」——两者互为倒数，是同仓内的**约定不一致**，复算时需注意（不是错误，因为判读方向各自自洽）。

### 3.2 KKKKhazix/human-writing（起点之二）

1. **名称 + 链接**：human-writing（活人感写作） — https://github.com/KKKKhazix/human-writing
2. **解决什么问题**：**起草与改稿都管**，且起草是主线。README 的定位是「让模型写出来的文章读起来像一个具体的人在说话」，用法示例是「把我的材料写成一篇有活人感和中文韵律的作品」。SKILL.md 有独立的两节：`## 动笔前先找到说话位置`（动笔前在内部回答五个问题，并明确「现实材料不够时先停在这里」「不要先交一篇空稿，再期待用户往里补活人感」）与 `## 第一稿直接带着人写`（第一稿的写法清单：开头尽快碰到事情、一段先完成眼下这一件事、新段落必须增加一件新东西、写到事情讲完就停）。事后层是 `## 成稿绝对不能出现`（中译：命中一项就不能交稿）。
3. **依据**：**经验清单**。仓库内**没有**语料统计、没有外部研究引用；规则来自写作经验与对模型输出的观察。它自带一个确定性脚本 `scripts/check_prose.py`，但 README 明确其边界：「检查脚本只管已经写明的硬规则，不替你决定风格」。
4. **语言覆盖**：中文（规则本体、面向中文写作场景）。
5. **打包与调用形态**：Agent Skill 目录 `human-writing/`（`SKILL.md` + `references/{fiction,reality,revision,formats,forum-prose}.md` 5 个参考文件 + `agents/openai.yaml` + `scripts/check_prose.py`），版本号 `VERSION` = 1.1.0；可 `npx skills add` 或整目录复制到 `~/.agents/skills/`。
6. **许可证**：MIT。
7. **热度**：3676 ★ / 281 fork。
8. **审的版本**：`4fda173f3fef7fb808f3eba991eeb2528ea4b189`，2026-08-05（「docs: 重写 README，去掉产品说明书腔」）。

### 3.3 blader/humanizer

1. **名称 + 链接**：humanizer — https://github.com/blader/humanizer
2. **解决什么问题**：**事后改写**。frontmatter 的 description：「Rewrite AI-sounding text so it reads like the writer without changing what it says.」工作流四步是「标记 → 草稿重写 → 对照检查 → 定稿」，输入是已有文本。
3. **依据**：**经验清单**，但上游很硬。frontmatter 直接写 `Based on Wikipedia's "Signs of AI writing."`（即 §3.14）。SKILL.md 自己补了一层成因解释（模型选「对最多读者都成立」的下一个 token，人只为一个读者选），并把模式按强弱分级：§1–§5 见一次即可改，标 *weak alone* 的需要与同段其他标记共现才动手。这层「共现才判」是本版图里少见的**误伤控制**设计。
4. **语言覆盖**：英文（SKILL.md 与 reference 均为英文）；中文生态靠 §3.4 的翻译版承接。
5. **打包与调用形态**：Agent Skill + Claude Code 插件（`.claude-plugin/`），另有 `agents/openai.yaml` 与 `scripts/validate-package.py`。
6. **许可证**：MIT（frontmatter 亦标 `license: MIT`）。
7. **热度**：**49306 ★ / 3998 fork**——本版图热度第一。
8. **审的版本**：`9862685f575c65a8247f90369951df1b3416e3d6`，2026-09-06；仓库创建于 2026-01-18。

### 3.4 op7418/Humanizer-zh

1. **名称 + 链接**：Humanizer-zh — https://github.com/op7418/Humanizer-zh
2. **解决什么问题**：**事后改写 + 审阅**（README：「适用于编辑和审阅 AI 生成的内容」）。
3. **依据**：**转述/翻译**，非独立实证。README 顶部「声明」写得很清楚：核心文件翻译自 blader/humanizer，实用工具部分（核心规则、快速检查清单、质量评分）参考 hardikpandya/stop-slop，原项目基于维基百科 Signs of AI writing。
4. **语言覆盖**：中文。
5. **打包与调用形态**：Claude Code Skill，`npx skills add` 或克隆到 `~/.claude/skills/`。
6. **许可证**：MIT。
7. **热度**：17414 ★ / 1152 fork——中文生态热度第一。
8. **审的版本**：`91f3d394db8419c20d67ebe22a96cf8fee0a404b`，2026-01-19（仓库当日创建后即停更，最后提交是「docs: 添加 npx 一键安装方式」）。

### 3.5 hardikpandya/stop-slop

1. **名称 + 链接**：stop-slop — https://github.com/hardikpandya/stop-slop
2. **解决什么问题**：主要是事后处理，但**自述覆盖起草**。frontmatter description：「Remove AI writing patterns from prose. Use when **drafting**, editing, or reviewing text to eliminate predictable AI tells.」正文形式是 8 条 Core Rules + 一组 Quick Checks + `references/{phrases,structures}.md`。
3. **依据**：**经验清单**（作者自述的规则表；无统计、无引用）。
4. **语言覆盖**：英文。
5. **打包与调用形态**：单文件 `SKILL.md` + `references/`（提示词/skill 形态，无代码）。
6. **许可证**：MIT。
7. **热度**：17250 ★ / 1256 fork。
8. **审的版本**：`8da1f030185bdfe8471220585162991eaeb970e9`（main 分支头），2026-03-17；仓库创建于 2026-01-11——比 blader/humanizer 还早一周。

### 3.6 petergyang/no-ai-slop

1. **名称 + 链接**：no-ai-slop — https://github.com/petergyang/no-ai-slop
2. **解决什么问题**：**事后改写（默认）+ 检测**。SKILL.md 的「Two jobs」：**Edit (default)** 与 **Detect**（「Do not rewrite, score the draft, or guess whether AI wrote it. AI detectors guess. Named patterns are evidence the user can check.」）。第三条用法是「Draft an AI slop post」——反着生成 slop 做讽刺，不是起草约束。
3. **依据**：**经验清单**。README 列了 20+ 模式中的 10 条（binary contrasts、throat-clearing openers、faux-insight setups、colon reveals、dramatic fragments、superficial analysis、importance puffery、weasel attribution、synonym cycling、fake-profound endings），无实证引用。
4. **语言覆盖**：英文（繁中版见 §3.7）。
5. **打包与调用形态**：Agent Skill（`skills/no-ai-slop/SKILL.md` + `eval.md`）+ ChatGPT/Codex 插件（`build_plugin.py` 构建校验）+ npx skills 安装。
6. **许可证**：MIT。
7. **热度**：10197 ★ / 712 fork。
8. **审的版本**：`000650b156983f5159695b441477f4e63b25dc85`，2026-09-02。

### 3.7 slivenred/no-ai-slop-zh-TW

1. **名称 + 链接**：no-ai-slop-zh-TW — https://github.com/slivenred/no-ai-slop-zh-TW
2. **解决什么问题**：同 §3.6（事后改写 + 检测）。
3. **依据**：**本地化**：6 号的繁中版，自述「移除 AI 寫作痕跡，同時保留作者原本的語氣與風格」。
4. **语言覆盖**：繁体中文。
5. **打包与调用形态**：Agent Skill。
6. **许可证**：MIT。
7. **热度**：14 ★ / 3 fork。
8. **审的版本**：`4dc7e1b6cf1b8aa2ee47156e23635aecdd537c5b`，2026-07-23。
9. **注**：本版图里「英文头部项目 → 中文移植」链条的第二例（第一例是 §3.3 → §3.4）。

### 3.8 Nanako0129/sepia

1. **名称 + 链接**：sepia — https://github.com/Nanako0129/sepia
2. **解决什么问题**：**四操作并列：write / review（只诊断）/ refactor（最小改动）/ recreate（按源事实重写）**——即**同时覆盖起草与事后**。主张「去 AI 味要去到真正露馅的那一层」：虚构先修叙事架构，专业文本按 venue（release notes、PR 回复、postmortem、ticket、技术文章、长报道）各配薄规则。有三遍协议：叙事架构 → 语篇流 → 表面风格，并配 30 项诊断评分表。
3. **依据**：**统计实证，且我核对到了关键数字**。依据 StoryScope（arXiv:2604.03136）。我 curl 了 arXiv abs 页，摘要确认：**10,272 个写作提示 ×（1 人类 + 5 LLM）= 61,608 篇、每篇约 5,000 词、304 个特征；仅叙事特征即达 93.2% macro-F1**，30 项核心特征保留大部分信号；AI 故事「over-explain themes」「tidy, single-track plots」，人类「morally ambiguous choices」「increased temporal complexity」。sepia README 引用的 LAMP 编辑条件「95.5% → 93.9%，只掉 1.6 点」我也在论文 PDF 里逐字核对到了（该项目用 `pdftotext` 后 grep，见 §7）。此外它消化了 `research/` 下多篇研究，中文校准写在 `references/languages/zh.md`（基于 HC3 加一个约两千篇台湾新闻的私有测量，并自陈语料不公开）。
4. **语言覆盖**：**英文为主 + 中文双语文档**（README.zh-CN.md / README.zh-TW.md、`references/languages/zh.md`）。规则本体英文。
5. **打包与调用形态**：符合 agentskills.io 规范的 Agent Skill（唯一 canonical `SKILL.md`，不做平台分叉）+ Claude Code / Codex / Grok Build / Antigravity 原生插件 + Skills CLI（自称支持 77+ agents）；仓库含 `evals/`、`tests/`、GitHub Actions（behavioral eval、version consistency）。**这是本版图里工程化程度最高的项目**。
6. **许可证**：MIT。
7. **热度**：2650 ★ / 170 fork。
8. **审的版本**：`4bf02fed4e7ea608b471340dd6e28de650126f57`，2026-09-16（合并 PR #252 journalism-domain）。

### 3.9 zenstory-ai/oh-story-claudecode

1. **名称 + 链接**：oh-story-claudecode — https://github.com/zenstory-ai/oh-story-claudecode（原 `worldwonderer/oh-story-claudecode`，现归属 zenstory-ai）
2. **解决什么问题**：**网文写作全流程，起草与去 AI 味在一条流水线上**。13 个 skill 覆盖扫榜选材 → 拆文 → 搭大纲写正文 → 去 AI 味（`story-deslop`）→ 封面。README 的结构图里 `write_l --> deslop`、`write_s --> deslop`：去 AI 味是写作流程的下游一段，同时 README 第 430 行的能力表把「去AI味」标注为「**预防** · 三遍去AI法 · 改写范例库 · 禁用词表」——即**预防与清理双轨**。
3. **依据**：**行业方法论 + 自建确定性检查**，不是统计实证。README 明确划界：「`story-deslop` 的本地检查是写作 lint：blocking 只限确定性句式/标点问题，其他提示按读感判断；朱雀等外部检测只作自测参考，不替代人工读感。」
4. **语言覆盖**：中文（有 `README_EN.md`）。
5. **打包与调用形态**：13 个 Agent Skill，可装到 Claude Code / Antigravity / OpenCode / ZCode / OpenClaw / Codex CLI / Reasonix；`story-setup` 在写作项目里部署 **7 个专业 Agent + 8 个自动化 hook** + `references/`（自称 100+ 份写作方法论）；用文件系统当记忆（设定/大纲/正文/追踪分目录）。
6. **许可证**：MIT。
7. **热度**：6926 ★ / 986 fork。
8. **审的版本**：`fe1c133167ae758663c69bd9e5198543958c8b35`，2026-09-16（最新版 v0.7.10，2026-09-09）。

### 3.10 OUBIGFA/De-AI-Prompt-Enhancer-Writer-Booster-SKILL

1. **名称 + 链接**：De-AI-Prompt-Enhancer & Writer Booster SKILL — https://github.com/OUBIGFA/De-AI-Prompt-Enhancer-Writer-Booster-SKILL
2. **解决什么问题**：**双模式：风格复现（good-writing）+ 去 AI 味补丁（de-AI-writing）**，且 README 明确「支持**从零生成**、改写、翻译（结构保真）、审阅、精修五种任务」。`good-writing` 是「作者风格复现引擎」，从 `.writer/` 目录的 7 篇原始文章中提取写作 DNA（半文半白用词、长短交替节奏、类比先行论证等），可自行迭代成专属风格。
3. **依据**：**小样本经验**——特征从 7 篇真实作者文章里提炼；另外自带「24 项 AI 痕迹检测体系」与七大铁律、段落谱系、句式节奏、标点自然生态、去模板规则。上游声明：基于 op7418/Humanizer-zh 做提示词升级。
4. **语言覆盖**：中文。
5. **打包与调用形态**：提示词 / SKILL 形态（适用于 Claude Code、Cursor、Windsurf 等），附两个自动化审计脚本 `style_audit.js`、`style-lint.ps1`。
6. **许可证**：**无**——仓库未附 LICENSE 文件，README 全篇未提许可（`gh api` 的 `license` 字段为 null）。而它声明基于 MIT 的 op7418/Humanizer-zh。**这是引用/聚合时的实际法律风险点。**
7. **热度**：791 ★ / 84 fork。仓库活跃度高（最后提交就在勘察当日）。
8. **审的版本**：`59eafed6c9ebee0cce142e2ea54aab41014afbe9`，2026-09-17（「docs: 优化标点使用指南，澄清去AI改写原则」）。

### 3.11 wei125775-lab/deai

1. **名称 + 链接**：deai — https://github.com/wei125775-lab/deai
2. **解决什么问题**：**四档并列：清理（只清语言、结构一字不动）/ 重构（可动结构骨架）/ 检测（只报告）/ 新写（从零写且默认去 AI 味）**。这是本版图里**唯一把「生成态」与「清理态」显式拆成不同档位、并给出不同流程**的项目：五步纵深链（预检 → 架构 → 段落删剪 → 句级门禁 → 禁词清零 → 冷读）里，第 1 步「架构」标注适用「重构/新写」，清理档跳过。
3. **依据**：**二次综合，本身无新实证**。SKILL.md 与 `SOURCES.md` 列明四家来源与各管哪层：human-writing（词句禁令、材料门槛、改稿七遍）、lieflat（句级触发标记、反误伤表、信息守恒）、sepia（叙事架构诊断、校准哲学、破折号按模型浮动的证据）、oh-story（网文门禁 A-G、禁词量化、过度清理保护）。它自己的贡献是**分级仲裁**：A 硬信号必改 / B 软信号标出给用户定 / C 禁动一律不碰，优先级为「作者风格文档 > C 禁动 > A 硬改 > B 软判」——这是对「多来源规则打架」这一真实问题的一个可复用解法。
4. **语言覆盖**：中文（覆盖网文/小说、知乎、公众号、评论、标题）。
5. **打包与调用形态**：单文件 `SKILL.md` + `references/`（calibration / architecture / passes / gates / hard-bans）+ `scripts/check_deai.py` + `test/`。
6. **许可证**：MIT（`SOURCES.md` 注明各上游保留各自版权，本仓新增与编排为 MIT，并声明「不含上游代码副本，规则文本为原创重写」）。
7. **热度**：3 ★ / 0 fork——**低热度但方法论上是最新的一个（2026-09-06 创建）**，值得当作「后来者的整合尝试」样本。
8. **审的版本**：`c53d22e733c9607675b7e0c63b04dedebca7dd8a`，2026-09-06。

### 3.12 harshaneel/humanize

1. **名称 + 链接**：humanize — https://github.com/harshaneel/humanize
2. **解决什么问题**：以事后改写为主（Rewrite protocol + 9 个 humanization levers），但**有独立一章 `## Generating human text from scratch`**——明确写「When writing new content (not rewriting): apply all nine levers from the first sentence」。这一章还给出**解码参数建议**：temperature 0.9–1.1、top-p 0.95–0.99、repetition penalty 1.1–1.2，理由是拓宽 token 分布以破坏困惑度检测器依赖的局部极大值（引 RAID benchmark）。另外「Hard rules」7 条里有可量化的硬指标，例如「em dash ≤ 每 300 词 1 个」「任意 80 词以上输出里最长句与最短句相差 ≥20 词，且 10–20 词区间的句子必须少于一半」。
3. **依据**：README 宣称「Grounded in 50+ peer-reviewed sources through April 2026」「Nine levers, 50+ peer-reviewed sources, 2024-2026 detection literature」。**核验结果：仓库内 `humanize/references/` 只有一个文件 `research.md`（3,710 字节）。** 也就是说「50+ 来源」的论证密度并未落在仓库里（README 自身的参考文献列表较长，但正文与引用文件不匹配）。**宣称与交付物不一致，需谨慎引用。**
4. **语言覆盖**：英文。
5. **打包与调用形态**：Agent Skill（`humanize/SKILL.md`）+ `install.sh` + `tests/`；自称 LLM-agnostic，覆盖 Claude Code / Codex CLI / ChatGPT / Gemini / Cursor / Aider / OpenCode / Continue / Copilot。另有 `ai-check/` 目录。
6. **许可证**：MIT。
7. **热度**：468 ★ / 49 fork。
8. **审的版本**：`4ec797314537ec9c2105f276d4561d240a0390ba`，2026-07-10。

### 3.13 kylehughes/writing-prose-like-a-human-for-agents

1. **名称 + 链接**：writing-prose-like-a-human-for-agents — https://github.com/kylehughes/writing-prose-like-a-human-for-agents
2. **解决什么问题**：**写作 + 编辑双形态**。Agent Skill 的 description 是「Produces prose that reads as authentically human... **Use when writing or editing** prose, documentation, READMEs, PR descriptions」——即在生成时直接套用；Subagent `prose-humanizer` 则只做编辑（「edits prose in place, applying five rules... Cuts rather than rephrases」）。五条规则：cut significance inflation / use plain verbs / end sentences at the fact / vary rhythm / earn every adjective。
3. **依据**：**经验清单**。Core Principle 给的成因解释是「回归均值」（regression to the mean），举例对照 before/after；无统计、无引用。理论框架与 §3.3、§3.14 同源（都比较接近维基百科那套「重要性膨胀 / 表面分析」的描述）。
4. **语言覆盖**：英文。
5. **打包与调用形态**：Claude Code 插件（skill + subagent），通过 `/plugin marketplace add` 安装，subagent 直接原地改文件并把改动摘要返回（把改写挪出主 agent 上下文）。
6. **许可证**：**NOASSERTION**（GitHub 识别为自定义/无法归类，引用前需读 LICENSE 原文）。
7. **热度**：20 ★ / 0 fork。
8. **审的版本**：`87233cb9e0e5d10b5fa6872cc391aaa291c9ac69`，2026-02-23（Release 1.1.0；此后未再更新）。

### 3.14 Wikipedia:Signs of AI writing（WikiProject AI Cleanup）

1. **名称 + 链接**：Wikipedia:Signs of AI writing — https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing （姊妹页 Wikipedia:Signs of AI-generated comments；配套 Wikipedia:WikiProject AI Cleanup/Guide and resources）
2. **解决什么问题**：**检测/标注，且刻意不改写**。它服务的是维基百科的巡查与删除流程（G15「Unambiguously LLM-generated pages」）。
3. **依据**：**观察清单，作者自陈得非常明确**：「this list is descriptive, not prescriptive; it consists of **observations, not rules**」，是「a field guide」，每类特征配真实条目 diff 的例文；同时在「AI detection tools」「Your detection ability」两节引研究说明检测工具与人类判断都不可靠（例如 2025 年研究称人类区分 LLM 文本的能力不优于随机；重度 LLM 用户约 90%）。所以它**既有大量真实案例，又主动声明自己不是规则、不是判据**——这一点比多数下游 skill 诚实。
4. **语言覆盖**：英文维基（其他语言维基有各自对应页/译本，未逐一核）。
5. **打包与调用形态**：维基页面（知识库），**没有代码**。但它是整个生态的事实上游：blader/humanizer 明写 based on it，op7418 明写原项目基于它，多数英文人的规则表都能追到它。
6. **许可证**：**CC BY-SA 4.0**（页面页脚实测）。注意：这与 MIT 的 skill 混用时的署名/同许可义务不同，聚合类项目要单独处理。
7. **热度**：不适用（维基页面）。wikitext 220,414 字节、18 个二级标题：9 组内容类目（Content / Language and grammar / Style / Communication intended for the user / Markup / Citations / Comment-specific indicators / Edit summaries / Miscellaneous）+ 3 张反向表（**Signs of human writing** / **Ineffective indicators** / Historical indicators）+ Caveats 与 5 个附录节。那 3 张反向表是它比下游 skill 更有价值的部分——下游几乎没人抄「哪些看起来像 AI 其实不是」。
8. **审的版本**：pageid 75478314，**revid 1374941330**，2026-09-14T23:46:58Z（编者 Fences and windows）。页面顶部挂着维护横幅「Parts of this page (those related to the most recent models) need to be updated (August 2026)」——**规则随时间失效的问题在这个「根知识库」上同样存在**。

### 3.15 vale-cli/vale

1. **名称 + 链接**：Vale — https://github.com/vale-cli/vale （注意：原 `errata-ai/vale` 已迁至 `vale-cli/vale`，`gh api repos/errata-ai/vale` 会跟随重定向）。
2. **解决什么问题**：**在写作过程中与 CI 里约束文本**——把风格指南变成可执行 lint（markup-aware）。它不做 AI 检测，也不生成文本，但提供了「起草时就受规则约束」的**工程化载体**：编辑器实时提示 + pre-commit / CI 卡口。
3. **依据**：**人工规则**（YAML 规则包，如 Google / Microsoft / write-good 等风格包），非统计实证。
4. **语言覆盖**：规则语言无关（社区有各语种规则包）。
5. **打包与调用形态**：Go CLI（单二进制）+ 可分发规则包；被大量文档仓库接进 CI。
6. **许可证**：MIT。
7. **热度**：6109 ★ / 225 fork。
8. **审的版本**：`0194fbbdd85f600caf4ff055c86bd6ed076e4b79`（默认分支 `v3`），2026-09-17。
9. **为什么列它**：它是「把写作规范做成机器可验证门禁」这一路径的成熟参照——本版图里做去 AI 味的项目**没有一个达到这种工程成熟度**（最接近的是 oh-story 的确定性脚本与 hook，但仅限网文工作流）。

### 3.16 Hello-SimpleAI/chatgpt-comparison-detection（HC3）

1. **名称 + 链接**：HC3（Human ChatGPT Comparison Corpus）+ Detectors — https://github.com/Hello-SimpleAI/chatgpt-comparison-detection
2. **解决什么问题**：**文本检测**（人机对照语料 + 检测器 + 在线 demo），不改写、不生成。
3. **依据**：**统计实证**——人机平行语料（同一问题的 ChatGPT 回答 vs 人类回答），并做检测器评测；是中文侧少有的公开对照语料。
4. **语言覆盖**：**中英双语**（HC3-English / HC3-Chinese，含 reddit_eli5、open_qa、wiki_csai、medicine、finance、psychology 等子集）。
5. **打包与调用形态**：数据集（HuggingFace + ModelScope）+ Python 检测器代码 + Demo（可自建在线服务）。
6. **许可证**：数据按子集来源分别适用许可，仓库声明「若子集来源许可比 CC-BY-SA 更严则从上游，否则 CC-BY-SA」——子集含 CC-BY-NC 4.0（medicine）、未知许可（nlpcc_dbqa）等。**仓库级 `license` 字段为 null，不能简单当成 CC-BY-SA 全量使用。**
7. **热度**：1460 ★ / 128 fork。
8. **审的版本**：`1f8c15c28f87e09a5abfd86ee6e15005dc7d2119`，2023-06-27（仓库自 2023-12 后基本停更）。**时效性提示：语料是 2023 年的 ChatGPT，与 2026 年的前沿模型分布已不能直接对齐**——sepia 的中文校准仍引用它，并自陈了这一局限。

### 3.17 零样本检测器群体（作为一个类目）

| 项目 | 链接 | 依据 | 形态 | 许可 | ★ / fork | 审的版本 |
|---|---|---|---|---|---|---|
| DetectGPT | https://github.com/eric-mitchell/detect-gpt | 统计实证（概率曲率，ICML 2023） | 论文代码 / Python | MIT | 477 / 72 | pushed 2023-03-04 |
| Fast-DetectGPT | https://github.com/baoguangsheng/fast-detect-gpt | 统计实证（ICLR 2024） | 论文代码 / Python | MIT | 433 / 85 | `971b052` 2026-02-07 |
| Binoculars | https://github.com/ahans30/Binoculars | 统计实证（ICML 2024，零样本） | Python 库 | BSD-3-Clause | 416 / 67 | pushed 2024-05-14 |

- **解决什么问题**：检测（给分数/判定），不改写。共同点：零样本、需要本地跑模型、维护基本停滞（2023–2024）。
- **补充线索（未作为条目）**：Gx664/AIGC（5 ★、MIT、本地检测工具箱，多引擎 SimpleAI/GLTR/Fast-DetectGPT，中英双语界面，`8aa6416` 2026-09-13）说明「把开源检测器包成本地工具」这个细分也有中文长尾；维基页面点名的 GPTZero、Pangram 属商业在线服务，无开源代码，不作条目。

### 3.18 传统写作风格指南仓库（作为对照）

| 项目 | 链接 | 解决什么 | 依据 | 语言 | 许可 | ★ / fork | 审的版本 |
|---|---|---|---|---|---|---|---|
| Microsoft Style Guide | https://github.com/MicrosoftDocs/microsoft-style-guide | 机构写作规范 | 机构规范 | 英文 | CC-BY-4.0 | 192 / 88 | `c6945c3` 2024-11-13 |
| 18F Content Guide | https://github.com/18F/content-guide | 政府内容写作规范 | 机构规范 | 英文 | NOASSERTION | 84 / 66 | pushed 2023-12-14 |

**为什么列**：它们是「写作风格指南仓库」这一形式的成熟样本（规则成文、可引用、可被 §3.15 的 linter 消费），但**与去 AI 味生态几乎没有交集**：不处理 AI 痕迹，也没有 agent 集成。这个断层本身就是空白点的证据（见 §6）。

---

## 4. 关键问题：有没有项目在约束「从零起草」而不是事后润色？

### 4.1 直接回答

**有，不是「没有找到」。** 明确的至少 6 个：**oh-story-claudecode、human-writing、sepia、OUBIGFA、deai、harshaneel/humanize**；另有 3 个只在描述里声称覆盖 drafting（stop-slop、kylehughes 的 skill 部分、ContractorKeith）。但**没有任何一个把它做成「不可绕过的起草前硬门禁」**（除了 oh-story 在网文这类垂直场景里做到了，见下），主流实现是**把同一份规则清单在生成时也读一遍**。

### 4.2 它们具体怎么做的（四种实现形态）

**形态 A：起草前的准备/材料门禁 —— 最接近「硬约束」**

- **oh-story-claudecode**（唯一有真门禁的）：
  - `story-long-write/SKILL.md` 开头即写「任何创建或修改长篇故事文件的动作前，先判断场景并完成本轮门禁……**只读本 SKILL.md 不算完成**；`rg` 检索或局部摘读也不算完整读取」「任一必需路径不存在、不可读或未读完时立即停止，报告准确路径，**不得先写正文再补读**」。这是把「读全设定/大纲」当成了写正文的前置条件。
  - `story-deslop` 的「预防 · 三遍去AI法」+ README 的能力表把去 AI 味标注为「预防」；`story-setup` 部署 **8 个自动化 hook**（含 `detect-story-gaps.sh` 在会话开始检测设定缺口、大纲缺失、伏笔断线）。
  - 确定性的写作 lint：`scripts/check-ai-patterns.js --check --fail-on=blocking`，blocking 类别（`not-is-comparison` / `em-dash` / `voice-contrast` / `negation-parade` / `reverse-not-is` / `trailer-ending` / `trailer-summary`）**并入 Gate B**；另有 `check-degeneration.js` 检测模型退化（逐字复读、末尾截断、占位符、工程词泄漏）。注意其自述边界：blocking 只限确定性句式/标点，其余按读感。
- **human-writing**：`## 动笔前先找到说话位置` 要求动笔前在内部回答五个问题（谁在说、凭什么知道、哪些只是推测、手里有什么能托住文章的东西、读者下一步会追问什么），并给出**停止条件**：「现实材料不够时先停在这里」「现实稿要求直接写而且无法补材料时，宁可交一篇更短、更实的作品」「篇幅是目标，材料边界是底线」「不要先交一篇空稿」。这是「材料门禁」而非「风格门禁」，但对起草的约束力比任何风格规则都强。
- **deai**：第 0 步「预检」写「材料/信息守恒、说话位置、网文别误伤」，且第 1 步架构在「新写」档位下需要**先报告症状、动刀前要授权**。

**形态 B：生成时的风格提示（把清理规则在起草时预置）——最主流**

- **human-writing** `## 第一稿直接带着人写`：直接规定第一稿的推进方式（开头尽快碰到事情、不预先命名结构、一段完成一件事、新段落必须带来新东西、写到事情讲完就停），并给正反例（「他毕业后离开上海，去了成都……」比「他关掉一条好走的路，把命运押上赌桌」更接近目标）。
- **sepia 的 `write` 操作**：`/sepia-write` 绑定 canonical skill 的 write 路由，走同一条三遍协议（架构 → 语篇 → 表面），原则是「校准到人类分布，不要反转 AI 分布」（每篇只挑 3–5 个动作、留白），并额外提供 `sepia-hemingway`（写作时直接套海明威声音）与 `references/voice-skills.md` 的声音 skill 叠加接口。
- **OUBIGFA `good-writing`**：从 7 篇文章提取「写作 DNA」当生成底座；README 明说适用「从零生成、改写、翻译、审阅、精修」五种任务。
- **deai「新写」档**：从无到有，默认落点就是去 AI 味。
- **harshaneel/humanize**：`Generating human text from scratch` 要求「从第一句起应用全部九个 lever」，并给开头/结尾的反模式。
- **stop-slop**（17250 ★）：description 写 `Use when drafting, editing, or reviewing text`，但正文规则与 Quick Checks 都是交付前检查，**实质仍是改稿清单**。
- **kylehughes 的 Agent Skill**：description 写 `Use when writing or editing prose`，五条规则本身是生成可用的正向要求（be specific / plain verbs / end at the fact）。**ContractorKeith/ai-writing-skill**（1 ★、无许可证、2026-06-21）自述是「Claude Code skill that writes articles and blog posts that read like a human wrote them」——纯起草向，但热度与可信度都很低，仅作存在性证据。

**形态 C：生成参数层约束（唯一一个管到解码参数的）**

- **harshaneel/humanize**：`Generating human text from scratch` 给出 temperature 0.9–1.1、top-p 0.95–0.99、repetition penalty 1.1–1.2，理由是「拓宽 token 分布、破坏困惑度检测器依赖的局部极大值（引 RAID benchmark）」。这是本版图里**唯一一个把约束下沉到采样参数**的方案——但它的实证依据在仓库内极薄（见 §3.12）。

**形态 D：模板 / 风格 DNA（起草时可填充的结构）**

- **OUBIGFA** 的 `.writer/` 作者 DNA；**human-writing** 的 `references/formats.md`（文体模板）；**sepia** 的 `references/voices/` 内置 Hemingway profile；**oh-story** 的 `大纲.md / 卷纲 / 细纲（1 章 1 文件）` 文件模板 —— 起草被拆成「先填结构、再填字」，风格约束在结构层就生效。

### 4.3 明确只做事后改写的

lieflat-less-ai-tone（**frontmatter 自述「适用于写作完成后的成稿清理」**）、blader/humanizer（Rewrite AI-sounding text；输入必须是已有文本）、op7418/Humanizer-zh（编辑/审阅）、petergyang/no-ai-slop（Two jobs = Edit / Detect；只有讽刺性生成）、slivenred 繁中版（同上）、kylehughes 的 subagent（原地编辑）、Wikipedia:Signs of AI writing（明确只标注不改写）、Vale（lint 现有文本）、HC3 与三个检测器（只判定）。

### 4.4 结论的边界

- 「起草期约束」在本版图里**普遍是软的**：它是「让 agent 在写的时候也读一遍规则」，没有校验、没有阻挡、没有可复现的失败信号。
- 唯一把起草做成**带阻断语义的门禁**的是 oh-story，而它是**网文垂直**场景（有明确的大纲/设定文件结构可检查），这套做法能否迁移到「任意语体、任意长度」的通用写作，**没有任何项目验证过**。
- 「生成态」与「清理态」用**同一份规则表**是常规做法；唯一显式拆开的是 deai（四档分流程）与 sepia（四操作分路由），但两者拆的是**操作流程**，不是**规则内容**——没有人为生成态单独设计规则集。

---

## 5. 分布规律（12 条）

1. **形态高度单一**：清一色是 Agent Skill（`SKILL.md` + `references/`），不是库、不是在线服务。真正的 Python 库/服务出现在**检测**一侧（HC3、DetectGPT 系），不在改写一侧。
2. **时间线三波**：2023 年检测/数据集波（HC3、DetectGPT）→ **2026 年 1 月 skill 引爆波**（stop-slop 01-11、blader/humanizer 01-18、op7418 01-19、OUBIGFA 01-21）→ 2026 年 8–9 月中文系第二波（sepia 08-28、deai 09-06、lieflat 08-20）。
3. **热度极度头部集中**：49306 / 17414 / 17250 / 10197 ★ 四个头部之后直接掉到 6.9k / 3.7k / 2.7k / 1.7k，再往下是几百和个位数长尾。
4. **热度与证据强度反相关**：四个最高热项目（blader/humanizer、Humanizer-zh、stop-slop、no-ai-slop）**全部是经验清单或翻译**；做统计实证的三个（lieflat、sepia、HC3）都在中腰部以下。
5. **上游单一化**：英文生态的规则祖先几乎都能追到维基百科 Signs of AI writing（blader/humanizer 与 op7418 明写）。中文生态则出现「翻译链」：blader → op7418 → OUBIGFA，且 stop-slop 也被 op7418 引用。
6. **规则高度趋同**：无论中英，被反复点名的是同一批——「不是 X 而是 Y」翻案腔 / 破折号（英文侧连 em dash 都禁）/ 三段式排比 / 重要性膨胀（testament、pivotal、见证）/ 表面分析（-ing 分词尾巴）/ 喉清式开头 / 假深刻结尾 / 同义词轮换。说明这些标记跨语言可迁移，**但阈值与误伤判断必须本地化**（lieflat 恰好在中文里证伪了其中 15 条）。
7. **误伤控制是分水岭**：做得细的项目都在防过度清理——lieflat 用白名单 + 「不作为改写理由」表；blader/humanizer 用「weak alone 需共现」；sepia 用「每篇只挑 3–5 个动作、不反转 AI 特征」；deai 用 A/B/C 分级 + 作者风格优先；oh-story 用「过度清理保护 + 退化检查 + 删除比例上限」。**只在规则表里列模式而不写误伤边的项目，是把用户文本当靶子。**
8. **垂直化正在发生**：网文（oh-story、sepia 的 fiction 路线）、专业文本（sepia 按 venue 分规则：release notes / PR 回复 / postmortem / ticket / 技术文章 / 长报道）、中文非虚构（human-writing 的知乎/公众号/博客）——「通用去 AI 味」正被切成场景。
9. **事后改写是绝对主流**：本报告逐个审的 21 个项目里，**明确覆盖起草约束的 6 个**（human-writing、sepia、oh-story、OUBIGFA、deai、harshaneel），**仅在描述里声称覆盖 drafting 的 2 个**（stop-slop；kylehughes 的 skill 部分，其 subagent 仍只做编辑），其余 13 个只做事后改写、检测或规范制定。起草期是新前线，不是已解决问题。
10. **许可分层混乱**：MIT 是默认，但混着 CC BY-SA 4.0（维基上游）、NOASSERTION（kylehughes）、无许可证（OUBIGFA、ContractorKeith）、数据集多许可（HC3）。**任何聚合类项目都必须逐源记许可**（deai 的 `SOURCES.md` 是目前唯一做了这件事的）。
11. **工程化程度普遍偏低**：只有 sepia（`evals/` + `tests/` + CI behavioral eval）与 oh-story（确定性脚本 + 8 个自动化 hook）做到了面向行为的可复现验证；harshaneel 有 `tests/` 目录，但其规则依据的引用文件只有一个 3.7KB 的 `research.md`。其余项目连一个 eval 都没有。
12. **时效性是结构性问题**：维基页面顶部挂着「most recent models need to be updated」；lieflat 因模型换代推翻过自己的结论（「早期只用 2 个模型 30 篇，得出的结论后来被推翻大半」）；HC3 语料停在 2023。**没有项目做规则的「失效期 / 复测触发机制」**。

---

## 6. 空白点（对 Watch-Your-Language 的启发）

1. **生成态缺一份独立规则集**。现有项目要么复用清理规则表，要么只做流程分档（deai / sepia）。**没人回答「起草时该被约束的是什么」**——从第一性原则看，生成态该管的是选材、推进、结构、说话位置（human-writing 与 sepia 架构层最接近），而不是 em dash 计数。这是一个明确的产品空位：「起草约束」与「清理约束」应当共享证据库、但用不同的规则投影。
2. **没有可机器验证的起草门禁（通用场景）**。oh-story 证明了「写正文前门禁 + hook + blocking 脚本」可行，但只在网文文件结构下成立。通用写作缺一个「下一段之前必须通过什么」的可执行定义——这恰恰是本项目最有价值的位置。
3. **负样本库无人沉淀**。只有 lieflat 系统列了 15 条**被实测否掉**的流行特征（且只有中文、只有一仓）。英文生态没有对应的「反误伤表 / 已被证伪的特征清单」。把「哪些流行特徵不该改」做成公共资产，比再加 20 条禁用词有价值得多。
4. **没有跨语言的统一证据层**。中英生态几乎不互相引用（唯一桥是翻译链与 deai 的合并）。HC3 是中英双语对照语料但停在 2023；lieflat 的 283 万字语料是中英不通的。**「同一批标记在中英两侧的倍率是否一致」这个问题没人测过**——这是最便宜也最有区分度的原创研究。
5. **没有可复现的评测集**。规则表满天飞，没有一个共享的「人味 / 去 AI 味」评测集与评分方法（sepia 的 evals 是自用、harshaneel 的「50+ 来源」在仓库里只剩 3.7KB）。谁先做出「同一批文本 × 各项目规则 × 可复现评分」的公开对比，谁就拿到这个领域的话语权。
6. **「生成时约束」到「采样参数」只有一例且证据很薄**。harshaneel 给了 temperature/top-p 建议（引 RAID），但没给仓库内可核验的测量。这是一个既有理论价值又有工程落点的方向（尤其对有本地推理控制权的 agent harness）。
7. **规则的时效机制缺失**。模型换代会让规则整批失效（lieflat 自陈推翻过自己、维基页面挂着待更新横幅）。**给每条规则打「测于哪个模型版本 / 何时复测」的字段**，是一个低成本的差异化设计。
8. **许可与聚合是真实风险**。生态里存在无许可证（OUBIGFA 791 ★，还被中文圈广泛引用）、NOASSERTION、CC BY-SA 与 MIT 混用的情况。若本项目要吸收同类规则，应当像 deai 那样从一开始就有 `SOURCES.md`，并把「方法借鉴」与「文本复制」分清楚。

---

## 7. 附录：复核方式与已知不确定项

### 7.1 复核命令

```bash
# 起点两仓：直接克隆读原文 + 取版本
git clone -q --depth 1 https://github.com/larashero3-dotcom/lieflat-less-ai-tone.git
git clone -q --depth 1 https://github.com/KKKKhazix/human-writing.git
git -C lieflat log -1 --format='%H %cI'

# 元数据（star/fork/许可/创建时间/默认分支）
gh api repos/<owner>/<repo> \
  --jq '{stars:.stargazers_count,forks:.forks_count,lic:(.license.spdx_id//"none"),created:.created_at,default:.default_branch}'

# 审的 commit SHA（部分仓库的 /commits 接口会 TLS 超时，改用 branches/<default>）
gh api repos/<owner>/<repo>/branches/<default> \
  --jq '{sha:.commit.sha,date:.commit.commit.committer.date,msg:(.commit.commit.message|split("\n")[0])}'

# 原文（本机 web_fetch 不可用）
curl -sL --max-time 30 -A "Mozilla/5.0 research" \
  https://raw.githubusercontent.com/<owner>/<repo>/<branch>/SKILL.md

# 维基页面版本
curl -sL "https://en.wikipedia.org/w/api.php?action=query&prop=revisions&titles=Wikipedia%3ASigns%20of%20AI%20writing&rvprop=ids%7Ctimestamp%7Cuser%7Csize&rvlimit=1&format=json"

# StoryScope 的 LAMP 数字核对（PDF 压缩，先转文本）
curl -sL -A "Mozilla/5.0 research" https://arxiv.org/pdf/2604.03136 -o storyscope.pdf
pdftotext storyscope.pdf ss.txt && grep -n -B3 -A3 "95.5" ss.txt
```

### 7.2 已知不确定项（如实标注）

- **star 数是快照**：2026-09-17 实测，头部项目日增可观，几天后即会漂移。
- **sepia 引用的 per-model fingerprints**（Claude / GPT / Gemini 各版本的行为差异）来自其 `research/` 目录与厂商自己的 prompting guide；我核对了它的**主要实证来源 StoryScope 论文原 PDF**（93.2% / 95.5%→93.9%），但**没有**逐个复核它全部 vendor guide 引用。
- **harshaneel/humanize 的「50+ peer-reviewed sources」未获仓库内证据支持**（`references/` 只有一个 3.7KB 文件）；README 的参考文献列表较长但未与正文逐条对应。此处按「宣称与交付不一致」记录，不代表它引用的文献不存在。
- **维基页面**只说「部分内容需按最新模型更新」（2026-08 横幅），所以其特徵清单对 2026 年模型的有效性未知。
- **未逐一核实的类别**：中文自媒体里流传的闭源/付费「去 AI 味」提示词（如各公众号版本）、商业检测服务（GPTZero、Pangram、朱雀）、以及其他语言维基的对应页面。
- **oh-story 的仓库迁移**：deai 的 `SOURCES.md` 仍写作 `worldwonderer/oh-story-claudecode`；实测 `gh api repos/worldwonderer/oh-story-claudecode` 返回 `zenstory-ai/oh-story-claudecode`（重定向，创建时间一致），引用时以新地址为准。
- **blader/humanizer 是否含中文**：我只核了 `SKILL.md`（英文）与仓库文件列表，未穷举其 agents/scripts 内容。

### 7.3 未纳入的类别（有意排除）

- **通用提示词技巧库**（如 awesome-chatgpt-prompts 一类）：与「去 AI 味」不是同一问题。
- **AI 水印 / provenance 技术**（C2PA、SynthID）：解决归属而非风格。
- **文学风格模仿 / 作者声音克隆**（除 sepia 的 voice 接口与 OUBIGFA 的作者 DNA 外）：题目与「说人话」部分重叠但目标不同，本次仅在相关处提及。
