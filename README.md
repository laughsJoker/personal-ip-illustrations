# Personal IP Illustrations

A Codex skill for creating reusable personal IP character cards and generating consistent Chinese illustrations, covers, knowledge cards, and visual content.

## What It Does

- Creates structured personal IP Cards from a short brief or broad photo-derived features.
- Maintains character consistency with `character_lock`.
- Supports `line-art` and `colored` render modes.
- Uses stable `palette_preset` values and per-IP three-color palettes.
- Plans article illustration shot lists, covers, knowledge cards, and multi-IP scenes.
- Keeps user-owned IP data outside the skill bundle.

## Install

Copy this folder into your Codex skills directory:

```text
~/.codex/skills/personal-ip-illustrations
```

On Windows:

```text
C:\Users\<you>\.codex\skills\personal-ip-illustrations
```

## Usage

```text
Use $personal-ip-illustrations 为我创建个人 IP 角色卡，并生成4张标准参考图。
```

After an IP exists, generated user assets belong in the workspace:

```text
<workspace-root>/ip-library/<ip-id>/
```

Do not save live user data inside this skill folder.

## Privacy

The photo-to-IP workflow is designed to extract broad, drawable styling features only. Do not store original photos, copied photo files, EXIF metadata, source file names, source paths, biometric identifiers, precise facial measurements, or uniquely identifying real-person details.

`character_lock` describes the generated cartoon IP, not a real person's face.

## Repository Layout

```text
personal-ip-illustrations/
├── SKILL.md
├── agents/
│   └── openai.yaml
├── references/
│   └── *.md
└── assets/
    └── examples/
```

## License

MIT. See `LICENSE`.
