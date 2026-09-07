# Awesome AI4AI [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> 每周更新的 AI for AI Research（Auto-Research）策展：从可 hack 的训练底座出发，一路攀登到自动科研闭环。

本仓库以「AI 研究本身如何被 AI 自动化」为主线，持续跟踪该方向的开源项目与论文（**有开源代码实现优先**）。条目按训练生命周期的依赖关系与抽象层次递进组织：可 hack 底座 → 训练基础设施 → 自进化训练 → 数据层 → 评测 → 自动科研闭环。

**每周一更新**过去一周的新项目与新论文，详见 [weekly/](weekly/) 目录下的周报。

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

代码精简可读、能作为二次开发和自动科研实验底座的项目。轻量级底座的意义在于：给 AI researcher（以及 AI agent）一个复杂度可控的 starting point。

- [nanoGPT](https://github.com/karpathy/nanoGPT) - 极简可读的 GPT 训练实现，「读懂全部代码再改」路线的经典起点。
- [nanochat](https://github.com/karpathy/nanochat) - 从预训练到对话的全栈最小实现，覆盖完整 LLM 生命周期。
- [llm.c](https://github.com/karpathy/llm.c) - 纯 C/CUDA 的 GPT-2 训练，无框架依赖的极简参照。

## 训练基础设施

### 开箱即训

封装训练复杂度、配置即可跑的工具。

- [Unsloth](https://github.com/unslothai/unsloth) - 高效微调框架，以显存与速度优化见长。
- [LLaMA-Factory](https://github.com/hiyouga/LLaMA-Factory) - 覆盖 SFT/RLHF 全流程的开箱即训工具，生态与文档完整。
- [Axolotl](https://github.com/axolotl-ai-cloud/axolotl) - YAML 驱动的微调工具，社区配置模板丰富。

### 底层 Infra 封装 + 灵活训练 API

藏掉分布式与算力细节、但暴露灵活训练接口的框架——更适合自动科研 agent 编程调用。

- [Tinker Cookbook](https://github.com/thinking-machines-lab/tinker-cookbook) - Thinking Machines 的 Tinker 训练 API 与配套 cookbook，post-training 实验的托管式底座。
- [OpenRL](https://github.com/OpenRL-Lab/openrl) - 通用强化学习研究框架，统一接口支持单/多智能体、自博弈与自然语言任务。
- [OpenRLHF](https://github.com/OpenRLHF/OpenRLHF) - 基于 Ray + vLLM 的高性能 RLHF 框架。

## 自进化 / 自我博弈训练

模型在训练中自我生成信号、自我改进的方法与系统。_（持续补充中，见每周报告）_

## 数据层

合成数据、数据筛选与策展。

- [distilabel](https://github.com/argilla-io/distilabel) - 合成数据生成与 AI feedback 管线框架。
- [data-juicer](https://github.com/modelscope/data-juicer) - 大模型数据处理系统，覆盖清洗、筛选与去重。
- [NeMo Curator](https://github.com/NVIDIA/NeMo-Curator) - NVIDIA 的大规模语料策展工具集。

## 评测

训练后评测基准与数据，尤其是衡量「agent 能否自动完成 AI R&D」的基准。

- [PostTrainBench](https://github.com/aisa-group/PostTrainBench) - 衡量 CLI agent 能否在单卡 10 小时内自动完成后训练任务的基准。
- [lm-evaluation-harness](https://github.com/EleutherAI/lm-evaluation-harness) - 社区标准评测框架。
- [OpenCompass](https://github.com/open-compass/opencompass) - 覆盖多维能力的大模型评测体系。

## 自动科研闭环

端到端自动完成「提出假设 → 实验 → 分析 → 迭代」的系统。

- [The AI Scientist](https://github.com/SakanaAI/AI-Scientist) - Sakana AI 的自动化科研系统，从 idea 生成到论文写作的全流程尝试。

## 每周调研报告

每周一更新，收录过去一周值得关注的新项目与论文：

| 周 | 报告 |
| --- | --- |
| 2026-W37 | _生成中，周一发布_ |

完整索引见 [weekly/README.md](weekly/README.md)。

## 相关 Awesome 列表

- [awesome-algorithm-auto-tools](https://github.com/BinHPdev/awesome-algorithm-auto-tools) - 自动科研 / AutoML 方向的论文与项目索引。

## Contributing

欢迎 PR 与 Issue，收录标准与格式见 [CONTRIBUTING.md](CONTRIBUTING.md)。

## License

[CC0 1.0](LICENSE)
