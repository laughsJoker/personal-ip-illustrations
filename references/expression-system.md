# Expression System

Expression is the key dimension for a character to convey personality. Each image's expression should dynamically match the **content state**, not always show the same "calm face".

## 5 States × 6 Personalities Matrix

| Personality \ State | Default (idle) | Thinking | Acting | Result OK | Result Bad |
|---|---|---|---|---|---|
| **Rational Restrained** | Calm gaze, peaceful eyes | Slight frown, push glasses | Lips slightly pressed, focused forward | Nod, slight smile | Sigh, hand on forehead |
| **Gentle Healing** | Soft curved-eye smile, relaxed | Tilt head thinking, finger on chin | Reach out gently, lean forward | Big curved-eye smile, clap | Frown with concern, offer tissue |
| **Sharp Critical** | Single raised brow, half-smile | Eye roll, arms crossed | Shrug, helpless look | Smirk, thumbs up | Eye roll, pointing |
| **Lively Social** | Open-mouth smile, bright eyes | Eyes circling, hand on cheek | Wave arms, jump | Happy bounce, heart hands | Mouth O-shape, surprised |
| **Energetic Super-Mom** | Sparkling curved-eye smile, full of warmth | Tilt head, finger on chin, eyes looking up | Hands on hips or arms wide open, full of energy | Bouncing with joy, peace sign or clapping, crescent-moon eyes | Mouth O-shape surprised, or facepalm with wry smile "又来了" |
| **Craft Maker** | Focused looking down, serious | Squint at detail, lean close | Bite lip operating, fully absorbed | Wipe sweat smile, satisfied nod | Frown sigh, scratch head redo |

## Expression Trigger Rules

When generating an image, apply this logic:

```
1. Determine which stage the content belongs to:
   - raise problem / stuck / confused        → thinking
   - processing / acting / in-progress        → acting
   - success / solved / completed             → result-ok
   - failure / problem / warning              → result-bad
   - no clear stage                           → default (idle)

2. Select the expression row based on IP Card core_personality.

3. Inject the expression description into the prompt's character section.
```

## IP Card Expression Field

Each IP should customize its own expression library instead of directly copying the generic matrix above. The matrix is an initial template — adjust wording to the specific personality when creating an IP Card.

```yaml
# Example from xiao-tao.yaml (理性克制型, line-art, 无眼镜)
expression_anchors:
  default: 平静直视，表情认真但不紧张，嘴角微微放松
  thinking: 微皱眉头，眼神聚焦在某处
  acting: 嘴角微微抿紧，专注看着手中的工作
  result_ok: 轻轻点头，嘴角微扬
  result_bad: 叹一口气，轻轻摇头
```

## State Detection Heuristics

| Content cue words | State |
|---|---|
| 卡住, 困惑, 为什么, 怎么回事, 不知道 | thinking |
| 在做, 正在处理, 开始, 动手, 流程 | acting |
| 解决了, 成功, 完成, 好了, 搞定 | result-ok |
| 失败, 问题, 警告, 出错了, 又坏了 | result-bad |
| (no clear cue) | default |
