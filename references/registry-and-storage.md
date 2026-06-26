# Registry And Storage

Use the registry whenever more than one IP may exist.

All user IP data lives under a fixed directory at the **workspace root**: `ip-library/`. See `ip-object-protocol.md` for the object folder structure.

**Never store user data inside the skill bundle's `assets/examples/`.** That directory is read-only and will be overwritten on skill updates.

## Contents

- Directory Layout
- Path Lookup Protocol
- Registry YAML
- IP Selection
- Multi-IP Co-Presence
- Manifest
- Reference Images
- Isolation Principle

## Directory Layout

```text
<workspace-root>/ip-library/
├── ip-registry.yaml                    ← shared registry
│
├── xiao-tao/                           ← IP object
│   ├── ip-card.yaml
│   ├── reference-images/
│   │   ├── 01-portrait.png
│   │   ├── 02-action.png
│   │   ├── 03-composition.png
│   │   └── 04-style.png
│   └── outputs/
│       └── 2026-06-26-topic/
│           ├── 01-topic.png
│           ├── prompt.md
│           └── manifest.yaml
│
└── a-zhen/
    ├── ip-card.yaml
    ├── reference-images/
    └── outputs/
```

## Path Lookup Protocol

The skill finds user IP data using this fixed rule:

```
1. Look for <workspace-root>/ip-library/ip-registry.yaml
2. If found → read registry → resolve target IP → enter ip-library/<path>/
3. If not found → the user has no IPs yet → ask whether to create one
4. If the user provides an explicit external path → use that instead
```

The directory name `ip-library` is fixed. Do not rename or nest it.

## Registry YAML

```yaml
default_ip: xiao-tao
ips:
  - ip_id: xiao-tao
    ip_name: 小涛
    status: active
    version: v2
    path: xiao-tao/
    summary: 程序员，白底手绘工程草图风，靛蓝+橙+暖灰，线稿模式
  - ip_id: a-zhen
    ip_name: 阿珍
    status: active
    version: v1
    path: a-zhen/
    summary: 超级宝妈，温暖手绘风，珊瑚粉+鼠尾草绿+暖黄，上色模式
```

## IP Selection

Choose the IP in this order:

1. User explicitly names an `ip_id`.
2. User explicitly names an IP name.
3. Only one active IP exists.
4. Multiple active IPs exist: ask the user to choose.
5. User asks to create a new IP: create the object folder, card, reference images, then add to the registry.

Ask like this when ambiguous:

```text
你现在有多个 IP：
1. 小涛：程序员，工程草图风
2. 阿珍：超级宝妈，温暖手绘风

这次要用哪一个？
```

## Multi-IP Co-Presence

Default to one IP per image.

Only use multiple IPs when the user explicitly asks for co-presence. Read each IP's `ip-card.yaml` from their respective object folders. Keep identities separate.

Prompt rule:

```text
Character A: <IP A anchors + character_lock>
Character B: <IP B anchors + character_lock>
Do not merge their appearances. Keep both identities visually distinct.
```

## Manifest

Save a manifest for every output set inside the IP object folder:

```yaml
ip_id: xiao-tao
ip_version: v2
topic: 需求越说越大
mode: single-image
render_mode: line-art
expression_state: thinking
created_at: 2026-06-26
prompt_file: prompt.md
reference_images_used:
  - 01-portrait.png
  - 02-action.png
outputs:
  - file: 01-big-requirement.png
    status: selected
    qa:
      character_consistency: pass
      character_lock_match: pass
      text_accuracy: review
      style_match: pass
      color_system: pass
      expression_match: pass
notes: 中文标注需要人工复查
```

## Reference Images

Each IP object folder must contain 4 standard reference images in `reference-images/`. These are the **visual anchors** for character consistency.

See `ip-object-protocol.md` for the full reference image protocol and `photo-to-ip.md` for generation rules.

When generating a new image:
1. Read `01-portrait.png` description from the IP Card's `character_lock` field.
2. Inject `character_lock` into the prompt as an unchangeable block.
3. After generation, QA-compare the result against the reference images.

## Isolation Principle

| Layer | Location | Purpose | Mutability |
|-------|----------|---------|------------|
| Skill bundle | `personal-ip-illustrations/` | Engine + read-only examples | Only on skill install/update |
| IP library | `ip-library/` | User IP assets (cards, refs, outputs) | User-owned, per-workspace |
| Content files | `草稿/`, `封面图/`, etc. | User articles and media | User-owned |

Never write user data into the skill bundle. User-owned IP data is written only to the workspace `ip-library/` through the path lookup protocol above.
