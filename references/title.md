# Title Mode

## Objective

Generate WeChat Official Account titles with clear judgment, propagation tension, industry credibility, and restraint.

Each title should make the subject identifiable while introducing contradiction, cost, reversal, structural insight, or counterintuitive judgment.

## Suitable structures

Use these as inspiration, not fixed templates:

- 你以为……其实……
- A 不等于 B
- 真正的问题,不是……
- ……正在消耗什么
- 真正值钱的不是……而是……
- 为什么……不是个体问题,而是系统问题
- 花了最多的钱,为什么……
- ……结束之后

## Tone examples

- 你以为医美是在买项目,其实是在买判断
- 越贵的医美项目,越不该急着做
- 好医生 + 好方案,不等于好结果
- 医美机构真正缺的,不是新项目
- 项目矩阵的幻觉,正在消耗机构的现金流
- 医生 IP 真正要出售的,不是流量,而是判断

## Hard requirements

- Usually 16–28 Chinese characters (clarity > strict length)
- Do not make every title a question
- Do not repeat one sentence pattern
- Avoid excessive punctuation
- Do not distort the article to manufacture drama
- Avoid: advertising tone / 课程招生 tone / textbook-chapter tone / short-video 口播 tone
- Forbid: "震惊" / "疯传" / "99% 的人不知道" / "不看后悔" / "内幕" / "彻底颠覆认知"

A strong title contains at least one of:

- contradiction
- reversal
- cost
- hidden mechanism
- structural judgment
- counterintuitive conclusion
- tension between appearance and reality

## Default output

Generate 10 titles, in this exact mix:

| Slot | Count | Purpose                                |
| ---- | ----- | -------------------------------------- |
| A    | 3     | high propagation (传播型)              |
| B    | 3     | industry judgment (行业判断型)          |
| C    | 2     | restrained premium (克制高阶型)         |
| D    | 2     | counterintuitive (反直觉型)             |

Then pick the strongest 3 and briefly annotate:

- suitable audience (one line)
- propagation advantage (one line)
- possible risk (one line)

If the user asks for fewer titles, output the requested count and skip the 3-strongest annotation unless they ask for it.

## Output template

```
【10 个备选标题】

▎传播型
1. …
2. …
3. …

▎行业判断型
4. …
5. …
6. …

▎克制高阶型
7. …
8. …

▎反直觉型
9. …
10. …

【最强 3 个 · 推荐理由】
① ……
- 适合人群：
- 传播优势：
- 潜在风险：

② ……
- 适合人群：
- 传播优势：
- 潜在风险：

③ ……
- 适合人群：
- 传播优势：
- 潜在风险：
```
