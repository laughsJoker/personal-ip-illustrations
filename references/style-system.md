# Style System

Choose a visual style that matches the IP Card. Do not let style override identity.

## Common Styles

### Whiteboard Engineering Sketch

Best for programmers, product people, consultants, researchers.

- pure white background
- black hand-drawn line art
- lots of whitespace
- three-color palette annotations (primary/accent-a/accent-b) — NOT old red/orange/blue
- tools, cards, boxes, logs, wires, pipes
- avoid cyber hacker UI and dense code screenshots

### Gentle Handdrawn Life Notes

Best for parenting, education, mental health, life writing.

- soft round lines
- warm but restrained colors (coral pink / sage green / warm yellow palette)
- colored render mode preferred (character body filled with primary)
- domestic props, cups, blankets, lamps, doors, bubbles
- actions like holding, repairing, accompanying, sorting
- allow real-life messiness (scattered toys, messy hair) — not perfect stock scenes
- avoid childish posters and stock-style family scenes

### Sharp Commentary Sketch

Best for workplace critique, product commentary, anti-fluff content.

- stronger contrast
- accent B color used for critique annotations (the "pay attention" color)
- exaggerated but clean metaphors
- props like warning tags, scissors, magnifier, masks
- avoid personal attacks, cruelty, or noisy meme styling

### Craft Process Sketch

Best for designers, indie makers, photographers, craft creators.

- visible process and tools
- desk, draft, prototype, half-finished object
- low-saturation accents
- allow some detail, but keep the image breathable

## Color System (Three-Color Palette)

Each IP uses a fixed three-color palette. See `references/color-system.md` for full rules.

### Default Palette Presets

| Preset | Primary | Accent A | Accent B |
|--------|---------|----------|----------|
| `indigo-engineering` | 靛蓝 `#3B5B7E` | 橙色 `#E89143` | 暖灰 `#9B9B9B` |
| `coral-warm` | 珊瑚粉 `#E8826B` | 鼠尾草绿 `#8FB386` | 暖黄 `#F2C94C` |

### Color Roles

- **Primary** (~60% of colored areas): Identity color. Fill character body/clothing only in `colored` mode; use sparse accents only in `line-art` mode.
- **Accent A** (~25%): Props, flow arrows, tools, positive actions.
- **Accent B** (~15%): Key warnings, results, highlights, important labels.
- **Environment**: Low-saturation same-hue as primary, or light gray. Always muted compared to character.
- **Black**: Outline and structure lines (not part of three-color palette).
- **White**: Background, always pure white (not part of three-color palette).

### Render Modes

- `line-art`: Character body/clothing left white/unfilled. Primary appears only as sparse identity accents; Accent A/B appear on props and annotations.
- `colored`: Character body/clothing filled with primary color. Keep hand-drawn texture, NOT flat vector.

Users may override `render_mode` in IP Card.

## Text Rules

Prefer 2-4 labels. Each label should be 2-6 Chinese characters when possible.

If generated text is wrong:

1. reduce label count
2. regenerate with exact labels
3. generate no-text image
4. add text later outside the image model
