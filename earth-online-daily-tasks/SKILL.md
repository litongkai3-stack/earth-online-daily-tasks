---
name: earth-online-daily-tasks
description: "Generate a pixel-art Earth Online daily task card from a reference card and date, with an HTML fallback and a task ledger that prevents repeats."
metadata:
  short-description: "Generate pixel-art daily cards with task history"
---

# Earth Online Daily Tasks

Create one publish-ready Chinese pixel-art daily task card. Use this skill when the user provides a pixel-art task-card reference and wants a dated card with three core tasks, one optional egg task, and a warm footer reminder.

The reference controls the visual language; the skill controls the task structure, text hierarchy, validation, and history. Do not reuse the old card's task copy as new content.

## Required input

Collect these before generating:

- **Reference image** — a pixel-art task-card image. It may be a blank template or a completed card; treat existing text as style/layout reference only.
- **Date** — required. Accept `YYYY-MM-DD`, `YYYYMMDD`, or an unambiguous Chinese date, then render it as `YYYYMMDD` on the card and use `YYYY-MM-DD` in filenames and records.

The user may optionally provide:

- a direction for core tasks (for example, “下班后放松” or “整理房间”);
- a direction for the egg task;
- a preferred final filename or workspace.

Do not ask for directions when they are absent. Generate suitable directions instead.

## Working directory and history

Use the caller's current project as the **working project**. Store generated artifacts outside the installed skill folder:

```text
<working-project>/.earth-online-daily-tasks/
├── output/YYYY-MM-DD.png or YYYY-MM-DD.html
└── records/YYYY-MM-DD.md
```

Before proposing tasks, read every existing `records/*.md` in that directory. Build a used-task list from their final core and egg tasks. Do not repeat an earlier task, including a close paraphrase with the same real-world action (for example, “倒一杯温水” and “洗杯子再装温水” are duplicates). A revision to the *same date* may retain the same tasks; it is a layout revision, not a new task set.

If the date already has a record, read it before working. Preserve its task set unless the user explicitly asks to replace the tasks. When the visual changes, append a revision entry to that date's record and save a versioned image such as `YYYY-MM-DD-v2.png`.

Read [the generation specification](references/generation-spec.md) before composing content or an image prompt. Read [the quality checklist](references/quality-checklist.md) after every image-generation pass.

## Workflow

1. Inspect the reference image. Identify its canvas ratio, title/date placement, pixel typography, task spacing, footer placement, and decorative safe zones.
2. Load task history and draft exactly three core tasks plus one egg task. Apply the content and no-repeat rules in the generation specification.
3. Draft a single `地球online温馨提醒：…` footer. It should feel warm and relate to at least one of today's tasks; it is not a generic slogan or an unrelated promotion.
4. Show the proposed text in the response when a user decision or wording choice is needed; otherwise proceed directly to the image. Keep the date formatted as `YYYYMMDD`.
5. Select a render path based on *available tools*, not the agent's name or assumed model capability:
   - **Image path:** when native image generation is available, use the platform image-generation workflow. If editing a local target image, inspect it first with the image-viewing tool. Put every intended text string in the prompt verbatim, state its placement, and preserve the reference's overall visual hierarchy.
   - **HTML fallback:** when native image generation is unavailable, read [the HTML fallback instructions](references/html-fallback.md). Copy `assets/fallback-card.html` into the output directory, fill its data block with the approved card copy, and return the standalone HTML file. It is an intentional deliverable, not an error state.
6. Inspect the resulting PNG or HTML card. Verify all Chinese characters, punctuation, date digits, task count, spacing, and footer against the checklist. If the copy is inaccurate or unreadable, make one targeted text/layout edit rather than rebuilding the whole card blindly.
7. Once the card is accepted as the final result, save the PNG or HTML card and create or update its Markdown record as defined in the generation specification. The record is mandatory; do not claim completion until it exists.
8. Return the card and link to both the final artifact and the record. Do not commit, publish, or push to GitHub unless the user separately asks.

## Non-negotiable visual lessons

- Use the reference's *relative* typography: title largest; section labels slightly larger than task body; task body readable but never poster-sized.
- Keep task copy left-aligned in a compact list with natural line breaks. Use the available space, but do not stretch every task into giant two-line headlines.
- Integrate text into the card background. Do not introduce ruled lines, dotted writing guides, oversized white panels, or generic form boxes unless the reference itself deliberately uses them.
- Reserve decorations for borders and corners. They must not collide with the date, task copy, or footer.
- A complete card always has: title, date, `核心任务：`, three core bullets, `彩蛋任务（选做）：`, one egg task, and a `地球online温馨提醒：…` footer.

## Cross-agent compatibility

Keep this skill normally discoverable (`allow_implicit_invocation: true`) so any agent that has the skill installed may use it. Do not require an agent-specific plugin, model name, API key, or cloud service to complete the request. Native image generation is preferred where available; the bundled HTML fallback is required when it is not.
