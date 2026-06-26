# IP Card Template

Use an IP Card to preserve a user's character identity across generations.

## Contents

- Minimal Questions
- Human-Readable Template
- Machine-Readable YAML
- Validation Rules
- Versioning

## Minimal Questions

Ask at most these five questions when the user gives too little information:

1. IP name?
2. Occupation or identity?
3. What personality should people feel?
4. What should the character look like?
5. What style should be avoided?

If the user gives enough hints, infer a draft card and ask for confirmation instead of blocking.

## Human-Readable Template

```text
IP 名字：
职业/身份：
性别：
配色预设：
一句话定位：
核心性格：
辅助性格：
外形锚点：
服装锚点：
常用道具：
常见动作：
适合内容：
视觉风格：
渲染模式：        # 线稿模式 / 上色模式
颜色系统：
  主色：
  强调色A：
  强调色B：
  环境色：
表情锚点：
  默认：
  思考中：
  行动中：
  结果好：
  结果差：
角色锁定块（character_lock）：   # 从卡通参考图提取的角色锁定描述，每次生成原样注入，不可改写；不要记录真人照片来源或生物识别细节
  脸型：
  发型：
  眼睛：
  鼻子：
  嘴巴：
  体型：
  默认服装：
  肤色：
中文标注风格：
常用隐喻：
偏好构图：
禁止风格：
禁止行为：
示例主题：
```

## Machine-Readable YAML

Below is a complete example based on the actual `xiao-tao.yaml` sample card. See `assets/examples/sample-cards/xiao-tao-sample.yaml` for the bundled sample and `ip-library/<ip-id>/ip-card.yaml` for live user cards.

```yaml
ip_id: xiao-tao
ip_name: 小涛
status: active
version: v2
identity: 程序员
gender: male
palette_preset: indigo-engineering
render_mode: line-art
positioning: 把复杂问题拆成能处理的小块的人
core_personality:
  - 清醒
  - 克制
  - 耐心
secondary_traits:
  - 冷幽默
  - 有点疲惫但不丧
  - 默默解决问题
visual_anchors:
  - 短黑发，两侧剃短渐变，头顶稍长（寸头风格）
  - 方圆脸，下颌线清晰
  - 无眼镜
  - 帽衫/连帽外套是标志性服装
clothing:
  - 深色连帽外套 / 帽衫
  - 简单 T 恤（内搭）
signature_props:
  - 电脑包
  - 便利贴
  - 任务卡
  - 工具箱
  - 日志纸条
  - 咖啡杯
common_actions:
  - 拆线团
  - 切任务卡
  - 看日志
  - 修水管
  - 拧螺丝
  - 背服务器
  - 给 Bug 贴标签
content_domains:
  - 技术文章
  - AI 编程
  - Bug 排查
  - 项目复盘
  - 职场协作
  - 效率工具
visual_style: 白底手绘工程草图，黑色线稿，大量留白
color_system:
  primary: 靛蓝
  primary_hex: "#3B5B7E"
  accent_a: 橙色
  accent_a_hex: "#E89143"
  accent_b: 暖灰
  accent_b_hex: "#9B9B9B"
  environment: 浅蓝灰
environment_rules:
  background: 纯白
  ambient_tint: primary 20%
  no_shadows: true
  no_gradients: true
expression_anchors:
  default: 平静直视，表情认真但不紧张，嘴角微微放松
  thinking: 微皱眉头，眼神聚焦在某处
  acting: 嘴角微微抿紧，专注看着手中的工作
  result_ok: 轻轻点头，嘴角微扬
  result_bad: 叹一口气，轻轻摇头
character_lock:
  # 从卡通 01-portrait.png 提取的角色锁定描述，每次生成原样注入 prompt，不可改写；不要记录真人照片来源或生物识别细节
  face: 方圆脸，下颌线清晰但不锋利，颧骨略宽，下巴微圆
  hair: 寸头，两侧剃短到3mm渐变，头顶长约4cm，自然黑色，发际线整齐
  eyes: 细长眼，单眼皮，眼角微下垂，瞳孔黑色
  nose: 鼻梁直，鼻头略圆，鼻翼适中
  mouth: 薄唇，嘴角平直
  body: 中等偏瘦，肩宽适中，7头身比例
  clothing_default: 深靛蓝连帽衫，拉链半开，内搭白色圆领T恤
  color_skin: 浅肤色，略偏暖白
annotation_style: 短、克制、冷幽默，每处 2-8 个字
metaphor_pool:
  - 线团
  - 黑盒
  - 管道
  - 任务卡
  - 工具箱
  - 日志
  - 开关
  - 漏斗
  - 旧机器
composition_preferences:
  - 问题拆解图
  - 工作流图
  - 前后对比图
  - 单观点隐喻图
avoid_styles:
  - 赛博黑客
  - 二次元
  - 商业扁平插画
  - PPT 架构图
  - 苦逼程序员段子
avoid_behaviors:
  - 不要把小涛画成超级英雄
  - 不要让他只站在角落
  - 不要堆满代码截图
example_topics:
  - 需求变大
  - Bug 排查
  - 上线前一晚
  - AI 帮我写代码
  - 别急着重构
creation_basis: photo-derived-cartoon-ip
```

## Validation Rules

- `ip_id` must use lowercase letters, digits, and hyphens.
- `status` must be `active`, `draft`, or `archived`.
- `version` should use `v1`, `v2`, etc.
- Include at least 3 visual anchors.
- Include at least 3 avoid styles.
- Personality must translate into visible action.
- Appearance anchors must be drawable, not abstract.
- `gender` is optional metadata. If present, use `male`, `female`, `unspecified`, or `custom`; do not use gender as the only palette decision.
- `palette_preset` determines the default palette. Use `indigo-engineering`, `coral-warm`, `custom`, or a project-specific slug. `color_system` is the source of truth after colors are confirmed.
- `render_mode` must be `line-art` or `colored`.
- `color_system` must include primary, accent_a, accent_b with hex values.
- `expression_anchors` should include all 5 states (default/thinking/acting/result_ok/result_bad).
- `character_lock` must include face, hair, eyes, nose, mouth, body, clothing_default, color_skin. This block is extracted from the cartoon `01-portrait.png`, is immutable once confirmed, and must not contain original photo paths, EXIF/location data, precise facial measurements, or uniquely identifying real-person details.

## Versioning

Do not silently mutate an established IP.

- Minor wording, props, or example-topic changes can stay on the same version.
- Appearance-anchor changes should create a new version.
- Major visual-style changes should create a new version.
- `character_lock` changes require a new version AND regenerating all 4 reference images.
- Historical outputs remain bound to the version used at generation time.
