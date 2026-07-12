# WeChat Writing — Manual

> Deep usage guide for the `wechat-writing` skill. Read this when you are integrating the skill into a new assistant, debugging unexpected output, or trying to push past the obvious use cases.

---

## 1. Operating principles (read once)

The skill encodes five positions, listed in order of how often they bite output:

1. **Restraint > volume.** A 1,400-character article that lands its judgment beats a 2,200-character article that hedges it. The skill prefers under-length to over-length.
2. **Mechanism > assertion.** "Good doctors + good plans ≠ good results" — every claim that survives review must point to a mechanism (medical / operational / aesthetic / psychological / structural).
3. **Negation > affirmation.** A surprising amount of the writing power comes from saying what the topic is NOT. Section 4 of `SKILL.md` lists the explicitly banned phrases — learn them, ban them at the model level if you can.
4. **Negative space > completeness.** Don't explain every objection. Don't write a "service / professional / management" trio. Let the reader finish the judgment.
5. **Cross-discipline honesty.** If medical content appears, mechanism / indication / execution / variability / short-term / long-term must be separate. Never collapse them.

These are the load-bearing walls. If your output violates one, fix it before ship.

---

## 2. Three modes in depth

### 2.1 `title`

**Trigger words:** 标题 / 爆款 / 封面 / 标题方向 / 标题诊断 / 起 10 个标题

**Default output:** 10 titles in a 3-3-2-2 mix:

| Slot | Count | Flavor                  | Job                                               |
| ---- | ----- | ----------------------- | ------------------------------------------------- |
| A    | 3     | 传播型                  | propagate; click-worthy without being cheap       |
| B    | 3     | 行业判断型               | industry credibility; reads as expert commentary   |
| C    | 2     | 克制高阶型               | restraint; pulls a narrower, sharper audience     |
| D    | 2     | 反直觉型                 | counterintuitive; rewards a reader who finishes it |

Then select the strongest 3 and annotate with: suitable audience · propagation advantage · possible risk.

**Tuning knobs you can pass to the model:**

- "需要反差更强的"
- "克制一下,不要传播型"
- "加一两个更长的(30+ 字)"
- "更冷一点的行业判断"

**Anti-patterns to call out:**

- All titles phrased as questions → usually signals low effort. ≤ 30% questions.
- Same sentence skeleton repeated 10 times → structural defect, regenerate.
- ≥ 1 title using 震惊 / 99% / 彻底颠覆 / 不看后悔 → reject and regenerate.

### 2.2 `draft`

**Trigger words:** 写一篇 / 重新撰写 / 给我一篇 / 输出公众号 / 根据材料成文

**Default deliverable:**

1. 3 alternative titles (one each from slots A / B / C above — drop D unless asked).
2. Cover copy ≤ 100 Chinese characters, single sentence.
3. Complete article, default 1,800–2,200 characters.

**Length guidance:**

| Length          | When                                                              |
| --------------- | ----------------------------------------------------------------- |
| 1,200–1,500 字 | topic is dense judgment; reader is expert                         |
| 1,800–2,200 字 | default for 公众号行业评论 / 审美评论                              |
| 2,500–3,000 字 | explainer with on-page mechanics; only when topic has hidden layers |

**The 6-step progression** (`references/draft.md`) is a license, not a checklist. Skip steps that don't apply, combine them, reorder them. The test is: does the article land a judgment with mechanism? Not: does the article hit all six steps in order?

**Opening checklist:**

- enters via scene / number / question / detail / contradiction / case / fact? ✓
- central judgment within paragraphs 3–5? ✓
- no industry background first? ✓
- no banned opening phrases? ✓

**Action recommendations** must specify: what · why · sequence · success criteria · what NOT to do. "提升服务" is a failure. "在术后第 3 / 7 / 30 天主动随访,把参数同步到私域档案,并把不复诊的客户标记为高流失风险" is a pass.

### 2.3 `polish`

**Trigger words:** 优化 / 精修 / 润色 / 改写 / 去AI味 / 改一下

**Default output:** two sections, in this order:

```
### 精修诊断       (300–500 字, concrete)
### 精修后的完整文章 (no annotations)
```

If the user only asks for the rewrite ("直接给我改好的"), drop the diagnosis and output the article directly.

**What the diagnosis must contain:**

| Slot            | Job                                                        |
| --------------- | ---------------------------------------------------------- |
| 值得保留         | 2–3 specific things — not "整体节奏"                       |
| 主要结构问题     | one paragraph                                              |
| 主要语言问题     | one paragraph                                              |
| 应删除/压缩/前移的段落 | call out specific passages (cite by line or quote first 6 chars) |
| 缺失的机制       | name the absent layer                                      |
| 编辑策略         | 1–2 sentences                                              |

**What the rewritten article must NOT do:**

- turn sharp judgments into polite suggestions
- flatten the writer's voice into standard essay prose
- add disclaimers that weren't in the original
- insert AI-transition phrases that weren't there
- rewrite metaphors that worked

If the article is already strong, the diagnosis should say so honestly and the rewrite can be light. Don't manufacture problems.

---

## 3. Cross-platform install & trigger

### 3.0 NPX Skills (recommended for multi-agent users)

[skills.sh](https://skills.sh) is a community registry + CLI for installing Skills (filesystem-resident prompt workflows) into any supported agent in one step.

```bash
# install latest
npx skills add sooogooo/wechat-writting-2026

# install a pinned version (good for reproducibility)
npx skills add sooogooo/wechat-writting-2026 --version v0.1.0

# find skills in the registry
npx skills find wechat

# update to the latest released version
npx skills update wechat-writing
```

| Prerequisite           | Required?  | Note                                       |
| ---------------------- | ---------- | ------------------------------------------ |
| Node.js ≥ 18           | yes        | ships with `npx`                           |
| A supported agent      | yes        | Claude Code · Cursor · Gemini · Copilot · VSCode · etc. |
| Internet access        | yes        | to pull from the registry                  |
| Git on PATH            | no         | the CLI handles clone resolution itself    |

What NPX Skills does for you:

- Pulls the repo (or the specific release tarball).
- Resolves the `SKILL.md` frontmatter and figures out the right drop-in path per agent.
- Auto-registers the slash trigger (frontmatter `name:` becomes the `/command`).
- Lets you update or remove with `update` / `remove` — no more hunting through `~/.claude/skills/` to find where you cloned it.

When to choose NPX Skills vs manual `git clone`:

- Choose **NPX Skills** if you want one command across multiple agents, or if you want version pinning and easy removal.
- Choose **manual `git clone`** if you want to develop or fork the skill locally (e.g., you're contributing back).

### 3.1 Claude Code — manual

```
# global
git clone https://github.com/sooogooo/wechat-writting-2026 ~/.claude/skills/wechat-writing
```

Trigger: `/wechat-writing <prompt>` — frontmatter `name: wechat-writing` becomes the slash command.

### 3.2 Codex CLI / OpenAI Codex
Two options.

**Option A — symlink into instructions/**

```bash
mkdir -p ~/.codex/instructions/wechat-writing
ln -s "$(pwd)/SKILL.md"        ~/.codex/instructions/wechat-writing/SKILL.md
ln -s "$(pwd)/references"      ~/.codex/instructions/wechat-writing/references
```

**Option B — AGENTS.md bridge**

Drop this at your project root as `AGENTS.md`:

```markdown
# Writing skill — wechat-writing
Read these files before responding to any writing request:
- ~/.config/wechat-writing/SKILL.md
- ~/.config/wechat-writing/references/title.md
- ~/.config/wechat-writing/references/draft.md
- ~/.config/wechat-writing/references/polish.md
```

Codex auto-loads `AGENTS.md` from the project root.

### 3.3 Cursor

Symlink under `~/.cursor/skills/wechat-writing/`. Trigger via `@wechat-writing <prompt>` in the composer.

### 3.4 Continue / Cline / JetBrains AI / Copilot Workspace

Each loads filesystem-resident instruction files. Drop the whole folder under their `skills/` or `commands/` directory; their slash-command triggers should auto-recognize `SKILL.md` frontmatter. If they don't, refer to their respective docs for `AGENTS.md` / `INSTRUCTIONS.md` / `.cursorrules` equivalents.

### 3.5 Raw API use

```python
SYSTEM = open("SKILL.md").read()
REFERENCE = {
    "title":  open("references/title.md").read(),
    "draft":  open("references/draft.md").read(),
    "polish": open("references/polish.md").read(),
}
# detect mode from user prompt → pick reference → inject after system
```

---

## 4. Troubleshooting

### 4.0 NPX Skills specific

- **`npx: command not found`** — Node.js / npm not on PATH. Install Node 18+ from <https://nodejs.org>.
- **`skill not found in registry`** — the repo hasn't been indexed yet. Wait a few minutes, or use the manual `git clone` recipe in §3.1.
- **`Permission denied` when installing globally** — prefix with `sudo` on macOS / Linux, or use `npx skills add ... --prefix ~/.local` to install user-scoped.
- **Skill installs but slash command is missing** — the agent may need a restart. For Claude Code: `/exit` then re-enter; for Cursor: reload the window (`Ctrl/Cmd+Shift+P` → "Developer: Reload Window").
- **Want to remove the skill** — `npx skills remove wechat-writing`, or for the manual install: `rm -rf ~/.claude/skills/wechat-writing` (or the equivalent path for your agent).

### 4.1 Output reads like generic AI

Almost always one of:

1. The assistant didn't load `references/*.md` — it only loaded `SKILL.md`. Force-load:
   - Claude Code: `/wechat-writing` triggers frontmatter dispatch which *should* load references — verify with `/memory show`.
   - Codex: the AGENTS.md bridge only mentions SKILL; add the references.
2. The `polish` mode dropped the original voice too aggressively. Add explicit constraint: "保留原文所有特殊比喻 / 个人节奏 / 行业细节。"
3. The model temperature is too high. For polish, prefer temperature ≤ 0.4.

### 4.2 Title set is homogeneous

You asked for 10 titles and got 10 variations of one skeleton. Force variety:

```
10 个标题,必须有不重复的句式 (假设/不等/真正/正在消耗/不是…而是…/为什么/结束之后),
不允许连续两个标题都用同一个开头词。
```

### 4.3 Article opens with banned phrase

The model is leaking a default behavior. Two ways to fix:

1. Add to your prompt: "如果开头出现 近年来 / 在当今社会 / 爱美之心 这类短语,直接全部删除,从第二段开始。"
2. Refactor `SKILL.md` Forbidden openings into a *negative example block* — most models pattern-match exact strings more reliably than instructed negative rules.

### 4.4 Polish rewrites too aggressively

Tell the model: "只动结构、不动句子"; or "只删除空话和重复、不重写任何比喻". For very strong originals, try "零改动,只在原文中删除空话和重复,其他完全保留。"

### 4.5 Medical claims worry you

Run a verification pass:

```
用以下问题检查上面文章的每一个医疗断言:
- 这是机制还是效果?
- 这是个体观察还是普遍规律?
- 是否给了变化空间 (因人而异 / 取决于)?
- 是否有"零风险 / 永久 / 根治"等绝对词?
凡是不通过的句子,标记并改写。
```

### 4.6 Article is too long

Cut from inside, not at the end. Targets in order:

1. The first paragraph if it has industry background → cut.
2. The mechanism section if it rambles past 3 paragraphs.
3. The action section if it has more than 5 recommendations.
4. The ending if it summarizes or moralizes.

---

## 5. Extending this skill

### Add a new mode (e.g., `outline`)

1. Create `references/outline.md` with the same self-documenting shape as `title.md` / `draft.md` / `polish.md`.
2. In `SKILL.md`, add the mode to the operating-modes table and a short mode-routing rule.
3. In `README.md`, add the trigger words and a one-line description.

### Add a new domain (e.g., legal content)

1. Add a "Boundaries" block to `SKILL.md` listing what the new domain's absolutes look like.
2. Update `references/draft.md` with domain-specific subheading examples.
3. Update `README.md` §"Domains this skill is tuned for".

### Add a language (e.g., English WeChat equivalent)

The skill is Chinese-tuned by intent. Don't bolt on languages. Fork a new `wechat-writing-en` skill instead.

---

## 6. Anti-patterns to never ship

These are documented failures, collected from public outputs. If your output resembles any of these, kill and restart.

| Anti-pattern                                           | Why it fails                                      |
| ------------------------------------------------------ | ------------------------------------------------- |
| End with "让我们一起……" / "未来已来……"                | slogan ending, kills credibility                  |
| Open with "随着消费升级……" / "在当今社会……"           | industry-background filler, kills pacing          |
| Action list: "提升服务 / 强化专业 / 加强管理"          | empty executives                                  |
| Medical claim: "零风险 / 永久根治 / 一次解决"          | absolutism; near-impossible to defend             |
| Every sentence becomes a "gold quote"                  | rhythm crushes; reader disengages                 |
| Subheading: "原因一 / 原因二 / 解决方案"               | textbook structure in editorial writing           |
| Cover copy > 100 Chinese characters                    | WeChat thumb crop; first 32 chars are what readers see |
| Title uses 你以为/99%/彻底颠覆                         | clickbait; loses expert credibility                |
| Body parallels three ideas in a row mechanically       | parallelism reads AI-generated                    |

## 7. License & contributing

MIT © 2026 sooogooo. See [LICENSE](../LICENSE).
Contributions: see [CONTRIBUTING.md](../CONTRIBUTING.md).
