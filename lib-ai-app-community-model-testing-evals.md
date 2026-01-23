---
title: lib-ai-app-community-model-testing-evals
tags: [evaluation, large-language-model, prompt, promptfoo, testing]
created: 2026-01-12T10:03:22.768Z
modified: 2026-01-12T10:04:03.442Z
---

# lib-ai-app-community-model-testing-evals

# guide

- tips
  - 💡 ai推理失败的提示词, 可尝试在后面添加 think/explain step by step
# discuss-stars
- ## 

- ## 

- ## 

- ## [Asking 60 LLMs a set of 20 questions | Hacker News _2023209](https://news.ycombinator.com/item?id=37445401)
- In case anyone's interested in running their own benchmark across many LLMs, I've built a generic harness for this at https://github.com/promptfoo/promptfoo.
  - I encourage people considering LLM applications to test the models on their _own data and examples_ rather than extrapolating general benchmarks.

- ChainForge has similar functionality for comparing : https://github.com/ianarawjo/ChainForge

- GPT 4 and another LLM have given the right answer only after adding "Let's think step by step." to the original prompt.
  - With the simpler prompt, all the answers were wrong, most of them ridiculously wrong.

- ## [6 months of prompt engineering, what i wish someone told me at the start : r/PromptEngineering _202509](https://www.reddit.com/r/PromptEngineering/comments/1nuf9qf/6_months_of_prompt_engineering_what_i_wish/)
  - lesson 1: examples > instructions needed weeks to developing good instructions. Then tried few-shot examples and got better results instantly. Models learn by example patterns instead of by miles long lists of rules
  - lesson 2: versioning matters made minor prompt changes that completely destroyed everything. I now version all prompts and test systematically
  - Lesson 3: evaluation is harder and everyone resists it. Anyone can generate prompts. determining if they are actually good across all cases is the tricky bit. require appropriate test suites and measures.
  - lesson 4: prompt tricks lose out to domain knowledge fancy prompt tricks won't make up for knowledge about your problem space. Best outcomes happen when good prompts are coupled with knowledge about that space.
  - lesson 5: simple usually works best attempted complicated thinking chain, role playing, advanced personas. simple clear instructions usually do as well with less fragility most of the time
  - lesson 6: other models require other methods what is good for gpt-4 may be bad for claude or native models. cannot simple copy paste prompts from one system to another
  - Largest lesson 7: don’t overthink your prompts, start small and use models like GPT-5 to guide your prompts. I would argue that models do a better job at crafting instructions than our own today
  - Biggest error was thinking that prompt engineering was about designing good prompts. it's actually about designing standard engineering systems that happen to use llms

- How do you store and iterate on your prompts?
  - Git

- ## [I spent weeks learning prompt evals before realizing I was solving the wrong problem : r/PromptEngineering _202601](https://www.reddit.com/r/PromptEngineering/comments/1q756cv/i_spent_weeks_learning_prompt_evals_before/)
  - I went down the rabbit hole of formal evaluation frameworks. Spent weeks reading about PromptFoo, PromptLayer, and building custom eval harnesses. Set up CI/CD pipelines. Learned about different scoring metrics.
  - Then I actually tried to use them on a real project and hit a wall immediately.
  - Something nobody talks about: Before you can run any evaluations, you need test cases. And LLMs are terrible at generating realistic test scenarios for your specific use case. I ended up using the Claude Console to bootstrap a bunch of test scenarios, but they were hardly any better than just asking an LLM to make up a bunch of examples.
  - What actually worked: I needed to build out my test dataset manually.
  - The bottleneck isn't running evals - it's capturing these moments as they happen and building your dataset iteratively.
  - The real lesson: Start with a test dataset, not eval infrastructure.

    - Capture edge cases as you build. Test iteratively in your normal workflow. Graduate to formal evals when you actually have 100+ test cases and need automation.
# discuss-promptfoo-issues
- ## 

- ## 

- ## 

- ## 
# discuss-promptfoo
- ## 

- ## 

- ## I am really digging promptfoo for building your own benchmarks for LLM models.
- https://x.com/ctrlaltdylan/status/1973030611364536689
  - It's like specs for LLMs. I can test tokens usage, latency, accuracy, recall and verify that new models actually improve for my own use cases.
  - You can verify new models/providers actually improve for your use case. Even make sure the latency doesn't get out of control. Like Gemini introduced a new "thinking" param so you can control latency vs accuracy more. I tested a range of them and found a sweet spot.

- ## [Why isn't Promptfoo more popular? It's an open-source tool for testing LLM prompts. : r/PromptEngineering _202508](https://www.reddit.com/r/PromptEngineering/comments/1mwstpx/why_isnt_promptfoo_more_popular_its_an_opensource/)
- because nobody runs evals it just vibes and complaints 😜 Just like nobody create unit tests… unless you’re forced to by work.

- It's interesting how Promptfoo aims to streamline prompt testing, which could save devs time. But the challenge might be that integrating such tools feels optional if the existing workflow isn't broken. Balancing flexibility and rigid testing is tricky.

- Honestly, there are just too many LLM testing/observability tools — it’s like every dev tried building one over the weekend.
# discuss-prompt-management
- ## 

- ## 

- ## 

- ## [Anyobdy knows a a open source prompt evaluation/testing framework? : r/LLMDevs _202401](https://www.reddit.com/r/LLMDevs/comments/1905c8t/anyobdy_knows_a_a_open_source_prompt/)
- Promptfoo? https://promptfoo.dev

- If your outputs are enumerable, its probably easier to write the script yourself. Otherwise you can give https://spellbook.scale.com/ a shot.

- What about https://github.com/hegelai/prompttools

- Check out https://github.com/agenta-ai/agenta provides the tools for automatic evaluation, comparing the results side by side, and doing human evaluation / A/B testing on the results. It's open-source and can be self-hosted.

- try out this one: https://github.com/Addepto/contextcheck
# discuss-eval-solutions
- ## 

- ## 

- ## 

- ## [What AI evaluation tools have you actually used? What worked and what totally didn't? : r/Rag _202512](https://www.reddit.com/r/Rag/comments/1phgej6/what_ai_evaluation_tools_have_you_actually_used/)
- In practice, most teams don’t rely on a single evaluation tool. They try a few—Ragas, TruLens, DeepEval, LangSmith—and use them mainly to understand what to measure, not as a final verdict on quality. Ragas and DeepEval are popular starting points for RAG-style metrics, but people often struggle to fully trust the scores. LangSmith, Promptfoo, and Humanloop tend to help more with debugging, prompt iteration, and team visibility than with “is this answer actually good?” decisions.
  - Over time, many teams move toward custom evaluation scripts backed by LLM-as-a-judge and a growing set of real failure cases. Instead of chasing perfect metrics, they focus on regression, trends, and user-visible errors like hallucinations or bad retrieval. No tool magically improves an AI app on its own—the real value comes from clearly defining what failure looks like and making sure it doesn’t happen again.

- Used custom Python scripts for the longest time, which worked but became a maintenance nightmare. Tried Ragas for RAG-specific stuff, solid metrics but felt narrow. LangSmith is decent for LangChain apps if you're already in that ecosystem.
  - Honestly most eval tools fall into two camps: either too basic (just accuracy checks) or too complex (need a PhD to configure). The gap is usually around production monitoring vs pre-deployment testing.
  - What actually helped was combining programmatic checks (for format/structure) with LLM-as-judge evals (for quality) and running both in CI/CD plus on sampled production logs. Ended up trying Maxim since it had both the pre-built stuff and let me write custom evaluators. The part that actually saved time was not having to context switch between tools for pre-prod testing vs production monitoring.

- I use my llm as a judge and now using and developing sourcemapR(https://github.com/kamathhrishi/sourcemapr) to help debug RAG pipelines better
# discuss
- ## 

- ## 

- ## 

- ## 
