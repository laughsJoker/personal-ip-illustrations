# 个人 IP 视觉分身

[English](README.md) | [简体中文](README.zh-CN.md) | [繁體中文](README.zh-TW.md)

这是一个 Codex skill，用于把创作者本人或虚拟人设沉淀成可复用的个人 IP 视觉分身，并生成稳定一致的中文视觉内容：正文配图、封面图、知识卡片、工作流图和多角色画面。

这个项目不是一组一次性画图 prompt，而是一个面向 Codex 的小型角色资产系统：每个视觉分身都有结构化角色卡、稳定的 `character_lock`、标准参考图、配色规则、表情锚点和 workspace 级输出库。

## 为什么做这个

AI 图像生成很擅长画出一张好看的图，但不擅长在很多主题里持续保持同一个角色。对写作者、教育者、创作者、顾问、产品人和技术博主来说，视觉一致性很重要：同一个角色应该在不同文章和社媒内容里保持相同的脸、气质、服装、配色、道具和标注风格。

个人 IP 视觉分身的目标，就是把一个人的身份、气质和风格整理成一个可复用的 IP 对象。

你不再只是说：

```text
帮我为这篇文章画一张图。
```

而是可以说：

```text
Use $personal-ip-illustrations 用我已有的 IP，为这篇草稿生成 4 张正文配图。
```

skill 会解析 IP Card，注入完整 `character_lock`，选择表情状态，应用配色系统，规划视觉隐喻，并把输出保存在该 IP 自己的资料夹中。

## 功能

- 从一句简短描述创建结构化个人 IP Card。
- 从照片的宽泛特征创建卡通视觉分身，同时避免保存生物识别信息。
- 为新 IP 生成 4 张标准参考图。
- 生成稳定一致的正文配图。
- 为长文章规划配图 shot list。
- 生成社媒封面、主视觉和知识卡片。
- 支持单 IP 和明确要求时的多 IP 同场景画面。
- 使用 `character_lock` 保持角色身份一致。
- 支持 `line-art` 和 `colored` 两种渲染模式。
- 使用 `palette_preset` 和每个 IP 自己的三元配色。
- 将 prompt、manifest 和输出保存在 `ip-library/`。

## 适合谁

- 想拥有稳定视觉分身的写作者。
- 需要干净概念配图的技术博主和开发者。
- 需要温暖持续角色的教育、育儿、心理咨询类创作者。
- 需要解释框架或工作流的顾问、产品人和知识工作者。
- 想把个人 IP 做成可复用资产，而不是每次重新画图的内容创作者。
- 想用 Codex 做可复用视觉内容工作流的人。

## 核心概念

### IP Card

IP Card 是一个结构化 YAML 对象，用来描述一个可复用个人角色。它包含身份、气质、外形锚点、服装、道具、常见动作、内容领域、配色、渲染模式、表情锚点、禁用风格和示例主题。

### Character Lock

`character_lock` 是每次生成图片时注入 prompt 的不可变角色锁定块，用来保持角色身份一致。它描述的是生成后的卡通 IP，不是真人的脸。注入时应保留完整内容，包括眼镜、胡须风格、发饰、姿态、标志服装等额外锚点。

### 标准参考图

每个 IP 应该有 4 张标准参考图：

```text
01-portrait.png      锁定脸、发型、服装、气质
02-action.png        锁定身体比例、动作、道具用法
03-composition.png   锁定构图、留白、标签位置
04-style.png         锁定线条质量、颜色质感、标注风格
```

### Palette Preset

`palette_preset` 用来选择初始配色方向，最终写入 IP Card 的 `color_system` 才是生成时的真实依据。当前预设包括：

```text
indigo-engineering
coral-warm
custom
```

### 渲染模式

`line-art`：角色身体和衣服内部保持白色/不填充，主色只作为少量身份点缀。

`colored`：角色身体/衣服使用主色填充，但保留手绘质感。

## 我的图片怎么放

用户真实图片和生成资产不要放到这个 skill 文件夹里。你可以在 Codex 对话里直接上传图片，或把图片放在当前工作区，再把路径告诉 Codex；确认生成后，个人 IP 数据统一保存在 workspace 根目录的 `ip-library/`。

| 场景 | 你怎么放/怎么给 | Codex 会怎么处理 | 保存位置 |
|------|-----------------|------------------|----------|
| 用真人照片创建视觉分身 | 在 Codex 对话里上传图片，或提供本机图片路径，例如 `D:\photos\me.jpg` | 只提取发型、眼镜、脸型、体型、服装风格等宽泛特征；生成 IP Card、`character_lock` 和 4 张标准参考图 | 确认后保存到 `<workspace-root>/ip-library/<ip-id>/`；不保存原始照片 |
| 已经有标准参考图 | 放到 `<workspace-root>/ip-library/<ip-id>/reference-images/` | 作为后续生成的一致性锚点 | `reference-images/01-portrait.png` 到 `04-style.png` |
| 已经有 IP Card | 放到 `<workspace-root>/ip-library/<ip-id>/ip-card.yaml` | 读取角色设定、配色、表情锚点和 `character_lock` | `ip-card.yaml` |
| 生成正文配图、封面、知识卡片 | 不需要手动放图；让 Codex 生成 | 保存图片、prompt 和 manifest，方便追溯和复用 | `<workspace-root>/ip-library/<ip-id>/outputs/<date-topic>/` |
| 放公开示例 | 只放脱敏、可公开的样例 | 用于说明 schema 和风格，不作为你的真实 IP 数据 | `assets/examples/` |

如果照片涉及未成年人，提取特征前必须先确认已获得监护人同意。

## 安装

把这个文件夹复制到 Codex skills 目录：

```text
~/.codex/skills/personal-ip-illustrations
```

Windows 路径示例：

```text
C:\Users\<you>\.codex\skills\personal-ip-illustrations
```

然后在 Codex 对话中调用：

```text
Use $personal-ip-illustrations 为我创建个人 IP 视觉分身，并生成4张标准参考图。
```

## 如何使用

技术调用名仍然是 `$personal-ip-illustrations`。安装后，在 Codex 对话里按下面的表格直接说即可。

| 目标 | 你可以这样说 | Codex 会输出什么 |
|------|--------------|------------------|
| 从文字创建视觉分身 | `Use $personal-ip-illustrations 我是一个写 AI 编程和产品复盘的技术创作者，想创建一个个人 IP 视觉分身。` | IP Card、配色、表情锚点、`character_lock` 和 4 张标准参考图 |
| 从照片创建视觉分身 | `Use $personal-ip-illustrations 我上传了一张照片，帮我提取宽泛特征，做成个人 IP 视觉分身。` | 特征摘要、初版 IP Card、肖像预览；确认后生成 4 张标准参考图 |
| 规划文章配图 | `Use $personal-ip-illustrations 用小涛这个 IP，为这篇文章规划 5 张正文配图。` | shot list：放在哪、画什么、结构类型、角色动作、中文标注 |
| 直接生成正文配图 | `Use $personal-ip-illustrations 用小涛这个 IP，为这篇草稿生成 4 张正文配图。` | 多张 PNG、对应 prompt、manifest 和保存路径 |
| 生成封面图 | `Use $personal-ip-illustrations 用阿珍这个 IP，生成一张小红书封面，标题是「妈妈的五分钟」。` | 一张封面主视觉，并保存到该 IP 的 outputs 目录 |
| 修改已有图 | `Use $personal-ip-illustrations 这张图角色不像我，把发型和眼镜调回参考图。` | 局部修改建议或重新生成版本 |
| 多 IP 同场景 | `Use $personal-ip-illustrations 让小涛和阿珍一起出现在一张图里，表现「技术工具如何帮妈妈节省时间」。` | 两个视觉分身同场景，但保持身份独立不混合 |

只有用户明确要求多 IP 同场景时，才会使用多个 IP。

## 用户数据目录

用户真实 IP 数据应保存在 workspace，而不是 skill 文件夹：

```text
<workspace-root>/ip-library/
├── ip-registry.yaml
├── xiao-tao/
│   ├── ip-card.yaml
│   ├── reference-images/
│   └── outputs/
├── a-zhen/
│   ├── ip-card.yaml
│   ├── reference-images/
│   └── outputs/
└── xiao-qiang/
    ├── ip-card.yaml
    ├── reference-images/
    └── outputs/
```

每组输出建议包含：

```text
outputs/<date-topic>/
├── 01-*.png
├── prompt.md
└── manifest.yaml
```

不要把真实用户数据保存到 skill 文件夹里。

## 仓库结构

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
        ├── sample-cards/          # 只读示例 IP Card
        └── showcase/              # README 展示图
            ├── xiao-tao/
            ├── a-zhen/
            └── xiao-qiang/
```

## 隐私与安全

照片转 IP 流程只提取宽泛、可绘制的风格特征。

不要保存：

- 原始照片
- 照片副本
- EXIF 元数据
- 源文件名
- 源路径
- 生物识别信息
- 精确面部测量
- 可唯一识别真人的细节

`character_lock` 描述的是生成后的卡通 IP，不是真人的脸。

如果来源照片涉及未成年人，提取特征前必须获得监护人同意。

## 设计原则

- 把每个 IP 当作可复用角色系统，而不是一次性 prompt。
- 在不同主题中保持角色身份稳定。
- 让角色参与隐喻行动，而不是站在角落当装饰。
- 每张图只表达一个清晰观点。
- 中文标注要短、少、准。
- 背景保持干净、白底、留白充足。
- 用户数据必须放在 skill 包之外。

## 示例 IP Card

只读示例位于：

```text
assets/examples/sample-cards/
```

它们只用于展示 schema 和风格约定，不是真实用户数据。

## 效果展示

以下示例展示了 skill 对三个不同个人 IP 的生成效果。每个 IP 从一句简短描述创建，然后用于生成场景配图。所有图片都使用了 `character_lock` 注入、三元配色和表情锚点系统。

### 小涛 — 程序员

| | |
|---|---|
| **身份** | 程序员，男性 |
| **渲染模式** | `line-art`（线稿） |
| **配色** | 靛蓝 `#3B5B7E` + 橙 `#E89143` + 暖灰 `#9B9B9B` |
| **IP Card** | [`sample-cards/xiao-tao-sample.yaml`](assets/examples/sample-cards/xiao-tao-sample.yaml) |

**场景一：需求越说越大** — 一个小需求像吹气球一样越说越大，小涛冷静地拿出剪刀准备剪开。

![需求越说越大](assets/examples/showcase/xiao-tao/01-big-requirement.png)

**场景二：AI 帮我写代码** — AI 像一台自动写作机器源源不断产出代码，小涛是质检员，拿着放大镜逐行检查。

![AI帮我写代码](assets/examples/showcase/xiao-tao/02-ai-write-code.png)

---

### 阿珍 — 超级宝妈

| | |
|---|---|
| **身份** | 超级宝妈 / 生活博主，女性 |
| **渲染模式** | `colored`（上色） |
| **配色** | 珊瑚粉 `#E8826B` + 鼠尾草绿 `#8FB386` + 暖黄 `#F2C94C` |
| **IP Card** | [`sample-cards/a-zhen-sample.yaml`](assets/examples/sample-cards/a-zhen-sample.yaml) |

**场景一：妈妈也需要五分钟** — 阿珍终于找到五分钟独处时间，像个充电中的手机一样坐在沙发上闭眼微笑，周围的一切都暂停了。

![妈妈也需要五分钟](assets/examples/showcase/a-zhen/01-five-minutes.png)

**场景二：娃又在闹了** — 阿珍正准备喝一口热咖啡，孩子突然开始闹腾，她一手扶额一手还端着咖啡，生活就是这么猝不及防。

![娃又在闹了](assets/examples/showcase/a-zhen/02-kid-tantrum.png)

---

### 小强 — 律师

| | |
|---|---|
| **身份** | 律师，男性 |
| **渲染模式** | `line-art`（线稿） |
| **配色** | 靛蓝 `#3B5B7E` + 橙 `#E89143` + 暖灰 `#9B9B9B` |
| **IP Card** | [`sample-cards/xiao-qiang-sample.yaml`](assets/examples/sample-cards/xiao-qiang-sample.yaml) |

**场景一：这份合同有坑** — 看似正常的合同里藏着风险条款，小强用放大镜和红笔把它们一个个揪出来。

![这份合同有坑](assets/examples/showcase/xiao-qiang/01-contract-trap.png)

**场景二：朋友借钱不还** — 朋友借钱不还，小强把这事拆成三步：留证据、设期限、不翻脸，像搭积木一样一步步来。

![朋友借钱不还](assets/examples/showcase/xiao-qiang/02-friend-owes-money.png)

## Roadmap

- 增加更多配色预设。
- 增加更多风格原型。
- 增加更丰富的验证样例。
- 增加可选的 IP Card 校验脚本。
- 增加示例输出 manifest。

## 贡献

欢迎提交 issue 和 pull request。请不要在贡献内容里包含真实用户照片、真实私有 IP Card、私有生成资产或可识别个人身份的信息。

## License

MIT. 见 `LICENSE`。
