# Examples Directory

This directory contains **read-only sample references only**.

## What's Here

- `sample-cards/`: Sample IP Cards for reference. These show the YAML structure and field conventions.
  - `xiao-tao-sample.yaml`: line-art mode, `indigo-engineering` palette
  - `a-zhen-sample.yaml`: colored mode, `coral-warm` palette
- `ip-registry.yaml`: Sample registry shape only. Live registries belong in `<workspace-root>/ip-library/ip-registry.yaml`.

## What Does NOT Belong Here

- Real user IP Cards → go to `<workspace-root>/ip-library/<ip-id>/ip-card.yaml`
- Real user reference images → go to `<workspace-root>/ip-library/<ip-id>/reference-images/`
- Real generation outputs → go to `<workspace-root>/ip-library/<ip-id>/outputs/<date-topic>/`
- The live IP registry → goes to `<workspace-root>/ip-library/ip-registry.yaml`

**Never write user data into this directory.** It is bundled with the skill and will be overwritten on skill updates.
