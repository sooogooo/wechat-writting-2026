# WeChat Writing

A writing skill that packages the editorial position of one senior medical-aesthetics practitioner, operator, investor, and aesthetics critic — judgment, restraint, vocabulary, prohibitions, and boundaries — into three operating modes for any sufficiently capable AI assistant.

Works in **Claude Code**, **Codex CLI**, **Cursor**, **Continue**, **Cline**, **GitHub Copilot Workspace**, **JetBrains AI Assistant**, **OpenAI Codex**, and any other AI coding assistant that loads filesystem-resident instruction files.

> 用医生与经营者的双重视角，拆解医美背后的审美、商业与人性。把医美行业里复杂的事讲明白，帮从业者少走弯路，也帮消费者少花冤枉钱。

---

## What is inside

```
wechat-writing/
├── SKILL.md              # frontmatter trigger + shared editorial position
├── references/
│   ├── title.md          # mode 1 — title generation (10 titles, 4 flavors)
│   ├── draft.md          # mode 2 — full article (3 titles + cover + body)
│   └── polish.md         # mode 3 — deep edit (诊断 + 完整重写)
├── docs/
│   ├── MANUAL.md         # deep usage manual — modes, examples, cross-platform
│   └── MARKETING.md      # PR / promotion copy for multiple channels
├── LICENSE               # MIT
└── README.md             # this file
```

## Three operating modes

| Mode     | When                                              | What you get                                         |
| -------- | ------------------------------------------------- | ---------------------------------------------------- |
| `title`  | 标题 / 爆款标题 / 封面文案 / 标题方向 / 标题诊断   | 10 titles — 3 传播 + 3 判断 + 2 克制 + 2 反直觉;再选 3 个最强并说明理由 |
| `draft`  | 写一篇文章 / 重新撰写 / 给我一篇公众号正文       | 3 备选标题 + 封面文案 + 1,800–2,200 字正文            |
| `polish` | 优化 / 精修 / 润色 / 改写 / 去AI味                | 300–500 字精修诊断 + 完整重写文                       |

The mode is inferred from the user request — no need to declare it. If the request mixes drafting and polishing, finish the asked-for artifact and stop.

## Install

### NPX Skills (recommended — works across Claude Code, Cursor, Gemini, Copilot, VSCode)

```bash
# install latest
npx skills add sooogooo/wechat-writting-2026

# install a pinned version
npx skills add sooogooo/wechat-writting-2026 --version v0.1.0

# list / check available skills
npx skills find wechat
```

The registry site: [skills.sh](https://skills.sh).
After install, the skill is auto-recognized by supported agents — typically no restart required.

### Claude Code — manual

```bash
# option A — global
git clone https://github.com/sooogooo/wechat-writting-2026 ~/.claude/skills/wechat-writing

# option B — project-scoped
git clone https://github.com/sooogooo/wechat-writting-2026 .claude/skills/wechat-writing
```

Trigger:
```
/wechat-writing 帮我写一篇关于医生 IP 的公众号文章
```

### Codex CLI / OpenAI Codex

Symlink the references into your Codex instructions directory:

```bash
mkdir -p ~/.codex/instructions/wechat-writing
ln -s $(pwd)/SKILL.md           ~/.codex/instructions/wechat-writing/SKILL.md
ln -s $(pwd)/references/*.md    ~/.codex/instructions/wechat-writing/
```

Or use the AGENTS.md bridge (see `docs/MANUAL.md` §3).

### Cursor

Drop the whole folder under `~/.cursor/skills/wechat-writing/`, then trigger via `@wechat-writing` in the chat composer.

### Continue / Cline / other

Place the whole folder under their respective `skills/` (or `commands/`) directory. Their slash-command triggers should auto-recognize the `SKILL.md` frontmatter.

For direct API use: load `SKILL.md` as a system-prompt prefix; attach the relevant `references/*.md` after the user picks a mode (or auto-detect and attach).

## Quick start

After installation, try these in order:

```
/wechat-writing 帮我起 10 个关于医美机构现金流危机的公众号标题
/wechat-writing 写一篇关于"医生 IP 不是短视频"的公众号文章
/wechat-writing 帮我精修下面这篇文章:[paste your draft]
```

## Domains this skill is tuned for

medical aesthetics · body aesthetics · healthcare management · consumer culture · industry commentary · doctor IP · compliance · device investment · anti-aging · regenerative medicine · longevity medicine

## Tone commitments

- calm, restrained, sharp, clear, natural
- intellectually dense without academic
- professional without sounding like a manual
- critical without becoming angry
- readable to ordinary readers, credible to industry professionals

Banned openings: "近年来,随着……" / "在当今社会……" / "爱美之心人皆有之……" / "随着消费升级……" / "不可否认的是……".
Banned transitions / endings: "值得注意的是" / "需要指出的是" / "从本质上来说" / "综上所述" / "总而言之" / "未来已来" / "希望这篇文章能……".
Medical absolutism banned: "零风险" / "永久" / "根治" / "最安全" / "百分之百有效" / "适合所有人" / "一次解决" / "完全没有恢复期".

## Documentation

- `SKILL.md` — full operating principles (read this first if you are integrating)
- `docs/MANUAL.md` — deep usage guide with examples for each mode, cross-platform install recipes, and a troubleshooting section
- `docs/MARKETING.md` — PR / launch copy for公众号、知乎、即刻、X、小红书

## Contributing

Issues and pull requests welcome. See [CONTRIBUTING.md](CONTRIBUTING.md) for voice & review criteria (the editorial bar in `SKILL.md` §"Writing style" applies to PR descriptions too).

## License

[MIT](LICENSE) — © 2026 sooogooo
