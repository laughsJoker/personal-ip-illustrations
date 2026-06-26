# 个人 IP 配图

[English](README.md) | [简体中文](README.zh-CN.md) | [繁體中文](README.zh-TW.md)

这是一个 Codex skill，用于创建可复用的个人 IP 角色卡，并生成稳定一致的中文正文配图、封面图、知识卡片和视觉内容。

## 概览

Personal IP Illustrations 会把一个人的身份、气质、外形锚点、配色方案和内容领域，整理成一套可持续复用的角色系统。它适合公众号/博客正文配图、社媒封面、知识卡片、工作流视觉化、多 IP 同场景等任务。

这不是一次性的画图 prompt，而是一个“个人 IP 资产系统”：每个 IP 都有自己的角色卡、`character_lock`、标准参考图、配色规则、表情锚点和输出目录。

## 功能

- 从一句简短描述或照片的泛化特征创建结构化个人 IP Card。
- 使用 `character_lock` 保持角色外观一致。
- 支持 `line-art` 和 `colored` 两种渲染模式。
- 使用稳定的 `palette_preset` 和每个 IP 自己的三元配色。
- 支持文章配图 shot list、封面图、知识卡片、多 IP 画面等。
- 将用户真实 IP 资产保存在 workspace 的 `ip-library/` 中，不写入 skill 包。

## 安装

把这个文件夹复制到 Codex skills 目录：

```text
~/.codex/skills/personal-ip-illustrations
```

Windows 路径示例：

```text
C:\Users\<you>\.codex\skills\personal-ip-illustrations
```

## 使用

```text
Use $personal-ip-illustrations 为我创建个人 IP 角色卡，并生成4张标准参考图。
```

已有 IP 后，用户生成资产应保存在当前 workspace：

```text
<workspace-root>/ip-library/<ip-id>/
```

不要把真实用户数据、原始照片或生成输出保存到 skill 文件夹里。

## 隐私

照片转 IP 流程只提取宽泛、可绘制的风格特征。不要保存原始照片、照片副本、EXIF 元数据、源文件名、源路径、生物识别信息、精确面部测量或可唯一识别真人的细节。

`character_lock` 描述的是生成后的卡通 IP，不是真人的脸。

## 仓库结构

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

MIT. 见 `LICENSE`。
