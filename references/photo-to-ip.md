# Photo To IP

This is the entry point for regular users to quickly obtain a personal IP from a photo.

Creating an IP is not just generating a card — it also requires **4 standard reference images** that lock the character's visual identity for all future generations.

## Contents

- Workflow
- Feature Extraction Rules
- Photo → Cartoon Prompt Template
- Character Lock Extraction
- 4 Standard Reference Images
- Privacy Guardrails
- Confirmation Step
- Save To IP Object Folder

## Workflow

```
User provides photo
    ↓
Extract generalizable appearance features (hair / glasses / face shape / body type / clothing style / signature features)
    ↓
Map to hand-drawn cartoon style
    ↓
Apply three-color palette system
    ↓
Output initial IP Card (with character_lock) + 1 portrait preview
    ↓
User confirms or adjusts
    ↓
Generate 4 standard reference images (portrait / action / composition / style)
    ↓
Create IP object folder under ip-library/<ip-id>/
    ↓
Write ip-card.yaml + save 4 reference images + register in ip-registry.yaml
```

## Feature Extraction Rules

Extract **generalizable appearance anchors**, not precise real-person portraits or biometric identifiers:

| Extract | Description | Examples |
|---------|-------------|----------|
| Hair | Shape + length + curl/straight | Short messy / shoulder-length wavy / high ponytail / bun |
| Glasses | Presence + shape | Round / square / thin frame / none |
| Face shape | Generalized (only affects cartoon face) | Round / square / oval / heart |
| Body type | Generalized (only affects cartoon proportions) | Slim tall / rounded / medium / petite |
| Clothing style | Generalized | Casual tee / shirt / hoodie / artsy dress / sporty |
| Signature feature | 1-2 broad, drawable styling traits | Bangs / beard style / twin tails / scarf / cap / glasses style |

Do not extract or store face geometry measurements, exact distances, skin blemish maps, scars, iris details, birthmarks, EXIF metadata, location data, file names, or any other source-photo identifiers.

## Photo → Cartoon Prompt Template

```text
Create a cartoon-style personal IP character based on a reference photo.

Extract only these generalizable features from the photo:
- Hair: {发型概括}
- Glasses: {有无及形状}
- Face shape: {脸型}
- Body type: {体型}
- Clothing style: {服装风格}
- Signature feature: {标志特征}

Convert into a hand-drawn cartoon character with these rules:
- Cute but not childish, clean but not overly polished
- Use the IP's render mode and color system:
  - If `line-art`: keep character body/clothing interiors white, with primary color only as sparse identity accents
  - If `colored`: fill character body/clothing with primary color
  - Props use {强调色A}; highlights use {强调色B}
- Pure white background, black hand-drawn outline, slightly wobbly pen lines
- Character should be a consistent stylized cartoon IP based on broad features, NOT a recognizable real-person portrait
- The character must be simple enough to redraw consistently across different illustrations
- Expression: {默认表情}

Do NOT create an exact portrait copy. Do NOT include photorealistic details.
The output is a reusable cartoon IP character for article illustrations.
```

## Character Lock Extraction

After generating the portrait preview, extract a **`character_lock`** block — a precise description of the generated cartoon character's reusable visual identity. This is different from `visual_anchors` (which is a human-readable summary). `character_lock` is precise for the **cartoon IP output**, not for the source person's real face or biometric likeness.

Extract these fields from the generated portrait:

```yaml
character_lock:
  face: "卡通脸型描述，如：方圆脸，下巴微圆"
  hair: "卡通发型描述，如：短黑发，两侧更短，头顶稍长"
  eyes: "卡通眼部描述，如：细长黑眼，眼角微下垂"
  nose: "简化鼻部描述，如：小而直的鼻子"
  mouth: "简化嘴部描述，如：薄唇，嘴角平直"
  body: "卡通体型描述，如：中等偏瘦，肩宽适中"
  clothing_default: "默认服装，如：深靛蓝连帽衫，内搭白T恤"
  color_skin: "肤色，如：浅肤色，略偏暖白"
```

This block is **immutable** once confirmed. It is injected into every generation prompt as a locked section that cannot be paraphrased or simplified. It must not contain original photo file names, source paths, EXIF/location data, exact facial measurements, or uniquely identifying real-person details.

## 4 Standard Reference Images (Mandatory)

After the user confirms the IP Card and `character_lock`, generate 4 standard reference images. These are the visual anchors stored in `ip-library/<ip-id>/reference-images/`.

### 01-portrait.png — Portrait Anchor

```text
Generate a half-body standard portrait of {IP 名字}.

Character (character_lock — do not alter):
{character_lock 完整内容}

Pose: front-facing, neutral stance, arms relaxed at sides.
Expression: {default 表情}
Background: pure white.
Clothing: {clothing_default}
No props, no annotations, no text.
The character must fill 50%-60% of the canvas, centered.

This image locks the character's face, hair, glasses, clothing, and overall temperament.
```

### 02-action.png — Action Anchor

```text
Generate a full-body action pose of {IP 名字} performing a signature action.

Character (character_lock — do not alter):
{character_lock 完整内容}

Action: {一个最常见的签名动作，如"拆线团"或"抱孩子"}
Expression: {acting 表情}
Signature prop: {一个标志性道具}
Background: pure white, minimal environment.
1-2 short Chinese labels in Accent A color max.

This image locks the character's body proportions, prop usage, and gesture style.
```

### 03-composition.png — Composition Anchor

```text
Generate a typical 16:9 composition sample using {IP 名字}.

Character (character_lock — do not alter):
{character_lock 完整内容}

Composition type: {一个偏好构图，如"问题拆解图"或"单观点隐喻图"}
Theme: a simple generic topic to showcase the composition.
Expression: {thinking 或 acting 表情}
2-3 short Chinese labels.
Lots of whitespace (≥35%). Environment in low-saturation primary tint.

This image locks the layout, whitespace ratio, label placement, and environment style.
```

### 04-style.png — Style Anchor

```text
Generate a close-up style sample of {IP 名字}.

Character (character_lock — do not alter):
{character_lock 完整内容}

Focus: close-up showing line quality, color application, and annotation handwriting.
Show: the character's hand holding a prop with a short Chinese label written on it.
Background: pure white.
2 short Chinese labels in the IP's accent colors.

This image locks the line quality, color texture, and text handwriting style.
```

## Privacy Guardrails

- Photos are only used for feature extraction in the current session. **Do not store original photos, copied photo files, screenshots, EXIF metadata, source file names, or source paths** to any persistent location.
- Extract broad temperament and styling features, not precise likeness, biometric identifiers, or source-photo identifiers. Output cartoonized/stylized original characters.
- IP Card should record generalizable appearance anchors (e.g. "short hair, round face"), not precise facial measurements or uniquely identifying facial details.
- `character_lock` describes the generated cartoon IP, not the real person's face.
- The character card should be described as "original cartoon character based on {name}'s temperament", not "{name}'s portrait".
- Users may request deletion of all reference data and derived character cards at any time.
- If the user is a minor (<18), must remind that guardian consent is required before photo extraction.
- Do not write real-child identity details into public IP Cards.

## Confirmation Step

After extracting features, generating the portrait preview, and extracting `character_lock`, present to the user for confirmation:

```text
我从照片中提取了以下外形特征：
- 发型：{提取结果}
- 眼镜：{提取结果}
- 脸型：{提取结果}
- 体型：{提取结果}
- 服装风格：{提取结果}
- 标志特征：{提取结果}

character_lock（角色锁定块，每次生成时原样注入）：
{character_lock 完整内容}

这是生成的初版 IP Card 和标准肖像预览图。
请确认：
1. 外形特征是否准确？
2. character_lock 中的卡通角色描述是否需要调整？
3. 标志特征是否需要补充或修改？
4. 性格定位是否合适？
5. 配色方案是否满意？（默认{性别}配色 / 自定义）

确认后我会生成4张标准参考图并写入 IP 对象文件夹。
```

If the user says "不像我" or wants adjustments:
1. Ask which specific anchor is wrong (hair? glasses? face? clothing?).
2. Re-extract or adjust that anchor only — do not regenerate the entire card from scratch.
3. Regenerate the portrait preview with updated anchors.
4. Update `character_lock` accordingly.
5. Re-confirm.

## Save To IP Object Folder

Only after user confirmation:

1. Create folder: `ip-library/<ip-id>/`
2. Write `ip-card.yaml` (including `character_lock`).
3. Generate and save 4 reference images to `ip-library/<ip-id>/reference-images/`.
4. Add entry to `ip-library/ip-registry.yaml`.

Do NOT save inside the skill bundle's `assets/examples/`.
