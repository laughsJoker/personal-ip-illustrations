# QA Checklist

Run this after generation or when editing.

## Must Pass

### Character Consistency
- The chosen IP is clear.
- The character keeps visual anchors.
- Clothing and signature props are present when relevant.
- Personality is visible through action.
- Character performs the core action, not decoration.

### Character Lock Match (against reference images)
- The generated character's face matches `reference-images/01-portrait.png` (face shape, hair, glasses, features).
- The generated character's body proportions and clothing match the reference.
- The `character_lock` block was injected into the prompt and not paraphrased.
- If the character looks visibly different from the reference portrait, flag as `character_lock_mismatch`.

### Three-Color Palette Check
- Character color uses primary fill (colored mode) or correct white space (line-art mode).
- Accent A is used for props/flow/arrows. Accent B is used for key points/results/warnings. The two are not mixed.
- Environment objects are lighter/muted compared to character (low-saturation same-hue or light gray).
- Background remains pure white — no gradients, no shadows, no textures.

### Expression Check
- Character expression matches the content state (thinking ≠ acting ≠ result-ok ≠ result-bad).
- Not every image shows the same "calm face".

### Composition and Text
- One image explains one core idea.
- Labels are short and few (2-8 chars each).
- No extra titles unless user requested a cover or knowledge card.
- Image has enough white space (≥35%).

### Forbidden Items
- No forbidden styles or behaviors appear.
- No PPT feeling, commercial stock feeling, or template feeling.
- If multiple IPs are used, identities are not merged.

## Failure Signals

### Character Problems
- Character looks like a generic person.
- Character changes appearance across images.
- Character only stands in the corner.
- Character face/hair/body does not match `reference-images/01-portrait.png`.

### Color Problems
- In colored mode, character is not filled with primary, or color changes every image.
- Accent A/B usage is confused — cannot distinguish roles.
- Environment colors are more vivid/eye-catching than character.
- Colors outside the three-color palette appear (e.g. sudden purple).
- Background has gradients, shadows, or textures.

### Expression Problems
- All images show the same "calm face" regardless of content.
- Expression contradicts content state (e.g. smiling happily while discussing a problem).

### Composition/Text Problems
- Too much text.
- Composition looks like a formal flowchart.
- Image looks like stock commercial art.
- Forbidden styles appear.
- Multiple IPs' appearances or personalities are auto-merged.

## Fixes

- Character drift: strengthen visual anchors and props in the prompt.
- **Character lock mismatch**: re-inject the full `character_lock` block verbatim. Ensure it is not paraphrased. Compare against `reference-images/01-portrait.png`. If mismatch persists after 2 regenerations, pause and inform the user — the reference images may need updating.
- Weak personality: make the action match the personality.
- **Color drift**: explicitly write the three hex values and their roles in the prompt. Reiterate primary=body, A=props, B=annotations.
- **Environment too loud**: change environment objects to light gray or very low saturation. Emphasize "environment lighter than character".
- **Expression monotony**: first determine content state (thinking/acting/result-ok/result-bad), then select corresponding expression to inject into prompt.
- Too complex: remove elements and keep one metaphor.
- PPT feeling: remove titles, boxes, grids, and many arrows.
- Bad Chinese text: reduce labels or use the no-text fallback.
- Missing personality: add signature props and fixed actions.
- Mixed IPs: reread the selected IP Card and explicitly forbid other IP traits.

## Text Accuracy

Mark text QA as:

- `pass`: all labels are correct.
- `review`: labels mostly work but need human check.
- `fail`: wrong text; regenerate or use no-text fallback.
