# shiyiagi-character-scene-consistency

一句话：把「换机位就变脸、每集场景都不一样、道具位置乱跳」三类穿帮，固化成可复用的跨镜头一致性工作流。

它是十一AGI 导演 skill 家族的**总控层**——不替代专家技能，而是保证「脸 / 景 / 道具」三件在跨镜头时不漂。

## 它解决什么

| 翻车 | 根因 | 本 skill 的解法 |
|---|---|---|
| 换机位就变脸 | 档案模糊 / 无锚点图 / 一次改太多维度 | 角色档案 + 锚点图 + 固定描述段，每镜只改一个维度 |
| 每集场景都不一样 | 光源方向没写死、空间结构没定死 | 场景资产定死四要素（空间 / 光向 / 主色调 / 标志道具）+ 空景参考图 |
| 道具位置乱跳、凭空生灭 | 道具没登记、接触关系没锁 | 道具清单六要素 + 接触关系 + 出场/消失连续性 |

## 核心方法

1. **三级一致性接力法**——按可靠性从低到高：`L1 文字串（固定描述段）` < `L2 参考图（锚点图/空景图垫图）` < `L3 首尾帧接力`。连续镜走 L3，每 3 跳回锁锚点图，跨场景不接力。
2. **一致性预算**——一场戏一次只改一个维度（表情 / 姿势 / 机位 / 光影），其余锁死。
3. **三不变清单**——脸不变、景不变、道具不变，逐镜红线自检。

> 口诀：**文字串保底、参考图稳压、首尾帧锁死；跨场景不接力、每三跳回锚。**

## 交付物

- 建库三件套：角色档案 + 锚点图 / 场景资产 + 空景参考图 / 道具清单 + 道具参考图
- 每镜提示词（固定描述段 + 垫图 + 只改一个维度）
- 三道关质检：建库期 / 每镜期 / 成片期 A/B 比对

## 目录结构

```text
shiyiagi-character-scene-consistency/
├── SKILL.md
├── agents/openai.yaml
└── references/
    ├── consistency-workflow.md     # 总流程 + 三级接力 + 一致预算 + 路由表
    ├── character-consistency.md    # 角色跨镜一致（含角度取舍表）
    ├── scene-consistency.md        # 场景跨镜一致（空间 + 光影时序）
    ├── prop-consistency.md         # 道具跨镜一致（六要素 + 接触关系）
    ├── consistency-checklist.md    # 三道关 + 引擎适配 + negative 模板
    ├── quickstart.md               # 一页开工速查卡
    └── walkthrough-demo.md         # 端到端示例（林夏 / 老办公室 / 金丝眼镜）
```

## 怎么用

**安装**

```bash
npx -y skills add shiyi-TNT-SOS/shiyiagi-character-scene-consistency -g --all
```

或把整个目录复制到你的 Agent 技能目录（豆包为 `...\.doubao\agent_mode\workspace\.user_skills\`）。

**流程**：建库（角色 + 场景 + 道具三件套）→ 每镜套固定描述段 + 垫图 + 只改一个维度 → L3 首尾帧接力 → 过三道关再拼。赶时间直接看 `references/quickstart.md`。

## 适用 / 不适用

**适用**：多镜 / 多集 / 有固定角色或场景的连续内容；要建一致性资产库；要为即梦 / 可灵 / Seedream / Grok 写带一致性约束的提示词。

**不适用**：纯单图无连续性诉求（走 `shiyi-agi-ip-character-studio`）；面部表情编码细节（走 `shiyiagi-facial-expression`）；分镜与故事结构（走 `shiyiagi-director-*`）。

## 依赖与协作

复用 `shiyi-agi-ip-character-studio`（角色档案 / 锚点图）、`shiyiagi-facial-expression`（表情编码）、豆包「06 场景资产」（场景资产）三处上游资产；本 skill 负责把它们编排成一条流水线。

## 版本与授权

- 版本：`1.0.0`
- 授权：MIT（见 SKILL.md frontmatter）。学习与**非商业**用途可自由使用；商用请先联系作者授权。
- 作者：柳十一（十一AGI认知圈）

## 系列导航

| Skill | 定位 | 仓库 |
|---|---|---|
| shiyiagi-director-action | 武打 / 格斗 / 动作戏 | [shiyiagi-director-action](https://github.com/shiyi-TNT-SOS/shiyiagi-director-action) |
| shiyiagi-director-ad-tvc | 品牌广告片 / TVC | [shiyiagi-director-ad-tvc](https://github.com/shiyi-TNT-SOS/shiyiagi-director-ad-tvc) |
| shiyiagi-director-film | 故事片 / 叙事短片 | [shiyiagi-director-film](https://github.com/shiyi-TNT-SOS/shiyiagi-director-film) |
| shiyiagi-director-story-selling | 剧情化带货短视频 | [shiyiagi-director-story-selling](https://github.com/shiyi-TNT-SOS/shiyiagi-director-story-selling) |
| shiyiagi-facial-expression | 面部表情量化编码 | [shiyiagi-facial-expression](https://github.com/shiyi-TNT-SOS/shiyiagi-facial-expression) |
| **shiyiagi-character-scene-consistency** | **角色 / 场景跨镜头一致性（总控层）** | **本仓库** |
