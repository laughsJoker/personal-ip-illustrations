# 個人 IP 配圖

[English](README.md) | [简体中文](README.zh-CN.md) | [繁體中文](README.zh-TW.md)

這是一個 Codex skill，用於建立可重複使用的個人 IP 角色卡，並生成穩定一致的中文正文配圖、封面圖、知識卡片與視覺內容。

## 概覽

Personal IP Illustrations 會把一個人的身分、氣質、外形錨點、配色方案與內容領域，整理成一套可持續使用的角色系統。它適合公眾號/部落格正文配圖、社群封面、知識卡片、工作流視覺化、多 IP 同場景等任務。

這不是一次性的繪圖 prompt，而是一個「個人 IP 資產系統」：每個 IP 都有自己的角色卡、`character_lock`、標準參考圖、配色規則、表情錨點與輸出目錄。

## 功能

- 從一句簡短描述或照片的泛化特徵建立結構化個人 IP Card。
- 使用 `character_lock` 維持角色外觀一致。
- 支援 `line-art` 與 `colored` 兩種渲染模式。
- 使用穩定的 `palette_preset` 和每個 IP 自己的三元配色。
- 支援文章配圖 shot list、封面圖、知識卡片、多 IP 畫面等。
- 將使用者真實 IP 資產保存在 workspace 的 `ip-library/` 中，不寫入 skill 包。

## 安裝

把這個資料夾複製到 Codex skills 目錄：

```text
~/.codex/skills/personal-ip-illustrations
```

Windows 路徑範例：

```text
C:\Users\<you>\.codex\skills\personal-ip-illustrations
```

## 使用

```text
Use $personal-ip-illustrations 為我建立個人 IP 角色卡，並生成4張標準參考圖。
```

已有 IP 後，使用者生成資產應保存在目前 workspace：

```text
<workspace-root>/ip-library/<ip-id>/
```

不要把真實使用者資料、原始照片或生成輸出保存到 skill 資料夾裡。

## 隱私

照片轉 IP 流程只提取寬泛、可繪製的風格特徵。不要保存原始照片、照片副本、EXIF 中繼資料、來源檔名、來源路徑、生物識別資訊、精確臉部測量或可唯一識別真人的細節。

`character_lock` 描述的是生成後的卡通 IP，不是真人的臉。

## 倉庫結構

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

MIT. 見 `LICENSE`。
