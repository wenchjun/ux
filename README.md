# 🧩 wenchjun/ux — UX Skill 包

本仓库是一个 **Hermes Agent UX 技能包**，包含体验测评、竞品对比、端到端分析、产品洞察等 UX 相关技能。

## 📦 当前技能

| 技能 | 目录 | 说明 |
|:-----|:-----|:------|
| **ux-evaluator** | `ux-evaluator/` | 网页体验测评。四类页面（品牌/购买/操作/资料）× 21 子维度评分，基于用户体验五要素和尼尔森可用性原则，输出专业 HTML 测评报告 |
| **ux-e2e** | `ux-e2e/` | 端到端网页体验测评。覆盖客户旅程四阶段（感知→购买→使用→反馈），五层维度评估，含转化漏斗分析和 P0/P1/P2 问题清单 |
| **ux-comparative-workflow** | `ux-comparative-workflow/` | 串行化竞品对比工作流。四步引导式流程：待测评对象 → 竞品采集 → 补充内容 → 输出含竞品对比矩阵的完整测评报告 |
| **product-insight** | `product-insight/` | 产品洞察与战略规划。五维分析框架，适用于竞品分析、新产品立项、产品复盘等场景 |

## 🔗 技能关系

```
product-insight                  # 宏观产品战略分析
       ↓
ux-evaluator                     # 单页体验评估（基础）
       ↓
ux-comparative-workflow          # 竞品对比（基于 ux-evaluator）
ux-e2e                           # 端到端全链路评估
       ↓
(外部) ux-demo                   # 基于评估结果生成优化 Demo
```

## 🚀 安装方式

```bash
# 方式一：直接从仓库安装单个技能
hermes skills install wenchjun/ux/ux-evaluator
hermes skills install wenchjun/ux/ux-e2e
hermes skills install wenchjun/ux/ux-comparative-workflow

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
