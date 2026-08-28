# Generation specification

## Input contract

| Input | Required | Rule |
| --- | --- | --- |
| Pixel-art card reference | Yes | Use for visual language and layout only; never carry over its old task copy. |
| Date | Yes | Normalize to `YYYY-MM-DD` for records/files and `YYYYMMDD` on the card. |
| Core-task direction | No | If absent, choose a balanced mix of care, reset, and small environmental action. |
| Egg-task direction | No | If absent, choose a harmless, playful action with a natural comment prompt. |

If either required input is missing, ask only for that missing input. Do not start content generation from a guessed date or a text-only style description.

## Task rules

Produce exactly:

- 3 core tasks: ordinary life actions, each feasible in five minutes or less, warm rather than productivity-punishing, and small enough to do without buying anything or leaving home.
- 1 egg task: optional, harmless, playful, feasible in five minutes or less, and phrased so readers may naturally share how they did it or what happened.

Prefer concrete verbs and observable completion states. Examples of useful shapes are “擦干一个杯子”, “站到窗边深呼吸三次”, and “给一个水果拍证件照”; do not reuse these exact examples once they appear in history.

Reject or rewrite tasks that require travel, spending, medical claims, intense exercise, forced social contact, revealing private information, dangerous objects, cleaning with chemicals, or more than five minutes. Avoid vague instruction such as “好好爱自己” unless paired with a concrete action.

## De-duplication standard

Compare proposed tasks with every final task in `.earth-online-daily-tasks/records/*.md`.

- **Exact duplicate:** same action or only punctuation/word-order changed — reject.
- **Semantic duplicate:** same primary object and outcome despite different wording — reject. For example, “整理书桌” and “清出书桌一角” are the same family unless at least one changes the real action, object, and completion experience.
- **Permitted variation:** a distinct action with a different object and experience — acceptable. For example, “写一句给明天的便签” is distinct from “整理书桌”.

When a proposed task is too close, replace it before image generation. The record is the source of truth; do not depend on conversational memory.

## Text hierarchy and layout

Use the supplied reference to determine exact colors and canvas ratio. For the common vertical 1024 px-wide card, use this relative hierarchy:

| Element | Target treatment |
| --- | --- |
| Title / date | Largest title; compact pixel date in its own fixed date area. |
| Section labels | Medium-large, visually distinct from body but not oversized. |
| Task body | Roughly 40–52 px high, left-aligned, compact, and smaller than the title. Preserve natural one-line tasks where they fit. |
| Footer | Roughly 24–32 px high, centered or reference-aligned just above the lower decoration. |

Leave breathing room between groups rather than inflating the font. The card should read as a real task list at a glance.

The footer must start exactly with `地球online温馨提醒：`. Add a short, genuine reminder tied to a task theme. Example structure: `地球online温馨提醒：慢一点，也没关系`.

## Image prompt requirements

State all of the following in the image prompt:

1. The reference image is for visual style and layout, not old task content.
2. Every required string, written verbatim, with its intended section and alignment.
3. `YYYYMMDD` date text, title, both section labels, 3 core bullets, 1 egg task, and footer.
4. Pixel-art typography: crisp dark-teal Chinese pixel lettering; title largest; compact left-aligned body.
5. Invariants: preserve the reference's pixel-art mood and decorative safe zones; no browser chrome, logo, watermark, filler text, ruled lines, dotted guides, white writing panels, or generic UI cards.

For an existing local card target, inspect it first. For a fresh generation, pass the reference image into the generation request and make the result original rather than a pixel-for-pixel reproduction.

## Mandatory record format

After visual validation, create `.earth-online-daily-tasks/records/YYYY-MM-DD.md` with this structure. The Markdown document is the adopted-result ledger used for later de-duplication.

```markdown
---
date: YYYY-MM-DD
card: ../output/YYYY-MM-DD.png
reference: <original reference filename or path>
core_direction: <user supplied or generated>
egg_direction: <user supplied or generated>
status: accepted
---

# YYYY-MM-DD 地球 Online 每日任务

## 核心任务

- <final task 1>
- <final task 2>
- <final task 3>

## 彩蛋任务（选做）

- <final egg task>

## 温馨提醒

地球online温馨提醒：<final footer>

## 复用检查

- 已检查既有 records；无重复或语义近似任务。
- 采用的视觉规则：<brief note about reference typography/layout>。
```

For a revision of the same card, retain the original accepted task list. Save a versioned asset and append this section:

```markdown
## Revision YYYY-MM-DDTHH:MM:SS±HH:MM

- card: ../output/YYYY-MM-DD-v2.png
- changed: <for example, body text enlarged and footer updated>
```
