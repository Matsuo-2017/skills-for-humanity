# Open-source inference-time reasoning techniques and agent frameworks (state as of 2026-09-29)

Scope note: this covers inference-time / orchestration techniques and agent scaffolds only. Model training code and skill libraries are out of scope. All GitHub metadata (stars, forks, license, last push) below was pulled live from the GitHub API on 2026-09-29 via the GitHub MCP search tool; other claims carry their source date. arxiv.org, huggingface.co, alphaxiv, semanticscholar and most tech-blog aggregators were blocked by the network proxy in this session, so several paper claims rest on search-result snippets and secondary write-ups rather than the full PDF; these are marked "(snippet-level)".

## Repository reference table (GitHub API, 2026-09-29)

### Technique implementations (research reference code)

| Repo | Pattern | Stars | License | Last push | Status |
|---|---|---|---|---|---|
| [stanfordnlp/dspy](https://github.com/stanfordnlp/dspy) | Structured-prompting compiler / program optimizer | 38,411 | MIT | 2026-09-28 | Active (745 open issues) |
| [gepa-ai/gepa](https://github.com/gepa-ai/gepa) | Reflective prompt/program evolution (GEPA) | 6,789 | MIT | 2026-09-28 | Active; created 2025-08 |
| [princeton-nlp/tree-of-thought-llm](https://github.com/princeton-nlp/tree-of-thought-llm) | Tree of Thoughts (NeurIPS 2023) | 6,073 | MIT | 2025-01-16 | Dormant (~20 months) |
| [noahshinn/reflexion](https://github.com/noahshinn/reflexion) | Reflexion (verbal RL / episodic reflection) | 3,288 | MIT | 2025-01-14 | Dormant |
| [spcl/graph-of-thoughts](https://github.com/spcl/graph-of-thoughts) | Graph of Thoughts | 2,841 | Custom (NOASSERTION) | 2026-03-24 | Low activity |
| [openreasoner/openr](https://github.com/openreasoner/openr) | PRM training + PRM-guided search (MCTS/beam) | 1,858 | MIT | 2025-01-17 | Dormant |
| [madaan/self-refine](https://github.com/madaan/self-refine) | Self-Refine (feedback-refine loop) | 822 | Apache-2.0 | 2024-10-04 | Dormant |
| [Skytliang/Multi-Agents-Debate](https://github.com/Skytliang/Multi-Agents-Debate) | MAD (adversarial debate, judge) | 613 | GPL-3.0 | 2025-12-16 | Low activity |
| [composable-models/llm_multiagent_debate](https://github.com/composable-models/llm_multiagent_debate) | Du et al. multiagent debate (ICML 2024) | 552 | none listed | 2025-04-24 | Dormant |
| [reasoning-machines/pal](https://github.com/reasoning-machines/pal) | Program-Aided Language models | 529 | Apache-2.0 | 2023-06-30 | Abandoned (3+ years) |
| [RyanLiu112/Awesome-Process-Reward-Models](https://github.com/RyanLiu112/Awesome-Process-Reward-Models) | PRM catalogue (not code) | 180 | none | 2026-09-13 | Active list |
| [liaolea/M3MAD-Bench](https://github.com/liaolea/M3MAD-Bench) | Multi-agent debate benchmark harness (ACM MM 2026) | 6 | MIT | 2026-07-10 | Recent |

Source for all rows: GitHub API via MCP, 2026-09-29.

### Agent frameworks

| Repo | Stars | License | Last push | Created | Notes |
|---|---|---|---|---|---|
| [anthropics/claude-code](https://github.com/anthropics/claude-code) | 148,522 | (no license field returned) | 2026-09-29 | 2025-02 | Harness that the Agent SDK wraps; 13,621 open issues |
| [microsoft/autogen](https://github.com/microsoft/autogen) | 61,215 | CC-BY-4.0 (docs; code was MIT) | 2026-04-15 | 2023-08 | Maintenance mode (see Q2) |
| [crewAIInc/crewAI](https://github.com/crewAIInc/crewAI) | 59,158 | MIT | 2026-09-29 | 2023-10 | Active |
| [langchain-ai/langgraph](https://github.com/langchain-ai/langgraph) | 42,448 | MIT | 2026-09-29 | 2023-08 | Active |
| [openai/openai-agents-python](https://github.com/openai/openai-agents-python) | 29,755 | MIT | 2026-09-29 | 2025-03-11 | Active; only 11 open issues |
| [huggingface/smolagents](https://github.com/huggingface/smolagents) | 29,576 | Apache-2.0 | 2026-09-23 | 2024-12 | Active |
| [mastra-ai/mastra](https://github.com/mastra-ai/mastra) | 28,411 | Custom (Apache-2.0 core + EE license) | 2026-09-29 | 2024-08 | Active, TypeScript |
| [letta-ai/letta](https://github.com/letta-ai/letta) | 24,966 | Apache-2.0 | 2026-09-10 | 2023-10 | 0 open issues; dev moved to letta-code |
| [google/adk-python](https://github.com/google/adk-python) | 21,675 | Apache-2.0 | 2026-09-29 | 2025-04 | Active |
| [pydantic/pydantic-ai](https://github.com/pydantic/pydantic-ai) | 20,251 | MIT | 2026-09-29 | 2024-06 | Active |
| [microsoft/agent-framework](https://github.com/microsoft/agent-framework) | 13,853 | MIT | 2026-09-29 | 2025-04 | AutoGen + Semantic Kernel successor |
| [anthropics/claude-agent-sdk-python](https://github.com/anthropics/claude-agent-sdk-python) | 8,185 | MIT | 2026-09-29 | 2025-06 | Active; 514 open issues |
| [ag2ai/ag2](https://github.com/ag2ai/ag2) | 4,968 | Apache-2.0 | 2026-09-28 | 2024-11 | Community fork of AutoGen 0.2 |
| [letta-ai/letta-code](https://github.com/letta-ai/letta-code) | 3,479 | Apache-2.0 | 2026-09-29 | 2025-10 | Letta's current harness (TypeScript) |

Source for all rows: GitHub API via MCP, 2026-09-29.

## Key Question 1: Which inference-time techniques have the strongest measured effect for current frontier models, and which are obsolete now that models reason natively?

### Takeaway
As of September 2026 the strongest, best-evidenced inference-time levers are (a) the model's own native adaptive thinking (Anthropic reports adaptive thinking beats fixed-budget extended thinking in internal evals), (b) sequential refinement chains with entropy-weighted voting rather than parallel majority voting at matched compute, and (c) prompt/program optimizers such as DSPy+GEPA that tune the scaffold offline. Manual "think step by step" CoT, prefill tricks, hand-built ToT/GoT search and PRM-guided beam search are documented as fallbacks or as superseded for native reasoning models, though self-consistency still buys accuracy at very large token cost.

### Cited Findings

Native thinking replaces prompted CoT:
- Anthropic's current prompting guide (covers Claude Fable 5.1, Mythos 5.1, Opus 5.5, Opus 4.6-4.8, Sonnet 4.6-5.5, Haiku 4.5) lists "Manual chain-of-thought (CoT) prompting as a fallback. When thinking is off, you can still encourage step-by-step reasoning..." and says on Opus 5 to "prefer keeping thinking enabled at a lower effort level instead" because with thinking disabled the model "can occasionally emit internal XML tags into its visible output" — [Anthropic prompting best practices](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices) (fetched 2026-09-29).
- Same page: "On Claude Fable 5.1, Claude Mythos 5.1, Claude Fable 5, Claude Mythos 5, and Claude Opus 5.5, thinking is always on and adaptive thinking is the only mode... In internal evaluations, adaptive thinking reliably drives better performance than extended thinking." Manual `budget_tokens` "is deprecated" on 4.6 and "On Claude 4.7 and later models, setting `budget_tokens` returns a 400 error." — [Anthropic prompting best practices](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices).
- Same page: "With adaptive thinking and subagent orchestration, Claude handles most multistep reasoning internally. Explicit prompt chaining... is still useful when you need to inspect intermediate outputs or enforce a specific pipeline structure. The most common chaining pattern is self-correction: generate a draft → have Claude review it against criteria → have Claude refine" — [Anthropic prompting best practices](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices).
- Same page: prefilled assistant responses "are no longer supported" starting with Claude 4.6 models; "Model intelligence and instruction following have advanced such that most use cases of prefill no longer require it." — [Anthropic prompting best practices](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices).
- Same page documents a new failure mode of native reasoners, "Overthinking and excessive thoroughness" (Opus 4.6 "may think extensively, which can inflate thinking tokens"), and recommends lowering `effort` or adding a "choose an approach and commit to it" instruction — [Anthropic prompting best practices](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices).
- Anthropic's steering page: "Claude's thinking is adaptive: the model evaluates each request and decides for itself whether to think and how much"; effort levels `low`/`medium`/`high`/`xhigh`/`max`; per-message steering phrases like "Please think hard before responding." are recommended for agent harnesses on planning steps — [Steering thinking](https://platform.claude.com/docs/en/build-with-claude/thinking-steering-and-cost) (fetched 2026-09-29).
- Practitioner framing (2026): CoT "is built into the reasoning modes of GPT-5, Claude Opus 4.7 extended thinking, Gemini 3 Pro deep think, and DeepSeek R1. The job has shifted from teaching the model to think to deciding when to spend reasoning tokens"; few-shot CoT "still help[s] small or medium models in 2026" — [FutureAGI CoT guide](https://futureagi.com/blog/chain-of-thought-prompting-ai-2025/) (snippet-level; page blocked).
- A 2026 OpenAI-affiliated study finds reasoning models' "CoT controllability [is] generally low (mostly below 10%)" — i.e., the model's thinking trace cannot be reliably steered by instruction, which limits scaffold designs that assume prompt-controllable reasoning — [Reasoning Models Struggle to Control their Chains of Thought (arXiv 2603.05706)](https://arxiv.org/html/2603.05706v1) (snippet-level).

Self-consistency / parallel sampling:
- Self-consistency still works but is extremely expensive on native reasoners: "improving pass@1 accuracy from 68% to 82% using standard majority voting on AIME 2025 requires 511 additional reasoning traces per question using Qwen3-8B, consuming 100 million additional tokens" — [Deep Think with Confidence (arXiv 2508.15260)](https://arxiv.org/pdf/2508.15260) (snippet-level).
- "The Sequential Edge" (arXiv 2511.02309, Nov 2025): across 5 open-source models and 3 reasoning benchmarks, "sequential scaling where chains explicitly build upon previous attempts consistently outperforms the dominant parallel self-consistency paradigm in 95.6% of configurations with gains in accuracy up to 46.7%"; introduces training-free inverse-entropy weighted voting — [arXiv abs](https://arxiv.org/abs/2511.02309); [OpenReview](https://openreview.net/forum?id=ZqiCAEQ4Sx) (snippet-level).
- Counter-evidence for small models: "When Self-Consistency Backfires: Majority Vote Hurts the Majority of Hard Science Problems for Small LLMs" (arXiv 2608.11403, Aug 2026) — [listing](https://awesomepapers.io/llm-papers/papers/2608.11403) (title-level only; content not fetched).
- "On the Overscaling Curse of Parallel Thinking: System Efficacy Contradicts Sample Efficiency" (arXiv 2601.21619, Jan 2026) — [arXiv](https://arxiv.org/pdf/2601.21619) (title-level).
- Adaptive/parallel reasoning is an active 2026 research direction: BAIR blog "Adaptive Parallel Reasoning: The Next Paradigm in Efficient Inference Scaling" (2026-05-08) — [BAIR](https://bair.berkeley.edu/blog/2026/05/08/adaptive-parallel-reasoning/) (page blocked; title/date only); Google's Gemini "leveraged parallel thinking to excel at the International Mathematical Olympiad" — [Parallel-Probe (arXiv 2602.03845)](https://arxiv.org/html/2602.03845v2) (snippet-level).
- Efficiency-focused test-time-scaling papers dominate 2026: FineVerify (2606.00660), "Do Not Waste Your Rollouts" (2601.21684), Temporal Reasoning Aggregation (2604.17304), ThinkBooster (2606.06915), Funnel of Thoughts (2608.15065), TMAS multi-agent synergy (2605.10344) — all listed in [search results](https://arxiv.org/html/2512.02008v1) (titles only).
- Survey: "The Art of Scaling Test-Time Compute for Large Language Models" (arXiv 2512.02008, Dec 2025) and "A survey on test-time scaling in large language models: What, how, where, and how well?" (2025) — [arXiv](https://arxiv.org/html/2512.02008v1) (content blocked; not read).

Self-refine / self-correction:
- "LARGE LANGUAGE MODELS CANNOT SELF-CORRECT REASONING YET" (arXiv 2310.01798) established that intrinsic self-correction without external feedback does not improve reasoning — [arXiv](https://arxiv.org/pdf/2310.01798).
- For native reasoners, a 2025 study reports DeepSeek-R1 "repeatedly fixes only what it initially corrected... both reasoning token counts and self-refinement performance consistently decline after the initial turn, with token counts dropping by 69.7%" — [search summary citing RefineBench / related (arXiv 2511.22173)](https://arxiv.org/pdf/2511.22173) (snippet-level; attribution of the 69.7% figure to a specific paper not verified).
- ICLR 2025 "Training Language Models to Self-Correct via RL" (SCoRe) moved self-correction into training, not inference — [ICLR proceedings](https://proceedings.iclr.cc/paper_files/paper/2025/file/871ac99fdc5282d0301934d23945ebaa-Paper-Conference.pdf).
- Reference implementation madaan/self-refine last pushed 2024-10-04 (GitHub API, 2026-09-29).

Tree / Graph of Thoughts:
- princeton-nlp/tree-of-thought-llm (6,073 stars) last push 2025-01-16; spcl/graph-of-thoughts (2,841 stars) last push 2026-03-24 (GitHub API, 2026-09-29). Original ToT reported 74% on Game of 24 vs 4% for GPT-4 CoT (NeurIPS 2023; from repo description/date, prior knowledge — not re-verified this session).

Process reward models / verifier-guided search:
- Qwen2.5-Math-PRM-7B/72B (Jan 2025): evaluated with best-of-8 sampling from Qwen2.5-Math-7B-Instruct on GSM8K, MATH, Minerva, GaoKao, OlympiadBench, College Math, MMLU-STEM; "Qwen2.5-Math-PRM-7B outperforms GPT-4o-0806" as a verifier on ProcessBench — [Qwen blog](https://qwen.ai/blog?id=qwen2.5-math-prm) (snippet-level).
- DeepSeek-R1 paper: "Prior works have explored process-based reward models, reinforcement learning, and search algorithms such as Monte Carlo Tree Search and Beam Search, but none of these methods has achieved general reasoning performance comparable to OpenAI's o1 series models" — [DeepSeek-R1 (arXiv 2501.12948)](https://arxiv.org/html/2501.12948v1).
- "Limits of PRM-Guided Tree Search for Mathematical Reasoning with LLMs" (arXiv 2510.20272, Oct 2025) — [arXiv](https://arxiv.org/pdf/2510.20272) (title-level).
- Generative PRMs ("Process Reward Models That Think", ThinkPRM-1.5B) "outperform discriminative PRMs and... MathShepherd-7B and RLHFFlow-8B" in beam search — [alphaXiv overview 2504.16828](https://www.alphaxiv.org/overview/2504.16828v5) (snippet-level). ICML 2026 "Process Reward Agents" turns the PRM into an online agent; Qwen3-4B reaches 81.9% on MedQA with beam search — [papernotes](https://en.papernotes.org/ICML2026/llm_agent/process_reward_agents_for_steering_knowledge-intensive_reasoning/) (secondary).
- OpenR (PRM + search framework) last push 2025-01-17 (GitHub API, 2026-09-29); the maintained resource is the Awesome-PRM list (push 2026-09-13).

Program-aided reasoning:
- reasoning-machines/pal last push 2023-06-30 (GitHub API). The pattern survives as built-in code execution / "agents that think in code" (smolagents CodeAgent, description "a barebones library for agents that think in code" — GitHub API) rather than as a standalone technique.

Prompt/program compilers:
- DSPy: 38,411 stars, MIT, pushed 2026-09-28 (GitHub API). Optimizers in 2026: BootstrapFewShot, MIPROv2, COPRO, GEPA — [FutureAGI DSPy optimizers](https://futureagi.com/blog/dspy-optimizers-explained/) (snippet-level).
- GEPA ("Reflective Prompt Evolution Can Outperform Reinforcement Learning", Agrawal et al. 2025, ICLR 2026 oral): "beats GRPO by 10% on average (up to 20%) with 35x fewer rollouts"; "beats MIPROv2 on every benchmark and model, with aggregate gains of +14% versus MIPROv2's +7%" and prompts "up to 9.2x shorter" — [Morph GEPA summary](https://www.morphllm.com/gepa-prompt-optimization) (secondary, snippet-level).
- GEPA README (fetched 2026-09-29): MIT; "35x faster than RL" (100–500 evaluations vs 5,000–25,000+ for GRPO); DSPy adapter "67% → 93%" on MATH; ARC-AGI agent "32% → 89%" via architecture discovery; 2026 adopters listed include Microsoft AI (MAI-Thinking-1 prompt filtering), Nubank, and Google's Gemini Enterprise Agent Platform `adk optimize` — [gepa-ai/gepa](https://github.com/gepa-ai/gepa). Note these are self-reported by the project.

### Inferences
- The "obsolete" list for frontier native reasoners is: manual CoT prompting (documented as fallback-only by Anthropic), assistant prefill (removed from the API), fixed thinking budgets (400 error on 4.7+), hand-rolled ToT/GoT search (reference repos dormant since Jan 2025), and PRM-guided beam/MCTS as a general-reasoning strategy (DeepSeek-R1 paper; "Limits of PRM-guided tree search"). None of these has a 2026 result showing gains on a frontier model.
- The "still works, but pay for it" list is self-consistency / parallel sampling (large gains on hard math at 100x+ token cost) and multi-sample best-of-N with a verifier in narrow domains (math, medicine).
- The techniques with growing 2026 evidence are sequential refinement with entropy weighting (95.6% of configs), adaptive thinking (vendor-reported), and offline scaffold optimization (GEPA/DSPy with 10–20 point self-reported deltas).
- Anthropic's own "self-correction" chaining pattern (draft → review against criteria → refine) is the surviving form of Self-Refine: it works because the review step has explicit criteria and a separate call, not because the model spontaneously self-corrects.

### Gaps
- No single 2026 controlled study was found that runs self-consistency, ToT, Reflexion, debate and PRM search head-to-head on a current frontier API model (Claude Opus 5.x, GPT-5, Gemini 3); the budget-matched studies use open-weight Qwen3/DeepSeek/Gemini 2.5.
- The full text of the test-time-scaling survey (2512.02008) and the parallel-thinking papers could not be fetched (arxiv/huggingface/alphaxiv/semanticscholar/awesomepapers all blocked), so their benchmark tables are not reproduced here.
- Anthropic's "adaptive thinking reliably drives better performance than extended thinking" is an internal-eval claim with no published numbers.

## Key Question 2: Which agent frameworks are the most used and best maintained in 2026 for building a reasoning agent on Claude or another frontier model?

### Takeaway
By stars and commit recency (2026-09-29) the actively maintained, general-purpose choices are CrewAI (59k), LangGraph (42k), OpenAI Agents SDK (30k), smolagents (30k), Mastra (28k, TS), Letta (25k), Google ADK (22k), Pydantic AI (20k), Microsoft Agent Framework (14k) and the Claude Agent SDK (8k Python, wrapping the 149k-star Claude Code harness). AutoGen (61k) is in maintenance mode since 2025-10-02; its successors are Microsoft Agent Framework (1.0 on 2026-04-03) and the community fork AG2.

### Cited Findings
- Star/license/push data for every framework: see table above — GitHub API via MCP, 2026-09-29.
- AutoGen: "Microsoft placed AutoGen in maintenance mode on October 2, 2025. AutoGen receives critical bug fixes and security patches, no new features, and is community managed going forward" — [Atlan AutoGen status](https://atlan.com/know/ai-agent/what-is-autogen/) (snippet-level; page blocked). GitHub API confirms last push 2026-04-15 and 1,110 open issues.
- Microsoft Agent Framework "merges AutoGen's simple agent abstractions with Semantic Kernel's enterprise-grade features... reached 1.0 on April 3, 2026" — [Atlan MAF](https://atlan.com/know/ai-agent/microsoft/agent-framework/) (snippet-level); lineage write-up [Bevilacqua, 2026-06-18](https://alexbevi.com/blog/2026/06/18/two-lineages-one-framework-how-autogen-and-semantic-kernel-became-the-microsoft-agent-framework/).
- AG2: "When AutoGen's original creators Chi Wang and Qingyun Wu left Microsoft in November 2024, they forked the repository and relaunched it as AG2 under the ag2ai GitHub organization, preserving the original 0.2 API surface" — [Atlan](https://atlan.com/know/ai-agent/what-is-autogen/) (snippet-level). GitHub API: 4,968 stars, Apache-2.0, pushed 2026-09-28, 40 open issues.
- CrewAI: "crossed 44,600 GitHub stars and shipped v1.10.1 with native MCP and A2A support" (earlier 2026 figure; GitHub API now shows 59,158) — [Agentmelt comparison](https://agentmelt.com/blog/ai-agent-frameworks-compared-2026/) (snippet-level).
- LangGraph: "leads in enterprise adoption with 34.5M monthly downloads"; "Klarna runs it at 85 million users, and benchmarks show 47% lower token costs than CrewAI due to explicit edge transitions instead of LLM-driven task routing" — [Let's Data Science comparison](https://letsdatascience.com/blog/ai-agent-frameworks-compared) (snippet-level, vendor-adjacent claims; methodology not verified).
- OpenAI Agents SDK: "v0.10.2... works with 100+ non-OpenAI models"; primitives are Agents, Tools, Handoffs, Guardrails, Sessions, Tracing — [Morph comparison](https://www.morphllm.com/ai-agent-framework) (snippet-level); [OpenAI Agents SDK docs](https://openai.github.io/openai-agents-python/). One search summary said the SDK "was released as an open-source framework in early 2026"; this conflicts with the GitHub repo creation date 2025-03-11 (GitHub API) and OpenAI's March 2025 announcement [New tools for building agents](https://openai.com/index/new-tools-for-building-agents/); treat the 2026 date as wrong.
- Claude Agent SDK: "v0.1.48"; "owns MCP-native development with its in-process server model and lifecycle hooks" — [Morph comparison](https://www.morphllm.com/ai-agent-framework) (snippet-level). Docs: subagents "are separate agent instances that your main agent can spawn to handle focused subtasks... isolate context... run multiple analyses in parallel"; a subagent "inherits the main session's extended thinking configuration" — [Subagents in the SDK](https://platform.claude.com/docs/en/agent-sdk/subagents) (snippet-level). An open feature request (#14321) asks to enable extended thinking for subagents independently — [anthropics/claude-code issue 14321](https://github.com/anthropics/claude-code/issues/14321).
- Anthropic on reasoning scaffolds inside the SDK: "Claude's latest models orchestrate subagents natively... do so proactively without requiring explicit instruction"; "Claude Opus 4.6 has a strong predilection for subagents and may spawn them in situations where a simpler, direct approach would suffice... Claude Opus 5 also delegates to subagents more readily" — [Anthropic prompting best practices](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices).
- Anthropic hooks vs prompts: "hooks enforce behavior architecturally — a hook that blocks a tool call cannot be reasoned around" — [Boringbot write-up](https://boringbot.substack.com/p/claude-code-skills-subagents-hooks) (secondary).
- smolagents: "By mid-2026, the project had accumulated over twenty-seven thousand stars... reached version 1.26.0"; Apache-2.0 — [Learn AI wiki](https://ai.miraheze.org/wiki/Smolagents) (secondary). GitHub API: 29,576 stars, pushed 2026-09-23.
- Letta: "24.7k stars with an Apache-2.0 license. The current source code lives in letta-ai/letta-code, which includes the agent harness, interactive terminal UI, App Server" — [Letta org](https://github.com/letta-ai) / [star-history](https://www.star-history.com/letta-ai/letta/). GitHub API: letta 24,966 stars (0 open issues, last push 2026-09-10); letta-code 3,479 stars, pushed 2026-09-29.
- Mastra: "over 24,000 GitHub stars... @mastra/core@1.35.0, released on May 15, 2026... Apache 2.0 license, with enterprise features being source-available under the Mastra Enterprise License" — [Mastra](https://mastra.ai/); GitHub API: 28,411 stars.
- Pydantic AI: "20.2k GitHub stars (as of... September 25, 2026)... MIT" — [pydantic-ai releases](https://github.com/pydantic/pydantic-ai/releases); GitHub API: 20,251.
- Google ADK: GitHub API 21,675 stars, Apache-2.0, pushed 2026-09-29; `adk optimize` integrates GEPA — [gepa README](https://github.com/gepa-ai/gepa).
- Dify (low-code) "leads overall GitHub stars with 144k" — [Let's Data Science](https://letsdatascience.com/blog/ai-agent-frameworks-compared) (snippet-level; not verified via API).
- Practitioner consensus on positioning: "vendor SDKs for single-provider agents, LangGraph for production state management, CrewAI for rapid multi-agent prototyping" — [Morph comparison](https://www.morphllm.com/ai-agent-framework) (snippet-level).

### Inferences
- For a reasoning agent on Claude specifically, the Claude Agent SDK is the only framework whose reasoning scaffold (adaptive/interleaved thinking, native subagent spawning, hooks) is co-designed with the model; its relatively low star count (8k) understates use because most adoption runs through Claude Code (149k stars).
- LangGraph, OpenAI Agents SDK and Pydantic AI are the safest model-agnostic choices on maintenance signals (daily pushes, MIT). AutoGen should not be started on; AG2 is small (5k) but well-triaged (40 open issues).
- 2026 entrants worth naming: Microsoft Agent Framework 1.0 (Apr 2026), Letta Code (Oct 2025 repo, now Letta's main harness), and Mastra 1.x for TypeScript.

### Gaps
- Download counts (PyPI/npm) could not be independently verified this session; only the 34.5M/month LangGraph figure from a secondary source was found.
- No published benchmark compares reasoning accuracy of the same model across frameworks; framework "benchmarks" found are token-cost comparisons from vendor-adjacent blogs.
- Claude Agent SDK's exact version and the claude-code license field were not returned by the API query.

## Key Question 3: Are there open-source projects specifically aimed at simulating human-like reasoning (deliberation, dual-process, metacognition, self-verification) rather than task accuracy?

### Takeaway
There is an active 2025–2026 research literature (metacognition surveys, Flavell-based monitoring, Bayesian meta-reasoning, cognitive-architecture hybrids) but the open-source code is small, academic and mostly dormant; the only widely used "deliberation" scaffold is Karpathy's llm-council pattern, which targets answer quality rather than cognitive fidelity.

### Cited Findings
- yale-nlp/LLM-Metacognition: "Metacognition in LLMs: Foundations, Progress, and Opportunities" (survey, arXiv 2607.11881, July 2026); includes "Decoupling Metacognition from Cognition: A Framework for Quantifying Metacognitive Ability in LLMs" and "Reinforcement Learning with Metacognitive Feedback Elicits Faithful Uncertainty Expression" — [repo](https://github.com/yale-nlp/LLM-Metacognition); GitHub API: 70 stars, MIT, created 2026-05-16, pushed 2026-07-19.
- "Before you <think>, monitor: Implementing Flavell's metacognitive framework in LLMs" (arXiv 2510.16374, Oct 2025) — [arXiv](https://arxiv.org/pdf/2510.16374) (title-level).
- "Metacognition as Reward: Reinforcing LLM Reasoning via Knowledge and Regulation Signals" (arXiv 2605.23384) and "Metacognition Should Be the Scientific Framework for Bounded and Effective Self-Governance in Generative AI" (arXiv 2605.23981), both May 2026 — [search listing](https://www.emergentmind.com/topics/metacognition-driven-llm-frameworks-a347e2cd-1f75-4970-88af-3ba283adf3de) (title-level).
- hanqi-qi/LLM_MetaReasoning: "proposes a Bayesian meta-reasoning framework that equips an LLM with four interacting modules" — [repo](https://github.com/hanqi-qi/LLM_MetaReasoning); GitHub API: 16 stars, no license, pushed 2025-07-29.
- xiaoyanLi629/dual-process-llm: "Investigating Dual Process Theory (System 1 vs System 2 thinking) in Large Language Models... targets IEEE BIBM 2026... 2x2x2 factorial ablation isolating model size, temperature, and prompting strategy" — [repo](https://github.com/xiaoyanLi629/dual-process-llm); GitHub API: 0 stars, MIT, created 2026-09-24 (brand new, unreviewed).
- open-thought/system-2-research: "System 2 Reasoning Link Collection" — [repo](https://github.com/open-thought/system-2-research); GitHub API: 873 stars, Apache-2.0, last push 2025-03-16 (stale).
- Cognitive-architecture hybrids: "Classical cognitive architectures such as ACT-R and SOAR were pioneered to simulate human cognition through production rules and symbolic memory structures. More recent efforts have sought to integrate Large Language Models into these frameworks, creating hybrid neurosymbolic agents" — [MIRROR (arXiv 2506.00430)](https://arxiv.org/pdf/2506.00430) (snippet-level); "Cognitive LLMs: Towards Integrating Cognitive Architectures and LLMs" (arXiv 2408.09176); NL2GenSym for SOAR (arXiv 2510.09355); "Simulating Human Cognition: Heartbeat-Driven Autonomous Thinking Activity Scheduling" (arXiv 2604.14178, Apr 2026) which "simulate[s] key cognitive activities (e.g., planning, dreaming, reflecting) driven by a lightweight heartbeat mechanism" — [arXiv](https://arxiv.org/pdf/2604.14178) (snippet-level).
- karpathy/llm-council: "a 3-stage deliberation system... Stage 1: the user query is given to all LLMs individually... Stage 2: anonymized peer review... Stage 3: a chairman model produces a final unified response"; "In early experiments, the council often produced results that were stronger than the best individual model acting alone" — [karpathy/llm-council](https://github.com/karpathy/llm-council) (snippet-level, no benchmark). Derivative projects: [LLM-Council-Grounded](https://github.com/danielrosehill/LLM-Council-Grounded), [llm-council-governance](https://github.com/andybhall/llm-council-governance), [Awesome-LLM-Council-Projects](https://github.com/danielrosehill/LLM-Council-Projects).
- Letta positions itself as "Stateful agents that are like people, with memory, identity, and the ability to learn and adapt" (repo description, GitHub API 2026-09-29) — a human-likeness framing centered on memory rather than reasoning process.
- Reflexion (episodic self-reflection memory, "verbal reinforcement learning") remains the canonical open-source metacognitive-loop reference; repo dormant since 2025-01-14 (GitHub API).

### Inferences
- No maintained open-source project was found whose stated goal is faithful simulation of human deliberation (dual-process switching, confidence monitoring, regulation) with a reusable code API; the material exists as papers plus small evaluation repos. A skills-based reasoning toolkit would be building in largely empty space.
- The closest maintained scaffolds for "deliberation" are council/debate patterns (llm-council, M3MAD-Bench) and Letta's memory-centric "agents like people"; the closest for "metacognition" is the model's own adaptive thinking plus effort control, which vendors now expose as API parameters rather than as open frameworks.

### Gaps
- Star counts for karpathy/llm-council and the cognitive-architecture repos were not retrieved (not included in the API batch).
- No benchmark evidence exists (that I could find) that any of the metacognition/dual-process projects improves reasoning accuracy over native thinking; their papers measure calibration, uncertainty expression, or controllability.
- ACT-R/Soar+LLM hybrids: no 2026 GitHub repo with meaningful adoption was identified.

## Key Question 4: What does the evidence say about multi-agent debate or council patterns versus a single strong model with extended thinking?

### Takeaway
Budget-controlled 2026 evidence says a single agent with the same thinking-token budget matches or beats debate, ensemble, sequential and parallel-roles multi-agent systems on multi-hop reasoning, and M3MAD-Bench finds debate gains are uneven and costly; the documented exceptions are breadth-first/parallelizable tasks (Anthropic's 90.2% research-eval gain, attributed 80% to extra tokens) and multimodal inputs.

### Cited Findings
- "Single-Agent LLMs Outperform Multi-Agent Systems on Multi-Hop Reasoning Under Equal Thinking Token Budgets" (arXiv 2604.02460, Apr 2026): across FRAMES (824 multi-hop questions) and MuSiQue (4-hop), three model families (Qwen3-30B, DeepSeek-R1-Distill-Llama-70B, Gemini 2.5) and five architectures (Sequential, Debate, Ensemble, Parallel-roles, Subtask-parallel), "single-agent systems match or outperform multi-agent systems when computation is normalized"; "many reported multi-agent gains are better explained by compute and context effects than by inherent architectural superiority"; budgets swept from 100 to 10,000 thinking tokens; on MuSiQue SAS is best or statistically indistinguishable "in all but the lowest budget (100 tokens)"; theoretical argument via Data Processing Inequality that decomposition adds communication bottlenecks — [arXiv html](https://arxiv.org/html/2604.02460v1) (blocked; snippet-level); [ResearchGate](https://www.researchgate.net/publication/403529711_Single-Agent_LLMs_Outperform_Multi-Agent_Systems_on_Multi-Hop_Reasoning_Under_Equal_Thinking_Token_Budgets); [technical review, Zhou 2026-05-18](https://www.zhongzhuzhou.org/blog/2026-05-18-singlevsmultiagent-technical-review-en/).
- The same paper notes MAS "can be advantageous specifically when a single agent's effective context utilization is degraded (e.g., due to long or noisy contexts), or when MAS benefit from additional unaccounted computation" — [Zhou review](https://www.zhongzhuzhou.org/blog/2026-05-18-singlevsmultiagent-technical-review-en/) (secondary).
- M3MAD-Bench (ACM Multimedia 2026; 5 domains, 13 datasets, 7 text + 6 multimodal; methods Div-MAD, DMAD, LLM-Debate, CoT, IO, Self-Consistency): "MAD is not uniformly effective: collaborative methods are generally more robust than adversarial ones... but often incur substantial efficiency costs"; "LLM Debate consistently achieved the highest average accuracy across most base models"; "Div-MAD, an adversarial approach, often underperformed even single-agent baselines, particularly with weaker base models"; heterogeneous model mixes "did not consistently yield substantial performance leaps"; multi-perspective benefit "is minimal or even negative in unimodal tasks" — [arXiv 2601.02854](https://arxiv.org/abs/2601.02854) (snippet-level); [repo](https://github.com/liaolea/M3MAD-Bench) (fetched; README gives scope but no numbers).
- A 2025 heterogeneous-debate study found debate "does not always guarantee improvement — when all roles... are assigned to Pixtral, performance drops below that of single-agent Pixtral on both MathVision and RealWorldQA" — [Springer, JKSU-CIS 2025](https://link.springer.com/article/10.1007/s44443-025-00353-3) (snippet-level).
- "Beyond the Strongest LLM: Multi-Turn Multi-Agent Orchestration vs. Single LLMs on Benchmarks" (arXiv 2509.23537, Sep 2025) — [arXiv](https://arxiv.org/pdf/2509.23537) (title-level).
- Anthropic (2025-06-13): "a multi-agent system with Claude Opus 4 as the lead agent and Claude Sonnet 4 subagents outperformed single-agent Claude Opus 4 by 90.2% on our internal research eval"; on BrowseComp "token usage by itself explains 80% of the variance, with the number of tool calls and the model choice as the two other explanatory factors"; agents use "about 4× more tokens than chat interactions, and multi-agent systems use about 15× more tokens than chats"; multi-agent excels at "heavy parallelization, information that exceeds single context windows, and interfacing with numerous complex tools" and is poor "for domains requiring all agents to share the same context or involving many interdependencies"; subagents use interleaved thinking after tool results — [Anthropic engineering](https://www.anthropic.com/engineering/multi-agent-research-system) (fetched 2026-09-29).
- Anthropic (2026-01-23): "we've seen teams invest months building elaborate multi-agent architectures only to discover that improved prompting on a single agent achieved equivalent results"; multi-agent justified only for context protection, parallelization, or specialization; "multi-agent implementations typically use 3-10x more tokens than single-agent approaches for equivalent tasks" — [claude.com blog](https://claude.com/blog/building-multi-agent-systems-when-and-how-to-use-them) (fetched 2026-09-29).
- LangChain's parallel guidance "How and when to build multi-agent systems" — [LangChain blog](https://www.langchain.com/blog/how-and-when-to-build-multi-agent-systems) (not fetched).
- 2026 debate research is now about fixing debate's failure modes rather than showing raw gains: "Dynamic Role Assignment for Multi-Agent Debate" (2601.17152), "CortexDebate: Debating Sparsely and Equally" (2507.03928), "Creative Generation via Multi-Agent Debate: Does Debate Suppress Diversity?" (2609.00683, Sep 2026) — [search listing](https://arxiv.org/pdf/2609.00683) (titles only).
- Multi-agent debate did win a 2026 competition in a multimodal setting: "Multi-Agent Debate and Visual Information Extraction for SeePhys Pro: A 1st-Place Technical Report from ICML 2026 AI4Math Track 3" (arXiv 2607.21946) — [arXiv](https://arxiv.org/pdf/2607.21946) (title-level).
- Reference debate repos are dormant: composable-models/llm_multiagent_debate last push 2025-04-24; Skytliang/Multi-Agents-Debate last push 2025-12-16 (GitHub API, 2026-09-29).

### Inferences
- The two lines of evidence are consistent: multi-agent gains are real when they buy more total tokens, more parallel context, or genuinely different input modalities; when compute is equalized and the task is single-context reasoning, the strong single reasoner wins or ties. A council/debate pattern should therefore be justified by context isolation or breadth, not by "wisdom of crowds" on reasoning per se.
- Adversarial debate (Div-MAD style) is the riskiest variant; collaborative "LLM-Debate" (Du et al.) is the most robust, but at multiples of the cost.
- For a Claude-based reasoning simulator, the cheapest defensible pattern is a single adaptive-thinking agent, escalating to subagents only for breadth-first research or when context is noisy, matching Anthropic's own 2026 guidance.

### Gaps
- No public study compares a debate/council of frontier models (e.g., Claude Opus 5.5 + GPT-5 + Gemini 3) against a single one of them at `max` effort; the equal-budget paper used open-weight and Gemini 2.5 models only.
- Anthropic's 90.2% figure is on an internal eval without a public dataset; the 2026 claude.com post gives no numbers.
- M3MAD-Bench's per-dataset accuracy and token-cost tables could not be retrieved (arxiv blocked; README omits numbers).
