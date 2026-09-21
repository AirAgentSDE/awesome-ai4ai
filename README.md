# Awesome AI4AI [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> AI for AI Research：每周更新的自动科研（Auto-Research）策展 —— 从可 hack 的训练底座出发，一路攀登到自动科研闭环。

面向**研究者与工程师**。收录标准：**有开源代码实现优先**（Agent skills 也算）；每个条目力求一句话说清「它解决了什么问题、为什么值得选型」。

## 编排逻辑

整份列表不平铺罗列，而是沿一条主线攀登（按训练生命周期的依赖关系与抽象层次递进）：

```
可 hack 底座 → 训练基础设施 → 自进化/自博弈 → 数据层 → 评测 → 自动科研闭环
```

- **可 hack 底座**：代码精简可读，是二次开发与自动科研实验的 starting point；
- **训练基础设施**分两类：开箱即训（封装训练复杂度）与底层 infra 封装 + 灵活训练 API（藏掉分布式/算力细节、但暴露可编程训练接口）；
- **评测**既是训练生命周期的下游，也是闭环系统的「裁判」，放在闭环之前；
- **自动科研闭环**是主线终点：agent 自主完成「假设 → 实验 → 分析 → 迭代」。

## 领域脉络（2023–2026）

- **2023 · Agent 做 ML 的可测量化起点**：MLAgentBench 等基准把「agent 能否跑通 ML 实验」变成可量化问题，经典 AutoML 工具链仍是主力。
- **2024 · 要素成熟与首个闭环**：AI-Scientist 首次演示从 idea 到论文的全流程；MLE-bench 用 75 个 Kaggle 任务标尺化 ML 工程能力；自博弈（SPIN/SPPO）与合成数据管线（Magpie/Cosmopedia/distilabel）补全信号层与数据层。
- **2025 · 端到端系统与严格评测**：AI-Scientist-v2 引入 agent 树搜索，AI-Researcher 获 NeurIPS 2025 Spotlight，AgentLaboratory、RD-Agent 覆盖工业 R&D；PaperBench 用 8,316 个层级化 rubric 节点把「复现顶会论文」变成长程评测。
- **2026 · 极简闭环范式普及**：karpathy/autoresearch 以 630 行 Python 证明「一个文件 + 一个指标 + 固定时间预算」即可跑通自主研究循环（两天 700 次无人值守实验）；范式迅速泛化到 GPU kernel 优化（AutoKernel）与任意可度量指标（pi-autoresearch）；Training-as-a-Service（Tinker/Twinkle）让训练能力可被 agent 编程调用；PostTrainBench 开始直接考核 agent 的后训练实操；闭环交付形态向 Agent Skills 库收敛（见 [weekly/2026-W38](weekly/2026-W38.md)）。

## Contents

- [可 Hack 训练底座](#可-hack-训练底座)
- [训练基础设施](#训练基础设施)
  - [开箱即训](#开箱即训)
  - [底层 Infra 封装 + 灵活训练 API](#底层-infra-封装--灵活训练-api)
- [自进化 / 自我博弈训练](#自进化--自我博弈训练)
- [数据层](#数据层)
- [评测](#评测)
- [自动科研闭环](#自动科研闭环)
- [每周调研报告](#每周调研报告)
- [相关 Awesome 列表](#相关-awesome-列表)

---

## 可 Hack 训练底座

代码精简可读、能作为二次开发和自动科研实验底座的项目。轻量底座的意义在于：给 researcher（以及 research agent）一个复杂度可控的 starting point。

- [nanoGPT](https://github.com/karpathy/nanoGPT) - 极简可读的 GPT 训练实现，「读懂全部代码再改」路线的经典起点。
- [nanochat](https://github.com/karpathy/nanochat) - 从预训练到对话的全栈最小实现；karpathy/autoresearch 的默认实验底座。
- [llm.c](https://github.com/karpathy/llm.c) - 纯 C/CUDA 的 GPT-2 训练，无框架依赖的极简参照。

## 训练基础设施

### 开箱即训

封装训练复杂度、配置即可跑的工具。

- [Unsloth](https://github.com/unslothai/unsloth) - 高效微调框架，以显存与速度优化见长。
- [LLaMA-Factory](https://github.com/hiyouga/LLaMA-Factory) - 覆盖 SFT/RLHF 全流程的开箱即训工具，生态与文档完整。
- [Axolotl](https://github.com/axolotl-ai-cloud/axolotl) - YAML 驱动的微调工具，社区配置模板丰富。
- [ms-swift](https://github.com/modelscope/ms-swift) - ModelScope 的一站式训练框架，支持 600+ LLM 与 Transformers/Megatron 多后端。

### 底层 Infra 封装 + 灵活训练 API

藏掉分布式与算力细节、但暴露灵活训练接口的框架——更适合自动科研 agent 编程调用。

- [Tinker Cookbook](https://github.com/thinking-machines-lab/tinker-cookbook) - Thinking Machines 的托管训练 API 与配套 cookbook，以 LoRA 粒度暴露采样/logp/训练原语。
- [Twinkle](https://github.com/modelscope/twinkle) - ModelScope 的 Client-Server 训练工作台，接口为 Tinker API 超集，支持 torchrun/Ray/Serverless 多租户 TaaS。
- [OpenRL](https://github.com/OpenRL-Lab/openrl) - 通用强化学习研究框架，统一接口支持单/多智能体、自博弈与自然语言任务。
- [OpenRLHF](https://github.com/OpenRLHF/OpenRLHF) - 基于 Ray + vLLM 的高性能 RLHF 框架。
- [KDFlow](https://github.com/songmzhang/KDFlow) - 解耦架构的 LLM 蒸馏框架（SGLang 教师 + FSDP2 学生，hidden states 零拷贝传输），支持 on-policy KD 与跨 tokenizer，较同类框架提速 1.44×~6.36×。

## 自进化 / 自我博弈训练

模型在训练中自我生成信号、自我改进的方法与系统。

- [SPIN](https://github.com/uclaml/SPIN) - Self-Play fIN-tuning：模型以自身生成数据为对手迭代，无需额外人类标注逼近强模型（UCLA，2024）。
- [SPPO](https://github.com/uclaml/SPPO) - Self-Play Preference Optimization：博弈论视角下的自博弈偏好优化（UCLA，2024）。

## 数据层

合成数据生成、筛选与策展。

- [distilabel](https://github.com/argilla-io/distilabel) - 合成数据生成与 AI feedback 管线框架。
- [Magpie](https://github.com/Magpie-Align/Magpie) - 从对齐模型自合成指令数据的方法与管线，无需种子问题。
- [Cosmopedia](https://huggingface.co/datasets/HuggingFaceTB/cosmopedia) - HuggingFace 的大规模合成教科书语料，合成预训练数据的参照系。
- [data-juicer](https://github.com/modelscope/data-juicer) - 大模型数据处理系统，覆盖清洗、筛选与去重。
- [NeMo Curator](https://github.com/NVIDIA/NeMo-Curator) - NVIDIA 的大规模语料策展工具集。
- [CuratorKIT](https://github.com/Lexsi-Labs/CuratorKIT) - 后训练数据策展全生命周期流水线：溯源精确的幻觉门 + reward/多样性门 + 自适应修复，导出 TRL/Unsloth/AlignTune 就绪格式，每个样本可审计回源（Lexsi Labs，2026）。

## 评测

训练后评测基准与数据，尤其是衡量「agent 能否自动完成 AI R&D」的基准。

- [MLAgentBench](https://github.com/snap-stanford/MLAgentBench) - Stanford 2023，衡量 agent 跑通 ML 实验全流程的早期标尺。
- [MLE-bench](https://github.com/openai/mle-bench) - OpenAI，75 个 Kaggle 任务衡量 agent 的 ML 工程能力。
- [PaperBench](https://github.com/openai/preparedness) - OpenAI 2025，从零复现 20 篇 ICML 2024 论文，8,316 个层级化 rubric 节点 + LLM 裁判。
- [PostTrainBench](https://github.com/aisa-group/PostTrainBench) - 衡量 CLI agent 在给定算力预算内自动完成后训练任务的能力。
- [ResearchClawBench](https://github.com/InternScience/ResearchClawBench) - 端到端自主科研基准：40 个真实论文任务、10 学科，专家加权 rubric 对照评分，「50 分追平论文、70 分超越论文」，leaderboard 周更（SJTU/InternScience，2026）。
- [Agent²RL-Bench](https://github.com/microsoft/RD-Agent/blob/main/rdagent/scenarios/rl/autorl_bench/README.md) - 考核 agent 能否自主工程化完整 RL 后训练管线（含闭环在线 RL 与轨迹收集），带运行时行为诊断（Soochow/MSRA/PKU，2026）。
- [lm-evaluation-harness](https://github.com/EleutherAI/lm-evaluation-harness) - 社区标准评测框架。
- [OpenCompass](https://github.com/open-compass/opencompass) - 覆盖多维能力的大模型评测体系。

## 自动科研闭环

端到端自动完成「提出假设 → 实验 → 分析 → 迭代」的系统。

- [autoresearch](https://github.com/karpathy/autoresearch) - Karpathy 2026.03，630 行 Python：agent 改 train.py、5 分钟一实验、keep/discard 循环，两天 700 次无人值守实验；极简闭环的精神原点。
- [AI-Scientist](https://github.com/SakanaAI/AI-Scientist) - Sakana AI，从 idea 生成、实验到论文写作与自动评审的全流程尝试。
- [AI-Scientist-v2](https://github.com/SakanaAI/AI-Scientist-v2) - 引入 agent 树搜索，摆脱模板约束，产出 workshop 级论文。
- [AI-Researcher](https://github.com/HKUDS/AI-Researcher) - HKUDS，NeurIPS 2025 Spotlight；文献调研 → 假设 → 实现 → 实验 → 论文全闭环，支持两档自主性。
- [AgentLaboratory](https://github.com/SamuelSchmidgall/AgentLaboratory) - LLM agent 充当研究助理覆盖完整流水线，含 AgentRxiv 累积式研究框架。
- [RD-Agent](https://github.com/microsoft/RD-Agent) - 微软的 R&D 自动化平台：假设生成 → 实验设计 → 迭代改进，面向工业场景。
- [AutoResearchClaw](https://github.com/aiming-lab/AutoResearchClaw) - 全自主、自进化的研究 agent，从想法到论文。
- [EvoScientist](https://github.com/EvoScientist/EvoScientist) - 自进化多智能体「vibe research」，持久记忆驱动。
- [DeepScientist](https://github.com/ResearAI/DeepScientist) - 本地优先的自主研究工作室：基线复现 → 实验 → 论文级产出。
- [FAROS](https://github.com/OpenNSWM-Lab/FAROS) - 蓝图驱动的 AutoResearch 运行时：想法 → 实验 → 写作 → 同行评审。
- [NanoResearch](https://github.com/OpenRaiser/NanoResearch) - 轻量级自主研究助手（skills/agent 驱动），从选题到端到端研究。
- [scientific-agent-skills](https://github.com/K-Dense-AI/scientific-agent-skills) - 把任意 agent 变成 AI Scientist 的技能库：165 个验证 skill + 100+ 科学数据库，闭环系统的「动手能力」走标准化 skill 接口（K-Dense-AI，2026）。
- [DARE](https://github.com/yogsoth-ai/de-anthropocentric-research-engine) - 900+ 纯 markdown skill 的自主研究编排系统，10 个可组合 package、四层命令层级、非线性回溯，零运行时、兼容 75+ agent harness。
- [Open Science Desktop](https://github.com/ai4s-research/open-science) - 本地优先的开源科研工作台（Tauri + MCP + agent skills），产物全链路可回溯，`osd` CLI 可无头/远程驱动；ResearchClawBench Pass@1 榜首。
- [The Station](https://github.com/dualverse-ai/station) - 开放世界多智能体科学发现环境：无中央管理器，agent 自主探索、发表并建设共享文献（DualverseAI，v2.0.0）。

**autoresearch 衍生生态**：[autoresearch-mlx](https://github.com/karpathy/autoresearch) 的 Apple Silicon 移植、pi-autoresearch（把循环泛化到任意可度量指标）、uditgoenka/autoresearch（Claude Code 插件形态）、AutoKernel（同一范式用于 GPU kernel 自动优化，arXiv:2603.21331）。

## 每周调研报告

每周一 9:00 自动调研过去一周的新项目与论文，产出见 [weekly/](weekly/)。调研与编排要求（闭环）：

1. 条目五要素：**项目链接、论文 | 技术报告链接、一句话描述、出处、卖点**；
2. 开头一段说明本周新条目分别落在主线（底座 → … → 闭环）的哪一环；
3. 结尾固定两节：**Recommended Stacks**（面向个人开发者/单卡场景、能跑通完整闭环的最小组合）与 **Trends**（扣住主线的趋势判断）。

| 周 | 报告 |
| --- | --- |
| 2026-W38 | [周报：闭环 skill 层爆发，评测与数据层补收](weekly/2026-W38.md) |
| 2026-W37 | [基线特刊：Auto-Research 三年脉络（2023–2026）](weekly/2026-W37.md) |

完整索引与报告模板见 [weekly/README.md](weekly/README.md) 与 [weekly/TEMPLATE.md](weekly/TEMPLATE.md)。

## 相关 Awesome 列表

- [awesome-algorithm-auto-tools](https://github.com/BinHPdev/awesome-algorithm-auto-tools) - 自动科研 / AutoML 方向的论文与项目索引。
- [awesome-autoresearch](https://github.com/yibie/awesome-autoresearch) - autoresearch 范式的应用案例与讨论合集。
- [Auto-Research-Skills](https://github.com/brycewang-stanford/Auto-Research-Skills) - 自主科研 skills 与 agent 精选库。
- [Claw4Science](https://claw4science.org/zh) - 科研 AI agent 目录（含 OpenClaw 生态）。

## Contributing

欢迎 PR 与 Issue，收录标准与条目格式见 [CONTRIBUTING.md](CONTRIBUTING.md)。

## License

[CC0 1.0](LICENSE)
