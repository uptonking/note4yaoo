---
title: lib-ai-app-benchmark
tags: [ai, benchmark, large-language-model]
created: 2024-04-19T12:23:14.454Z
modified: 2024-04-19T12:23:44.448Z
---

# lib-ai-app-benchmark

# guide

# benchmark
- leaderboard
  - https://chat.lmsys.org/?leaderboard
    - https://leaderboard.lmsys.org
    - [Open LLM Leaderboard - a Hugging Face Space by open-llm-leaderboard](https://huggingface.co/spaces/open-llm-leaderboard/open_llm_leaderboard#/)

- [大语言模型评测数据集](https://fm.ai.tsinghua.edu.cn/superbench/#/)
  - ExtremeGLUE是一个包含72个中英双语传统数据集的高难度集合，旨在为语言模型提供更严格的评测标准，采用零样本cot评测方式，并根据特定要求对模型输出进行评分。我们首先使用了超过20种语言模型进行初步测试，包括了gpt4、claude、vicuna、wizardlm和chatglm等。我们基于所有模型的综合表现，决定了每个分类中挑选出难度最大的10%～20%数据，将它们组合为"高难度传统数据集"。
  - CodeBench是一个评估模型代码能力的基准测试，包括基础编程、算法逻辑和多语言代码生成与翻译，由Natural Code Bench、Humaneval和Mbpp三大数据集组成，模拟真实编程场景并考核多语言环境下的代码理解和生成技巧。
  - AlignBench旨在全面评测大模型在中文领域与人类意图的对齐度，通过模型打分评测回答质量，衡量模型的指令遵循和有用性。它包括8个维度，如基本任务和专业能力，使用真实高难度问题，并有高质量参考答案。优秀表现要求模型具有全面能力、指令理解和生成有帮助的答案。
  - AgentBench是一个评估语言模型在操作系统、游戏和网页等多种实际环境中作为智能体性能的综合基准测试工具包。
  - SafetyBench是首个全面的通过单选题的方式评估大型语言模型安全性的测试基准。
# comparison

# more
