# Prompt Template

Use this template for image generation. Replace fields from the resolved IP Card and current task.

## Contents

- Character Lock Insertion Rule
- Single Image
- Photo → IP
- Multi-IP Image
- No-Text Fallback
- Cover / Hero Image
- Knowledge Card
- Prompt Record

## Character Lock Insertion Rule

Always inject the complete `character_lock` YAML block from the resolved IP Card. Do not list only the standard fields. Preserve every extra identity anchor, such as glasses, beard, mole, hair accessory, posture, signature clothing details, or any other custom field.

## Single Image (With Color System + Expression)

```text
Generate one standalone 16:9 horizontal Chinese article illustration.

Personal IP:
{IP 名字}, {职业/身份}. Palette preset: {palette_preset}. Gender metadata if relevant: {gender}.
Appearance anchors: {外形锚点}. Clothing anchors: {服装锚点}.
Personality: {核心性格 + 辅助性格}. Signature props: {常用道具}.
The character must perform the core conceptual action, not decorate the scene.

--- CHARACTER LOCK (immutable — paste the full YAML block verbatim) ---
{character_lock 完整 YAML 内容，包含所有额外身份锚点，例如 glasses、beard、mole、hair_accessory、posture、signature_clothing 等。不要省略任何字段。}
--- END CHARACTER LOCK ---
The character must match every field in the full CHARACTER LOCK block. Only the action, expression, and scene may change. Never change the face, hair, body proportions, clothing defaults, or extra anchors such as glasses and signature features.

Character expression:
{根据内容状态选择表情锚点：default/thinking/acting/result-ok/result-bad}
Expression detail: {具体表情描述}

Color system (三元配色):
- Primary color ({主色名} {色值}): Identity color. In `colored` mode, fill character body/clothing with it. In `line-art` mode, use it only as sparse accents (small clothing edge, tiny badge, key label, or one prop); keep body/clothing interiors white.
- Accent A ({强调色A名} {色值}): Props, tools, flow arrows, path lines.
- Accent B ({强调色B名} {色值}): Key warnings, results, highlights, important labels.
- Environment: Light tint of primary color or light gray for ambient objects. Pure white background always.
- Black outline: All elements use black hand-drawn outline as structure.

Render mode: {line-art | colored}
{如果是 line-art}: Character body and clothing interiors remain white/unfilled. Primary appears only as sparse identity accents; Accent A/B appear on props, arrows, markers, and labels.
{如果是 colored}: Fill character body/clothing with primary color. Keep hand-drawn texture — NOT flat vector fill. Allow slight pen wobble and imperfect edges.

Visual style:
{视觉风格}. Keep the image clean, recognizable, and consistent with the IP Card.
Lots of white space (at least 35%). Main subject occupies 40%-60% of canvas.

Theme:
{主题}

Core idea:
{核心观点}

Composition type:
{构图类型}

Composition:
{具体画面。说明角色在哪里、做什么、主要物件是什么、信息如何流动。
说明环境元素用什么颜色（低饱和主色或浅灰）。}

Chinese handwritten labels:
{标注词 1} / {标注词 2} / {标注词 3} / {标注词 4}
(Label color: use Accent A for flow labels, Accent B for key points)

Constraints:
Use only the listed Chinese labels (max 5-8 short labels). Do not add extra text.
Do not make it a formal PPT infographic. Do not change the character identity.
Every field in the CHARACTER LOCK block must match exactly.
Do not use forbidden styles: {禁止风格}. One image explains one core idea.
Leave enough white space. Environment colors must be lighter/muted compared to character.
Character expression must match the content state (not always the same face).
```

## Photo → IP

For photo-to-IP creation, use `photo-to-ip.md` as the only authoritative workflow and prompt source. Do not maintain a second photo prompt here.

## Multi-IP Image

```text
Generate one standalone 16:9 horizontal Chinese article illustration with multiple personal IP characters.

Character A:
{IP A name and anchors}. Color system: {IP A 三元配色}. Render mode: {IP A render_mode}.
--- CHARACTER LOCK A (immutable — paste the full YAML block verbatim) ---
{IP A character_lock 完整 YAML 内容，包含所有额外身份锚点。不要省略任何字段。}
--- END CHARACTER LOCK A ---

Character B:
{IP B name and anchors}. Color system: {IP B 三元配色}. Render mode: {IP B render_mode}.
--- CHARACTER LOCK B (immutable — paste the full YAML block verbatim) ---
{IP B character_lock 完整 YAML 内容，包含所有额外身份锚点。不要省略任何字段。}
--- END CHARACTER LOCK B ---

Do not merge their appearances. Keep both identities visually distinct. Every field in each character's own CHARACTER LOCK must match exactly. Give each character a clear role in the scene.

Theme:
{主题}

Core idea:
{核心观点}

Composition:
{具体画面}

Chinese handwritten labels:
{短标注}

Constraints:
Use only the listed labels. Do not add extra text. Keep the scene clean. Avoid more than 2-3 characters. Preserve each IP's appearance anchors, character_lock, props, and personality.
```

## No-Text Fallback

Use this when Chinese text is unstable:

```text
Generate the same image with no text, no labels, no letters, and no symbols that resemble writing. Leave clean blank spaces where labels can be added later.
```

## Cover / Hero Image Template

```text
Generate one standalone {1:1 or 3:4} Chinese cover image.

Personal IP:
{IP 名字}, {职业/身份}. Palette preset: {palette_preset}. Gender metadata if relevant: {gender}.
Appearance anchors: {外形锚点}. Clothing anchors: {服装锚点}.
The character is the focal point — large, centered or slightly off-center.

--- CHARACTER LOCK (immutable — paste the full YAML block verbatim) ---
{character_lock 完整 YAML 内容，包含所有额外身份锚点。不要省略任何字段。}
--- END CHARACTER LOCK ---

Character expression: {default or acting state — energetic and welcoming}

Color system (三元配色):
- Primary ({主色名} {色值}): Identity color. In `colored` mode, fill character body/clothing. In `line-art` mode, keep body/clothing white and use primary only as sparse accents.
- Accent A ({强调色A名} {色值}): One signature prop.
- Accent B ({强调色B名} {色值}): Title text color or highlight.

Render mode: {line-art | colored}
{same rules as single image template}

Title:
{4-12 Chinese characters, bold, placed at top or side}

Composition:
IP character occupies 50%-70% of canvas. Background minimal — at most 1-2 environment objects in low saturation. Title is prominent but does not overlap character face.

Constraints:
Use only the listed title text. Do not add extra text or labels.
Character must be the visual focus. Keep background clean.
Every field in the CHARACTER LOCK block must match exactly.
One signature prop maximum. Do not clutter.
Leave enough breathing room around the title.
```

## Knowledge Card Template

```text
Generate one standalone 1:1 Chinese knowledge card.

Personal IP:
{IP 名字}, {职业/身份}. Appearance anchors: {外形锚点}.

--- CHARACTER LOCK (immutable — paste the full YAML block verbatim) ---
{character_lock 完整 YAML 内容，包含所有额外身份锚点。不要省略任何字段。}
--- END CHARACTER LOCK ---

Character expression: {default or acting state}

Color system (三元配色):
- Primary ({主色} {色值}): Character fill only in `colored` mode; sparse identity accent only in `line-art` mode.
- Accent A ({强调色A} {色值}): Three key points text color.
- Accent B ({强调色B} {色值}): Title or highlight.

Render mode: {line-art | colored}
{如果是 line-art}: Character body and clothing interiors remain white/unfilled. Primary appears only as sparse identity accents.
{如果是 colored}: Fill character body/clothing with primary color while preserving hand-drawn texture.

Title:
{短标题, 4-8 Chinese characters}

Three key points:
1. {点1, 2-6 chars}
2. {点2, 2-6 chars}
3. {点3, 2-6 chars}

Composition:
Title at top. IP character performing a simple action in center. Three short points listed below or beside character, each with a small icon or bullet. Clean card layout with rounded border in light primary tint.

Constraints:
Use only the listed text. Do not add extra text.
Every field in the CHARACTER LOCK block must match exactly.
Keep it card-like but hand-drawn, not corporate template.
Character should look engaged, not decorative.
```

## Prompt Record

Save the final prompt as `prompt.md` alongside generated outputs.
