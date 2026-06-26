# Color System

Each IP character owns a fixed **three-color palette** used for identity color, environment rendering, props, and annotation distinction.

The palette is not three random nice colors. It must satisfy:

- **Primary**: Character identity color — fills body/clothing only in `colored` mode; appears as sparse identity accents in `line-art` mode.
- **Accent A**: Props, flow elements, path arrows — expresses "something is happening".
- **Accent B**: Key annotations, problems, results, warnings — expresses "pay attention here".

Base layer is always **pure white background + black line art**. Black exists as outline and structure lines; white keeps the image clean. Neither participates in the three-color palette.

## Contents

- Palette Presets
- Custom Palette Rules
- Render Modes
- Coloring Detail Rules

## Palette Presets

When the user does not specify colors, assign a `palette_preset` based on personality, domain, and user preference. Gender may be used as a weak hint only when the user explicitly provides it. Once `color_system` is written into the IP Card, it becomes the source of truth.

### `indigo-engineering`: Indigo + Orange + Warm Gray

| Role | Name | Hex | Usage | Ratio |
|------|------|-----|-------|-------|
| Primary | 靛蓝 Indigo | `#3B5B7E` | Identity color; clothing/body fill only in `colored` mode; sparse clothing/label accents in `line-art` mode | ~60% of colored areas |
| Accent A | 橙色 Orange | `#E89143` | Props, flow arrows, tools, positive actions | ~25% |
| Accent B | 暖灰 Warm Gray | `#9B9B9B` | Secondary annotations, minor objects, background elements | ~15% |

**Temperament**: Calm engineering warmth. Indigo is friendlier than pure black, orange brightens without glaring, warm gray grounds the image. Suited for programmers, engineers, product managers, analysts, and restrained professional IPs.

### `coral-warm`: Coral Pink + Sage Green + Warm Yellow

| Role | Name | Hex | Usage | Ratio |
|------|------|-----|-------|-------|
| Primary | 珊瑚粉 Coral Pink | `#E8826B` | Identity color; clothing/body fill only in `colored` mode; sparse clothing/label accents in `line-art` mode | ~60% of colored areas |
| Accent A | 鼠尾草绿 Sage Green | `#8FB386` | Props, flow elements, plants, companion objects | ~25% |
| Accent B | 暖黄 Warm Yellow | `#F2C94C` | Key annotations, results, highlights, hope | ~15% |

**Temperament**: Warm healing with vitality but not overly sweet. Coral pink is more mature than traditional pink, sage green balances sweetness, warm yellow lifts mood. Suited for educators, counselors, parenting bloggers, lifestyle creators, and warm social IPs.

## Custom Palette Rules

Users may override defaults. Custom palettes must follow:

1. **Primary must be identifiable**: not too light (near white) or too dark (near black), saturation 40%-70%.
2. **Three colors must contrast**: at least visible lightness or hue difference between primary and accents.
3. **Avoid clashing combos**: red+green or blue+orange as strong colors need caution; recommend one strong + two muted.
4. **Record in IP Card**: write confirmed palette into `color_system` field.

## Render Modes

Controlled by IP Card `render_mode` field.

### Line-Art Mode (`line-art`)

```
Character = black hand-drawn outline; body and clothing interiors stay white/unfilled
Primary color = sparse identity accents only, such as a small clothing edge, tiny badge, label, or one signature prop
Accent colors = sparse Chinese annotations + arrows + key markers
Style reference: ian-xiaohei-illustrations pure line-art style
```

Best for: rational restrained personality, engineering sketch style, minimalist technical content.

**Default for male IPs.**

### Colored Mode (`colored`)

```
Character body/clothing filled with primary color
Hair in dark color (black / dark brown)
Skin in very light tone or left white
Props in Accent A
Key results in Accent B
Environment in low-saturation same-hue as primary
```

Best for: gentle healing type, lively social type, craft maker type, and all female IPs by default.

**Default for female IPs.**

Users may override in IP Card.

## Coloring Detail Rules

### Mode-Aware Body Color

```yaml
line_art_mode:
  body_clothing: pure_white       # keep interiors unfilled; black outline defines form
  primary_use: sparse_identity_accent  # tiny clothing edge, small badge, key label, or one prop only
  hair: black / dark_brown
  skin: pure_white or very_light_flesh

colored_mode:
  body_clothing: primary          # clothing and body, keep hand-drawn texture, NOT flat fill
  hair: black / dark_brown
  skin: very_light_flesh or pure_white
  shoes: dark_gray or darker_primary
```

**Key requirement**: In `line-art` mode, never fill the main character body or clothing with primary color. In `colored` mode, coloring must retain hand-drawn texture. Do NOT turn into flat vector fill. Allow pen stroke marks, slight unevenness, minor edge bleed — these "imperfections" are the soul of hand-drawn style.

### Props and Objects

```yaml
props_color:
  main_props: accent_a            # common props (laptop bag, cup, toolbox)
  secondary_props: warm_gray      # minor objects (table, floor lines)
  highlight_elements: accent_b    # special elements to emphasize
```

### Environment Color Rules

Environment must not steal visual focus from the character:

```yaml
environment_rules:
  background: pure_white
  floor_surface: light_gray or primary 20% opacity
  ambient_objects: primary 30% opacity
  atmosphere: none               # no light effects, no gradient ambiance
```

**Core principle**: Environment colors are always low-saturation degraded versions of the character's colors. If the character wears indigo, the chair in the scene uses light blue-gray outlines. If the character wears coral pink, the environment uses light warm gray.

| Layer | Color | Canvas Ratio |
|-------|-------|-------------|
| Character | `colored`: Primary + black outline; `line-art`: white interior + black outline + sparse primary accent | 30%-40% |
| Props (accent colors) | Accent A/B | 10%-15% |
| Environment objects | Primary low-sat / light gray | 10%-20% |
| Chinese annotations | Accent A/B handwritten | minimal |
| **White space** | **Pure white** | **≥35%** |
