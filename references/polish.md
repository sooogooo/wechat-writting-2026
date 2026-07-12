# Polish Mode

## Objective

Deeply edit an existing WeChat article while preserving its central judgment, useful structure, personal voice, sharpness, strongest scenes, and intentional unfinished quality.

Do not rewrite it into a generic standardized essay unless the user explicitly asks for a complete reconception.

## Diagnose (check in order)

1. Is the opening generic or slow?
2. Does the core judgment appear too late?
3. Are ideas repeated?
4. Are explanations too complete / defensive / pre-empting every objection?
5. Do AI transitions or stock phrases appear?
6. Does the structure lean on "首先、其次、最后" mechanically?
7. Is every paragraph trying to become a gold quote?
8. Is parallelism overused?
9. Are paragraphs fragmented into one-sentence paragraphs?
10. Do long sentences carry too many causal / concessive clauses?
11. Are medical or operational mechanisms unsupported or oversimplified?
12. Does the ending repeat, moralize, comfort, or force elevation?

## Preserve (do not flatten)

- central judgment
- strongest scene
- distinctive metaphor
- valuable sentence
- industry experience
- critical edge
- restraint
- personal rhythm
- intentional negative space

Hard rule: do not turn sharp judgments into polite advice. Do not flatten the text into official or academic prose.

## Repair

- Delete empty industry background and over-explanation.
- Move the central judgment earlier if it lands after paragraph 5.
- Merge repeated claims.
- Replace AI transitions with natural logic ("值得注意的是" → sentence-level rewrite).
- Restore natural paragraph rhythm (target 2–5 sentences each).
- Break overloaded long sentences, but retain variation.
- Strengthen mechanisms — do NOT invent data or cases.
- Replace generic absolutes ("零风险 / 永久 / 适合所有人") with "取决于 / 在这种情况下 / 因人而异".
- Replace generic subheadings with judgment-led ones.
- Cut the ending earlier when it has already landed.

## Default output — two sections

### 精修诊断
300–500 Chinese characters, concrete and non-generic. Cover:

- what is worth preserving
- main structural problem
- main language problem
- passages to cut / compress / move
- missing mechanism
- editing strategy in 1–2 sentences

### 精修后的完整文章
Publication-ready article. No annotations, no tracked changes, no inline explanations.

## Output template

```
### 精修诊断
……（300–500 字）

### 精修后的完整文章
……（完整可发布正文）
```

If the user only asks for the final rewrite ("直接给我改好的"), output the article directly and skip the diagnosis section.
