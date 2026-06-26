# Validation Matrix

Use these cases to test the skill.

| Case | Input | Expected Result |
| --- | --- | --- |
| Create IP | "小涛，程序员" | Complete IP Card with `palette_preset`, three-color palette + expression anchors |
| Single IP image (indigo, line-art) | Use 小涛 for "需求越说越大" | Stable 小涛 appearance, indigo+orange+warm-gray palette correct, line-art mode with sparse primary accents |
| Single IP image (coral, colored) | Use 阿珍 for "妈妈的五分钟" | Stable 阿珍 appearance, coral pink body fill, sage green props, expression matches content state |
| Multi-IP choice | Registry has 小涛 and 阿珍, user does not specify | Ask user which IP to use |
| Multi-IP scene | "小涛和阿珍一起出现" | Both identities stay distinct, each keeps own three-color palette |
| Color drift check | Generate 3 images consecutively | Each image's three-color palette is consistent, environment lighter than character |
| Expression linkage | "Bug排查中" vs "Bug修好了" | thinking expression → result-ok expression, visibly different |
| Photo → IP | Upload a real-person photo + "帮我做IP" | Output cartoonized character card from broad features, not a precise or recognizable portrait |
| Long article planning | Paste article and ask for shot list | 4-6 cognitive-anchor shots, each with composition + expression suggestion |
| Text failure | Generated Chinese text is wrong | Suggest fewer labels or no-text fallback |
| Character drift | User says "不像我" | Diagnose missing anchors and regenerate |
| Forbidden style | User forbids cyber style | Prompt explicitly avoids it |
| Cover image | User asks for a cover | Uses cover composition, may include short title, IP character as focal point |
| Knowledge card | User asks for a knowledge card | Title + IP action + 3 short points format |

Pass only when the output follows IP selection rules, appearance consistency, three-color palette rules, expression matching, prompt constraints, and QA reporting.
