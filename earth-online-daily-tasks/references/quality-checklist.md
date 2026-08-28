# Quality checklist and lessons from the first production run

Use this checklist after each image-generation pass. If a required item fails, make a narrowly scoped correction and inspect again.

## Content checks

- [ ] The date is present, correct, and rendered as `YYYYMMDD`.
- [ ] There are exactly 3 core tasks and 1 egg task.
- [ ] Each task is a concrete, safe action achievable in five minutes or less.
- [ ] Core and egg directions were honored when supplied.
- [ ] The footer starts with `地球online温馨提醒：` and relates to the day's task theme.
- [ ] The task ledger was checked; no exact or semantic task repeat is introduced.

## Text checks

- [ ] Every Chinese character and punctuation mark matches the approved copy.
- [ ] No characters are clipped, substituted, duplicated, or turned into unreadable pseudo-text.
- [ ] Body text is visibly larger than a caption but smaller than section labels/title.
- [ ] Bullets are aligned; multi-line content wraps deliberately rather than accidentally.
- [ ] The date has enough contrast and does not crowd its frame.

## Composition checks

- [ ] Text is integrated into the background, not trapped inside unrelated white panels or form boxes.
- [ ] There are no dotted or ruled writing guides unless the supplied reference explicitly calls for them.
- [ ] Core and egg groups use space efficiently without giant headline typography or excessive empty gaps.
- [ ] Border decorations do not overlap text; the footer remains legible above bottom artwork.
- [ ] The result contains no browser chrome, watermark, unrelated logo, or copied task text from the reference.
- [ ] For an HTML fallback, the file opens as a standalone card and contains no unresolved `[PLACEHOLDER]` or sample task content.

## Known pitfalls and corrections

| Pitfall | Why it fails | Correction |
| --- | --- | --- |
| Body type is too small | The card feels unfinished and leaves a void. | Enlarge only the task body by a modest step; keep its natural one-line list rhythm. |
| Body type is too large | It becomes a poster and destroys the task-list hierarchy. | Return body text to medium size and use group spacing rather than line breaks to fill space. |
| Dotted lines / white panels appear | They turn the card into a generic worksheet and depart from the reference's fused scene. | Remove guides and panels; extend the card background behind the text. |
| Footer is decorative but unrelated | The world-building line loses its purpose. | Make the reminder acknowledge a task's emotional or practical theme. |
| Image model garbles Chinese text | The output cannot be published even when the scene is attractive. | Perform a targeted text-localization edit using exact copy; do not accept near-matches. |
| Native image generation is unavailable | The request should not fail merely because a specific agent lacks a media tool. | Produce the standalone HTML fallback with the final task data, then record its `.html` output path. |
| Same task returns on a later day | The series starts to feel templated. | Read the Markdown ledger first and replace the proposed task with a distinct action family. |

## Acceptance rule

Do not save the daily record until every required content and text check passes. Once saved, the record is the final source for the next run's de-duplication pass.
