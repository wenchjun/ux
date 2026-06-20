# 🧩 wenchjun/ux — UX Skill 包

本仓库是一个 **Hermes Agent 技能包**，包含多个 UX 相关的技能，每个技能放在独立子目录中。

## 📦 当前技能

| 技能 | 目录 | 说明 |
|:-----|:-----|:------|
| **ux-evaluator** | `ux-evaluator/` | 网页体验测评，基于用户体验五要素输出 HTML 报告 |
| **product-insight** | `product-insight/` | 产品洞察与战略规划，五维分析+竞品对比+行业趋势研究 |

## 🚀 安装方式

```bash
# 方式一：安装单个技能
hermes skills install wenchjun/ux/ux-evaluator

# 方式二：添加整个仓库为技能源（推荐，可搜索全部技能）
hermes skills tap add wenchjun/ux
hermes skills search 关键词
hermes skills install <找到的技能名>
```

## 📝 添加新技能

在根目录下创建新子目录，放入 `SKILL.md`，并更新 `.well-known/skills/index.json`：

```
my-skill/
└── SKILL.md
```

然后提交推送即可。
