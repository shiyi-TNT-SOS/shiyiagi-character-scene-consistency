---
name: shiyiagi-character-scene-consistency
description: "十一AGI 专属角色/场景一致性库。当用户需要让 AI 生成的连续镜头保持同一角色不变脸、同一场景不变景、关键道具不变样时使用——包括建立角色档案与场景资产、生成锚点图、跨镜头复用固定描述段、用首尾帧接力锁一致性、以及为即梦/可灵/Seedream/Grok 等引擎适配。触发词：角色一致性、场景一致性、跨镜头不变、不变脸、不变景、道具一致性、一致性库、character consistency。"
agent_created: true
license: MIT
user-invocable: true
tags: [consistency, shiyiagi, 十一AGI, 角色一致性, 场景一致性, 道具一致性, 跨镜头]
metadata:
  version: "1.0.0"
  brand: "十一AGI认知圈"
  owner: "爸爸"
---

# 十一AGI 角色 / 场景一致性库

把"换机位就变脸、每集场景都不一样、道具位置乱跳"三类穿帮，固化成可复用的跨镜头一致性工作流。专治 AI 连续生成的三类翻车：角色漂移（脸/发型/服装每镜变）、场景漂移（窗光向每集变、道具位置乱跳）、道具生灭（凭空出现/消失、材质变色）。

## Overview

核心判断：**一致性不是靠形容词堆出来的，是靠"可复用的资产 + 一次只改一个维度 + 接力锁死"锁出来的。** 本技能提供一条完整流水线——建库（角色档案+场景资产+道具清单，三件套各带参考图）→ 每镜复用固定描述段、只改一个维度 → 用三级一致性接力（文字串<参考图<首尾帧）兜底 → 三道质检关逐镜过关。它不替代专家技能，而是**总控层**：调用 `shiyi-agi-ip-character-studio` 建角色、调用 `shiyiagi-facial-expression` 编码表情、复用豆包「06 场景资产」建场景，并保证"脸/景/道具"三件在跨镜头时不漂。

## When to Use

- 用户要做连续镜头 / 多集内容，抱怨"换机位变脸""每集场景不一样""道具位置乱跳"
- 用户要建角色档案、场景资产、道具清单等"一致性基准资产"
- 用户要出锚点图、空景参考图、道具参考图，并跨镜头复用
- 用户要为即梦 / Seedance、可灵 / Kling、豆包 / Seedream、Grok 写带一致性约束的提示词
- 用户要验收成片，做跨镜 A/B 比对

**不适用**：纯单图无连续性诉求（走 ip-character-studio 即可）；面部表情编码细节（走 shiyiagi-facial-expression）；分镜 / 广告 / 故事结构（走 shiyiagi-director-*）。本技能只解决"跨镜头不变"这一层。

## How to Use

1. 读取 [references/consistency-workflow.md](references/consistency-workflow.md) 走总流程，理解「三级接力法 / 一致性预算 / 三不变清单」。**赶时间直接看 [references/quickstart.md](references/quickstart.md) 一页开工卡。**
2. 按总流程四阶段产出：
   - **建库**：角色档案+锚点图（→ ip-character-studio）、场景资产+空景图（→ 豆包场景资产 + scene-consistency.md）、道具清单+道具图（→ prop-consistency.md）。
   - **每镜**：套固定描述段 + 垫锚点图/尾帧 + 只改一个维度 + 套 negative prompt。
   - **接力**：连续镜头用 L3 首尾帧接力，每 3 跳回锁锚点图；跨场景不接力。
   - **质检**：用 consistency-checklist.md 三道关（建库期/每镜期/成片期）逐镜过关。
3. 角色细节复用 [references/character-consistency.md](references/character-consistency.md)（含角度维度取舍表）；场景细节复用 [references/scene-consistency.md](references/scene-consistency.md)（空间+光影双层面）；道具细节复用 [references/prop-consistency.md](references/prop-consistency.md)。
4. 一处红线漂移即退回对应阶段重出，不得带病出片。

## Resources

- `references/consistency-workflow.md` — 总流程：核心判断 + 四阶段 + **三级一致性接力法（L1文字串<L2参考图<L3首尾帧）+ 一致性预算（一次只改一个维度）+ 三不变清单（脸/景/道具）+ 上游 skill 路由表**
- `references/quickstart.md` — **一页开工速查卡**：0 判要不要上 → 建库三件套 → 每镜写法 → 三级接力锁死 → 三道关质检 → 引擎一句话。赶时间直接看这张。
- `references/walkthrough-demo.md` — **端到端示例（行为冒烟）**：林夏 / 老办公室 / 金丝眼镜 3 镜连续戏，跑通建库→每镜复用→L3 接力→三道关，附 5 条可直接复制的提示词。等级 2 行为测试证据。
- `references/character-consistency.md` — 角色跨镜头一致性：三种根因对策 + 最小可行流程（档案→锚点图→固定描述段→表情基线卡→每镜复用）+ **不同镜头角度下必须写死 vs 可放松** 取舍表
- `references/scene-consistency.md` — 场景跨镜头一致性（复用豆包「06 场景资产」）：**空间结构 + 光影时序双层面** + 换机位身份不丢 + 光影连续渐变 + 双轨参考图
- `references/prop-consistency.md` — 道具跨镜头一致性（全新）：根因对策 + **道具清单六要素模板** + 接触关系一致性 + 出场/消失连续性 + 成对道具 + 角色绑定
- `references/consistency-checklist.md` — 跨镜头一致性总检表：**建库期/每镜期/成片期三道关** + 引擎适配速查（Seedance首尾帧/Kling参考图/Seedream图像/Grok英文短句）+ 标准 negative prompt 模板
