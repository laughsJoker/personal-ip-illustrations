# Examples Directory

This directory contains **read-only sample references and showcase images**.

## Structure

```
examples/
├── sample-cards/              # Sample IP Cards (YAML schema reference)
│   ├── xiao-tao-sample.yaml   # Male, line-art, indigo palette
│   ├── a-zhen-sample.yaml     # Female, colored, coral pink palette
│   └── xiao-qiang-sample.yaml # Male, line-art, indigo palette (lawyer)
│
└── showcase/                  # Demo images for README and skill promotion
    ├── xiao-tao/
    │   ├── 01-big-requirement.png    # 需求越说越大
    │   └── 02-ai-write-code.png      # AI帮我写代码
    ├── a-zhen/
    │   ├── 01-five-minutes.png       # 妈妈也需要五分钟
    │   └── 02-kid-tantrum.png        # 娃又在闹了
    └── xiao-qiang/
        ├── 01-contract-trap.png      # 这份合同有坑
        └── 02-friend-owes-money.png  # 朋友借钱不还
```

## What Does NOT Belong Here

- Real user IP Cards → go to `<workspace-root>/ip-library/<ip-id>/ip-card.yaml`
- Real user reference images → go to `<workspace-root>/ip-library/<ip-id>/reference-images/`
- Real generation outputs → go to `<workspace-root>/ip-library/<ip-id>/outputs/<date-topic>/`
- The live IP registry → goes to `<workspace-root>/ip-library/ip-registry.yaml`

**Never write user data into this directory.** It is bundled with the skill and will be overwritten on skill updates.
