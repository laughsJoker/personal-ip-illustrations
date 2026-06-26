# Personal IP Illustrations

[English](README.md) | [简体中文](README.zh-CN.md) | [繁體中文](README.zh-TW.md)

A Codex skill for creating reusable personal IP character systems and generating consistent Chinese visual content: article illustrations, covers, knowledge cards, workflow visuals, and multi-character scenes.

This project is not a single image prompt collection. It is a small character asset system for Codex: each personal IP has a structured card, a stable `character_lock`, reference images, palette rules, expression anchors, and a workspace-level output library.

## Why This Exists

AI image generation is good at producing one nice picture, but weak at maintaining the same personal character across many topics. For writers, educators, creators, consultants, product people, and technical bloggers, visual consistency matters: the same character should keep the same face, temperament, outfit, color system, props, and annotation style across articles and social posts.

Personal IP Illustrations solves that by turning a person's identity and style into a reusable IP object.

Instead of asking:

```text
Draw me an illustration for this article.
```

you can ask:

```text
Use $personal-ip-illustrations with my existing IP to create 4 article illustrations for this draft.
```

The skill then resolves the IP Card, injects the full `character_lock`, chooses expression states, applies the palette system, plans the visual metaphor, and keeps outputs inside the IP's own library folder.

## What It Can Do

- Create structured personal IP Cards from a short brief.
- Create a cartoon IP from broad photo-derived features while avoiding biometric storage.
- Generate 4 standard reference images for a new IP.
- Produce consistent article illustrations.
- Plan shot lists for long articles.
- Generate social covers, hero images, and knowledge cards.
- Support single-IP and explicitly requested multi-IP scenes.
- Preserve character identity with `character_lock`.
- Use `line-art` and `colored` render modes.
- Apply per-IP three-color palettes with `palette_preset`.
- Save generated prompts, manifests, and outputs under `ip-library/`.

## Who It Is For

- Writers who want a recognizable visual persona.
- Developers and technical bloggers who need clean conceptual illustrations.
- Educators, parenting creators, and counselors who need warm recurring visual characters.
- Consultants and product people who explain frameworks or workflows.
- Creators who want a reusable IP asset rather than one-off illustrations.
- Codex users who want a practical skill for repeatable visual content workflows.

## Core Concepts

### IP Card

An IP Card is a structured YAML object that describes one reusable personal character. It includes identity, temperament, appearance anchors, clothing, props, actions, content domains, palette, render mode, expression anchors, forbidden styles, and examples.

### Character Lock

`character_lock` is the immutable block injected into image prompts to preserve identity. It describes the generated cartoon IP, not a real person's face. It should be pasted in full, including custom anchors such as glasses, beard style, hair accessories, posture, or signature clothing.

### Reference Images

Each IP should have 4 standard reference images:

```text
01-portrait.png      face, hair, clothing, temperament
02-action.png        body proportions, gesture, props
03-composition.png   layout, whitespace, label placement
04-style.png         line quality, color texture, annotation style
```

### Palette Preset

`palette_preset` selects an initial color direction, while the final `color_system` in the IP Card is the source of truth. Current presets include:

```text
indigo-engineering
coral-warm
custom
```

### Render Modes

`line-art` keeps character body and clothing interiors white/unfilled. The primary color appears only as sparse identity accents.

`colored` fills character body/clothing with the primary color while preserving hand-drawn texture.

## Install

Copy this folder into your Codex skills directory:

```text
~/.codex/skills/personal-ip-illustrations
```

On Windows:

```text
C:\Users\<you>\.codex\skills\personal-ip-illustrations
```

Then start a Codex conversation and invoke:

```text
Use $personal-ip-illustrations 为我创建个人 IP 角色卡，并生成4张标准参考图。
```

## Basic Usage

### Create a New IP

```text
Use $personal-ip-illustrations
我是一个写 AI 编程和产品复盘的技术创作者，想创建一个个人 IP。
```

The skill will create an IP Card, select a palette preset, define expression anchors, extract a `character_lock`, and generate the required reference images.

### Generate Article Illustrations

```text
Use $personal-ip-illustrations
用小涛这个 IP，为这篇文章规划 5 张正文配图。
```

### Generate a Cover

```text
Use $personal-ip-illustrations
用阿珍这个 IP，生成一张小红书封面，标题是「妈妈的五分钟」。
```

### Use Multiple IPs

```text
Use $personal-ip-illustrations
让小涛和阿珍一起出现在一张图里，表现「技术工具如何帮妈妈节省时间」。
```

Multi-IP images are only used when explicitly requested.

## User Data Layout

User-owned IP data should live in the workspace, not inside this skill:

```text
<workspace-root>/ip-library/
├── ip-registry.yaml
├── xiao-tao/
│   ├── ip-card.yaml
│   ├── reference-images/
│   └── outputs/
└── a-zhen/
    ├── ip-card.yaml
    ├── reference-images/
    └── outputs/
```

Generated output sets should include:

```text
outputs/<date-topic>/
├── 01-*.png
├── prompt.md
└── manifest.yaml
```

Do not save live user data inside this skill folder.

## Repository Layout

```text
personal-ip-illustrations/
├── SKILL.md
├── agents/
│   └── openai.yaml
├── references/
│   ├── color-system.md
│   ├── composition-patterns.md
│   ├── expression-system.md
│   ├── ip-card-template.md
│   ├── ip-object-protocol.md
│   ├── personality-mapping.md
│   ├── photo-to-ip.md
│   ├── prompt-template.md
│   ├── qa-checklist.md
│   ├── registry-and-storage.md
│   ├── style-system.md
│   └── validation-matrix.md
└── assets/
    └── examples/
```

## Privacy and Safety

The photo-to-IP workflow is designed to extract broad, drawable styling features only.

Do not store:

- Original photos
- Copied photo files
- EXIF metadata
- Source file names
- Source paths
- Biometric identifiers
- Precise facial measurements
- Uniquely identifying real-person details

`character_lock` describes the generated cartoon IP, not a real person's face.

If the source photo involves a minor, guardian consent is required before feature extraction.

## Design Principles

- Treat each IP as a reusable character system, not a one-off prompt.
- Keep character identity stable across topics.
- Make the character act inside the metaphor instead of standing as decoration.
- Prefer one clear idea per image.
- Keep Chinese labels short and sparse.
- Keep the background clean and white.
- Keep user data outside the skill bundle.

## Example IP Cards

Bundled examples live in:

```text
assets/examples/sample-cards/
```

They are read-only references for schema and style conventions. They are not live user data.

## Roadmap

- Add more palette presets.
- Add more style archetypes.
- Add richer validation examples.
- Add optional scripts for IP Card validation.
- Add sample output manifests.

## Contributing

Issues and pull requests are welcome. Please do not include real user photos, real private IP Cards, generated private output assets, or identifying personal data in contributions.

## License

MIT. See `LICENSE`.
