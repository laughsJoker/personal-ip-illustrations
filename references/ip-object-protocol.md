# IP Object Protocol

Each personal IP is a **self-contained object folder**. All assets for one IP — card, reference images, and outputs — live inside a single directory. This makes each IP portable: copy one folder to migrate, delete one folder to remove.

## Contents

- Path Convention
- Object Folder Structure
- Object Fields
- Lifecycle
- Isolation Principle

## Path Convention

All user IP data lives under a fixed directory at the **workspace root**:

```text
<workspace-root>/ip-library/
```

This directory name is fixed as `ip-library`. Do not rename or nest it deeper. The skill looks for IP data here by default.

If the workspace does not yet have an `ip-library/` folder, create it when saving the first IP.

## Object Folder Structure

Each IP gets one folder named by its `ip_id`:

```text
ip-library/
├── ip-registry.yaml                    ← shared registry (points to each IP folder)
│
├── xiao-tao/                           ← IP object 1
│   ├── ip-card.yaml                    ← the character card (core attributes)
│   ├── reference-images/               ← 4 standard reference images (consistency anchors)
│   │   ├── 01-portrait.png             ← half-body portrait: locks face/hair/glasses/clothing
│   │   ├── 02-action.png               ← common action pose: locks body proportions/props
│   │   ├── 03-composition.png          ← typical composition: locks layout/whitespace/label placement
│   │   └── 04-style.png                ← annotation style: locks line quality/color application/text style
│   └── outputs/                        ← all generated images for this IP
│       └── <date-topic>/
│           ├── 01-*.png
│           ├── prompt.md
│           └── manifest.yaml
│
└── a-zhen/                             ← IP object 2
    ├── ip-card.yaml
    ├── reference-images/
    └── outputs/
```

## Object Fields

### ip-card.yaml (required)

The character card. See `ip-card-template.md` for the full schema. Must include `character_lock` for visual consistency.

### reference-images/ (required)

Four standard reference images generated at IP creation time. These are the **visual anchors** that lock the character's appearance across generations.

| File | Purpose | What It Locks |
|------|---------|---------------|
| `01-portrait.png` | Half-body standard portrait | Face shape, hair, glasses, clothing, overall temperament |
| `02-action.png` | Common action pose | Body proportions, signature prop usage, gesture style |
| `03-composition.png` | Typical composition sample | Layout, whitespace ratio, label placement, environment style |
| `04-style.png` | Annotation style sample | Line quality, color application, text handwriting style |

**Generation rules:**
- All 4 images are generated in the same session as IP creation.
- They use the IP's render mode and three-color palette.
- They are stored as PNG and never overwritten once confirmed.
- If the IP card is version-upgraded (e.g. appearance anchor change), regenerate all 4 reference images.

### outputs/ (created on demand)

Generated images organized by `<date-topic>` folders. Each folder contains:
- One or more PNG images
- `prompt.md`: the exact prompt used
- `manifest.yaml`: metadata (IP version, expression state, QA results)

## Lifecycle

### Create

1. User provides info or photo → generate IP Card + 4 reference images.
2. Create folder: `ip-library/<ip-id>/`
3. Write `ip-card.yaml`.
4. Save 4 reference images to `reference-images/`.
5. Add entry to `ip-library/ip-registry.yaml`.

### Use

1. Read `ip-library/ip-registry.yaml` → find target IP `path`.
2. Read `ip-library/<path>/ip-card.yaml` → get character card + `character_lock`.
3. Read `ip-library/<path>/reference-images/01-portrait.png` description → confirm visual identity.
4. Generate image with `character_lock` injected into prompt.
5. Save output to `ip-library/<path>/outputs/<date-topic>/`.

### Delete

1. Remove the IP folder: `ip-library/<ip-id>/`.
2. Remove the entry from `ip-registry.yaml`.
3. Historical outputs in other locations are not affected.

### Migrate

Copy the entire `ip-library/<ip-id>/` folder to the new workspace's `ip-library/`. Update the registry in the target workspace.

## Isolation Principle

- **Skill bundle** (`personal-ip-illustrations/`): engine + read-only examples. Never stores user data. Survives skill install/update without data loss.
- **IP library** (`ip-library/`): user data. Each IP is an independent object. Not affected by skill updates.
- **Content files** (`草稿/`, `封面图/`, etc.): the user's articles and media. IP outputs may be copied here for publishing, but the canonical store is `ip-library/`.
