---
name: personal-ip-illustrations
description: 生成可定制个人 IP 视觉分身和中文视觉内容。用于用户要求根据姓名、职业、性格、外形、内容领域、照片或角色卡创建个人 IP Card / 视觉分身，或基于 IP Card 生成稳定一致的文章配图、正文插图、知识卡片、社媒封面、shot list、改图和多 IP 选择任务；支持白底手绘、漫画、拼贴、工程草图、温柔治愈、犀利吐槽等不同人格风格，三元配色系统、表情锚点联动、照片转 IP 流程，并管理多个个人 IP。
---

# 个人 IP 视觉分身

## Core Purpose

Generate stable Chinese visual content from a personal IP Card. Treat each visual avatar as a reusable character system, not a one-off prompt. Keep appearance, personality, props, actions, annotation tone, three-color palette, expression anchors, and forbidden styles consistent across topics.

## Quick Reference Cheat Sheet

Use this table to avoid reading every reference file for routine tasks:

| Task | Key Rule | Reference |
|------|----------|-----------|
| Create IP Card | Ask ≤5 questions, fill all fields, pick `palette_preset`, extract `character_lock` | `ip-card-template.md` |
| Pick colors | `indigo-engineering`: 靛蓝#3B5B7E + 橙#E89143 + 暖灰#9B9B9B; `coral-warm`: 珊瑚粉#E8826B + 鼠尾草绿#8FB386 + 暖黄#F2C94C | `color-system.md` |
| Pick render mode | `line-art`: body/clothing white, sparse primary accents; `colored`: body/clothing filled with primary | `color-system.md` |
| Pick expression | thinking(卡住) / acting(在做) / result-ok(搞定) / result-bad(出错了) / default(无明确阶段) | `expression-system.md` |
| Photo → IP | Extract features → cartoonize → apply palette → extract `character_lock` → confirm → generate 4 reference images → save to `ip-library/` | `photo-to-ip.md` |
| Pick composition | 单观点隐喻 / 工作流 / 前后对比 / 角色状态 / 小漫画分镜 / 知识卡片 / 封面主视觉 | `composition-patterns.md` |
| Write prompt | IP info → **character_lock (immutable)** → expression → color system → render mode → theme → composition → labels → constraints | `prompt-template.md` |
| Multi-IP | Default one IP per image. Multi-IP only when explicitly asked. Never auto-merge. | `registry-and-storage.md` |
| Labels | 2-4 labels, 2-6 chars each. Accent A for flow, Accent B for key points. If wrong → reduce or no-text. | `style-system.md` |
| QA after gen | Check: character_lock match ✓, three-color palette ✓, expression matches state ✓, one idea per image ✓, ≥35% white ✓ | `qa-checklist.md` |
| IP storage | Each IP = one object folder under `ip-library/<ip-id>/`. Card + reference images + outputs self-contained. | `ip-object-protocol.md` |

## User-Facing Storage Rule

When users ask "我的图片怎么放" or "怎么使用", explain in tables:

| User Need | Where It Goes | Rule |
|-----------|---------------|------|
| Source photo for creating a visual avatar | User uploads it in chat or provides a local path | Use only for current-session feature extraction. Do not persist the original photo. |
| Live IP Card | `<workspace-root>/ip-library/<ip-id>/ip-card.yaml` | Contains identity, visual anchors, palette, expression anchors, and `character_lock`. |
| Standard reference images | `<workspace-root>/ip-library/<ip-id>/reference-images/` | Four files: `01-portrait.png`, `02-action.png`, `03-composition.png`, `04-style.png`. |
| Generated outputs | `<workspace-root>/ip-library/<ip-id>/outputs/<date-topic>/` | Save PNGs, `prompt.md`, and `manifest.yaml`. |
| Public examples only | `assets/examples/` inside this skill | Never store real user data here. |

## Read References As Needed

- `references/ip-card-template.md`: read when creating, completing, or validating an IP Card.
- `references/ip-object-protocol.md`: read when understanding IP object folder structure, creating or migrating an IP.
- `references/color-system.md`: read when choosing or applying the three-color palette, render mode, or environment colors.
- `references/expression-system.md`: read when selecting character expressions based on content state.
- `references/photo-to-ip.md`: read when a user provides a photo and wants to create an IP from it.
- `references/registry-and-storage.md`: read when multiple IPs exist, when choosing an IP, or when saving outputs.
- `references/personality-mapping.md`: read when translating personality into visual language.
- `references/style-system.md`: read when choosing or adapting a visual style.
- `references/composition-patterns.md`: read when making a shot list or selecting composition.
- `references/prompt-template.md`: read before generating images or writing final image prompts.
- `references/qa-checklist.md`: read after generation, for edits, or when the user says the image is off-brand.
- `references/validation-matrix.md`: read when testing or forward-validating the skill.
- `assets/examples/sample-cards/`: read-only sample IP Cards for reference. Never write user data here.

## Workflow

### 1. Resolve The IP

All user IP data lives under `<workspace-root>/ip-library/`. Each IP is a self-contained object folder. See `references/ip-object-protocol.md`.

**Lookup order:**
1. Look for `<workspace-root>/ip-library/ip-registry.yaml`.
2. If found → read registry → resolve target IP by `ip_id` or name → enter `ip-library/<path>/`.
3. If not found → the user has no IPs yet → ask whether to create one.

If the user provides an IP Card, use it exactly.

If the user only provides a name, occupation, personality, or vague direction, create an initial IP Card first. Ask at most five questions only when required details cannot be reasonably inferred.

If the user provides a photo, follow `references/photo-to-ip.md` to extract generalizable features, generate a cartoon IP Card with `character_lock`, and produce 4 standard reference images. Do not store the original photo.

If multiple IP Cards exist, read the registry. Use the explicitly requested IP by `ip_id` or IP name. If the user does not specify an IP and multiple active IPs exist, ask which IP to use. Do not merge multiple IPs unless the user explicitly asks for multi-IP co-presence.

**Never treat `assets/examples/` as the user's live IP library.** That directory is read-only and bundled with the skill.

### 2. Understand The Content

Read the article, topic, screenshot, link, or short idea. Extract the core viewpoint, emotional state, workflow, conflict, before/after shift, or metaphor worth visualizing.

Determine the content state for expression selection: thinking / acting / result-ok / result-bad / default. See `references/expression-system.md`.

Do not illustrate every paragraph. Prefer cognitive anchors: core judgment, turning point, input/output loop, common pitfall, messy-to-clear transformation, emotional support moment, or one memorable metaphor.

### 3. Plan Before Generating When Useful

If the user asks for planning, strategy, "where to add images", or a long article workflow, output a shot list first.

Each shot should include:

- placement
- theme
- core idea
- composition type
- IP character action
- expression state (thinking/acting/result-ok/result-bad/default)
- suggested elements
- Chinese labels
- risks

Default to 4-8 shots. Use 1-3 for short content. Avoid exceeding 9 unless the user explicitly asks.

### 4. Generate Images

If the user explicitly asks to generate, create each image separately. Do not combine multiple shots into one collage.

Each image must:

- use one resolved IP Card
- inject the `character_lock` block into the prompt as an immutable section (do not paraphrase)
- keep appearance anchors visible and matching the reference images
- make the IP character perform the core conceptual action
- apply the three-color palette correctly (line-art: primary as sparse identity accents only; colored: primary for body/clothing; accent A for props; accent B for highlights)
- use the correct render mode (line-art or colored)
- match character expression to the content state
- express one core idea
- use short Chinese labels
- keep environment colors muted compared to character
- avoid forbidden styles and behaviors

For generated Chinese text, prefer 2-4 labels. If text accuracy fails, reduce labels or generate a no-text version and add text later.

### 5. Save And Report

All outputs are saved inside the IP's own object folder:

```text
<workspace-root>/ip-library/<ip-id>/outputs/<date-topic>/
```

Example: `ip-library/xiao-tao/outputs/2026-06-26-big-requirement/`

Keep the image, `prompt.md`, and `manifest.yaml` together. Do not overwrite existing outputs unless the user explicitly requests replacement.

**Never save user data inside the skill's `assets/examples/` directory.** That directory is read-only and will be overwritten on skill updates.

IP object folder structure (each IP is self-contained):

```text
<workspace-root>/ip-library/
├── ip-registry.yaml              ← shared registry
├── xiao-tao/                     ← IP object
│   ├── ip-card.yaml              ← character card (with character_lock)
│   ├── reference-images/         ← 4 standard reference images
│   │   ├── 01-portrait.png
│   │   ├── 02-action.png
│   │   ├── 03-composition.png
│   │   └── 04-style.png
│   └── outputs/                  ← generated images
│       └── <date-topic>/
│           ├── 01-*.png
│           ├── prompt.md
│           └── manifest.yaml
└── a-zhen/
    └── ...
```

Report:

- which IP was used
- what was generated
- output path
- expression state used
- `character_lock` match result (against reference images)
- any QA issues, especially text accuracy, color drift, or character drift

## Guardrails

- Do not invent a new IP when the user clearly asked to use an existing one.
- Do not mix two IPs unless explicitly requested.
- Do not imitate existing commercial characters, brand mascots, or unauthorized real-person likenesses.
- Do not store original photos from photo-to-IP flow. Only keep generalizable anchors.
- Do not store sensitive real-child identity details in public IP Cards.
- Do not create dense PPT diagrams unless the user asks for a structured slide/card format.
- Do not let the IP character stand as decoration; it must act inside the metaphor.
- Do not use colors outside the three-color palette unless explicitly justified.
- Do not use the same expression for every image — match expression to content state.
- Do not generate more than 8-9 images in one batch without user confirmation.
- Do not paraphrase or simplify the `character_lock` block — inject it verbatim into every prompt.
- Do not save user IP data inside the skill bundle (`assets/examples/`). User data goes to `ip-library/`.
- Do not skip reference image generation when creating a new IP — all 4 are mandatory.
