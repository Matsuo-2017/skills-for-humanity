# Systems That Explicitly Simulate Human Reasoning and Cognition (state as of 2026-09-29)

Scope note: This survey covers (1) cognitive architectures, (2) foundation models of cognition trained on behavioural data, (3) LLM-based human simulators / digital twins, and (4) evidence on how closely LLM reasoning matches human reasoning. General LLM benchmarks and agent frameworks are excluded per assignment.

Access note (important for the writer): during this research the egress proxy blocked arxiv.org, nature.com, science.org, huggingface.co, pmc.ncbi.nlm.nih.gov, alphaxiv.org, wikipedia.org, act-r.psy.cmu.edu, helmholtz-munich.de, techxplore.com, and ccrg.cs.memphis.edu. GitHub pages were fetched directly. Anything sourced from those blocked hosts below comes from search-result summaries of the page, not from a full-text read, and is tagged "[from search summary]". Items I could not confirm at all are tagged "[UNVERIFIED]".

---

## Key Question 1: Which system currently best predicts or reproduces human reasoning behaviour, and on what evidence?

### Takeaway
As of September 2026, the strongest quantitative evidence for *trial-by-trial* prediction of human behaviour in psychology experiments belongs to the Centaur family (Helmholtz Munich; Llama-3.1-70B fine-tuned on Psych-101), which beat domain-specific cognitive models on 159 of 160 experiments and generalised to held-out tasks; but the claim that it "simulates cognition" is contested by multiple 2025-2026 critiques showing brittleness and no process-level insight. For *individual-level* prediction of survey/attitude responses, Stanford's interview-based generative agents (85% of test-retest reliability on the GSS) remain the reference point, while 2026 work shows LLM digital twins reproduce averages but carry little individual-level signal.

### Cited Findings

**Centaur (Binz et al., Nature 2025) — the current benchmark for behavioural prediction**
- Centaur is "a computational model that can predict and simulate human behaviour in any experiment expressible in natural language", derived by fine-tuning a language model on Psych-101; published in Nature Vol. 644 (28 Aug 2025 issue; online 2 July 2025 per Helmholtz news search summary) — [Nature](https://www.nature.com/articles/s41586-025-09215-4) [from search summary]; [arXiv 2410.20268](https://arxiv.org/abs/2410.20268); [Helmholtz Munich news](https://www.helmholtz-munich.de/en/newsroom/news-all/artikel/ai-that-thinks-like-us-and-could-help-explain-how-we-think) [from search summary].
- Psych-101 covers trial-by-trial data from >60,000 participants making >10,000,000 choices in 160 experiments (multi-armed bandits, decision-making, memory, supervised learning, Markov decision processes) — [Nature](https://www.nature.com/articles/s41586-025-09215-4) [from search summary].
- Centaur outperforms domain-specific cognitive models in all but one of the 160 experiments; average negative log-likelihood difference of 0.13 vs cognitive models (cognitive-model NLL 0.56) — [Nature](https://www.nature.com/articles/s41586-025-09215-4) [from search summary].
- Centaur "captures the behaviour of held-out participants better than existing cognitive models" and "generalizes to previously unseen cover stories, structural task modifications and entirely new domains" — [Nature](https://www.nature.com/articles/s41586-025-09215-4) [from search summary].
- Centaur also "predicts reaction times with surprising precision" and its internal representations became more aligned with human neural activity after fine-tuning (fMRI alignment claim) — [Helmholtz Munich news](https://www.helmholtz-munich.de/en/newsroom/news-all/artikel/ai-that-thinks-like-us-and-could-help-explain-how-we-think) [from search summary]; [TechXplore, July 2025](https://techxplore.com/news/2025-07-centaur-ai.html) [from search summary]. Exact fMRI alignment numbers could not be read (Nature full text blocked).
- Weights: [marcelbinz/Llama-3.1-Centaur-70B](https://huggingface.co/marcelbinz/Llama-3.1-Centaur-70B) and the [LoRA adapter](https://huggingface.co/marcelbinz/Llama-3.1-Centaur-70B-adapter) on Hugging Face, license "llama3.1" (i.e., Meta Llama 3.1 Community License) — [from search summary]. Code: [github.com/marcelbinz/Llama-3.1-Centaur-70B](https://github.com/marcelbinz/Llama-3.1-Centaur-70B); earlier project [github.com/marcelbinz/CENTaUR](https://github.com/marcelbinz/CENTaUR).
- Training data: [marcelbinz/Psych-101](https://huggingface.co/marcelbinz/Psych-101) (training) and Psych-101-test (46 held-out tasks); the test set is gated and released under CC-BY-ND-4.0 — per the [socius-org/Centauri README](https://github.com/socius-org/Centauri) [from search summary of that README].

**Critiques of Centaur's fidelity claims (2025-2026)**
- Science (AAAS) news piece "Researchers claim their AI model simulates the human mind. Others are skeptical": Jeffrey Bowers (Bristol) argues Centaur "can't explain anything about human cognition" (analog vs digital clock analogy); Federico Adolfi (Ernst Strüngmann Institute, Max Planck Society) says stringent tests will show the model is "very easy to break" and that 160 experiments is "a grain of sand in the infinite pool of cognition" — [Science](https://www.science.org/content/article/researchers-claim-their-ai-model-simulates-human-mind-others-are-skeptical) [from search summary].
- Bowers reports subjecting Centaur to two experimental manipulations in which it "failed dramatically, in ways that show that Centaur's predictions are completely unrelated to the processes that drive human responses" — [Bowers, Bluesky post](https://bsky.app/profile/jeffreybowers.bsky.social/post/3lsjxpcfetv2n) [from search summary]. Preprint: "Centaur: A model without a theory" (PsyArXiv v9w37) — [Sciety listing](https://labs.sciety.org/articles/by?article_doi=10.31234%2Fosf.io%2Fv9w37_v1) [blocked; existence confirmed via search only].
- "'Captured' by Centaur: Opaque predictions or process insights?" — commentary in Journal of Experimental Psychology: Animal Learning and Cognition (2026), doi 10.1037/xan0000410; argues Centaur is "brittle and sensitive to small variations in task input, and their internal representations often remain opaque" — [PubMed 41021501](https://pubmed.ncbi.nlm.nih.gov/41021501/); [APA PsycNet](https://psycnet.apa.org/doiLanding?doi=10.1037%2Fxan0000410) [from search summary].
- "Can Centaur truly simulate human cognition?" (National Science Open, 2026) raises the "behaviourist trap": behavioural equivalence classes are large, so matching input-output does not imply shared mechanism; concludes Centaur is "a high-coverage behavioral emulator for tasks encoded in natural language", not the same competence type as biological cognition; also notes Centaur does not simulate timing dynamics, attention, physical interaction, or social settings — [NSO 2026](https://www.nso-journal.org/articles/nso/pdf/2026/01/NSO20250053.pdf) [from search summary].
- "Not Even Wrong: On the Limits of Prediction as Explanation in Cognitive Science" (arXiv 2510.03311, Oct 2025) and "Taming the Centaur(s) with LAPITHS" (arXiv 2604.27927, Apr 2026) are further methodological critiques of prediction-as-explanation — [arXiv 2510.03311](https://arxiv.org/pdf/2510.03311); [arXiv 2604.27927](https://arxiv.org/html/2604.27927v2) [from search summary; not read].
- Response/agenda from the modelling side: "Addressing longstanding challenges in cognitive science with language models" (Trends in Cognitive Sciences, 2026; arXiv 2511.00206) — [ScienceDirect](https://www.sciencedirect.com/science/article/pii/S1364661326001580); [arXiv](https://arxiv.org/html/2511.00206v3) [from search summary; authorship not confirmed].

**Successors: Psych-201, "Centauri" small models, and post-training findings (2026)**
- Psych-201: open-collaboration successor dataset (GitHub, Apache-2.0, 416 commits, 100+ experiments, optional reaction-time, age, clinical-diagnosis and nationality fields; contributions via pull request with lightweight peer review; 32K-token limit per participant transcript) — [github.com/marcelbinz/Psych-201](https://github.com/marcelbinz/Psych-201) (fetched directly).
- Search summaries state Psych-201 contains 208,021 participants and 25,906,599 behavioural responses, ~3.5x Psych-101; this figure appears in the "Post-training makes LLMs less human-like" paper's description — [arXiv 2605.07632](https://arxiv.org/abs/2605.07632) [from search summary; not in the README I fetched].
- "Post-training makes large language models less human-like" (Binz et al., arXiv 2605.07632, May 2026): using Psych-201, post-training (instruction tuning/RLHF) "consistently reduces alignment with human behavior across model families, sizes, and objectives"; base models keep improving in behavioural alignment across generations while the post-training gap widens; persona induction "does not improve predictions at the level of individuals" — [arXiv 2605.07632](https://arxiv.org/abs/2605.07632) [from search summary].
- "Small Foundation Models of Human Cognition and Behaviour" (Nick Oh & Fernand Gobet, arXiv 2608.05224, COLM 2026; code "Centauri"): fine-tuned Llama 3.2/3.1 (1B-8B), Qwen3 (0.6B-14B), OLMo 2/3 (1B, 7B), SmolLM2/3 (0.1B-3B) with LoRA on Psych-101; finds models of "0.6B to 1B parameters suffice to match a reproduced Centaur-70B" in-distribution, with steeper scaling gradients out-of-distribution (Psych-201-RT benchmark); MIT-licensed code, 117 LoRA adapters under the "socius" Hugging Face org — [github.com/socius-org/Centauri](https://github.com/socius-org/Centauri) (fetched directly); [arXiv 2608.05224](https://arxiv.org/pdf/2608.05224).

**Stanford generative agents of real people (individual-level fidelity)**
- "Generative Agent Simulations of 1,000 People" (Park et al., arXiv 2411.10109, 15 Nov 2024): agents built from 2-hour qualitative interviews with 1,052 real individuals replicate their General Social Survey responses "85% as accurately as participants replicate their own answers two weeks later", perform comparably on Big Five and experimental replications, and reduce accuracy bias across racial/ideological groups relative to demographic-prompted agents — [arXiv 2411.10109](https://export.arxiv.org/abs/2411.10109) [from search summary].
- Code: [github.com/joonspk-research/genagents](https://github.com/joonspk-research/genagents), MIT licence, 13 commits on main, 6 open issues; includes agent class, memory stream + reflection, GSS-demographic example agents; the full 1,000-agent bank (2,000 interview hours) is NOT public — aggregated data on fixed tasks is open, individual responses on open tasks require a reviewed access request (fetched directly).

**Digital twins / silicon samples: aggregate vs individual fidelity (2025-2026)**
- Twin-2K-500 (Toubia, Gui, Peng, Merlau, Li, Chen; Marketing Science 2025 database report; arXiv 2505.17479): 2,058 US participants, ~2.42 h each, 4 waves, >500 questions incl. behavioural-economics replications; wave 4 repeats earlier tasks for a test-retest ceiling; "for 6 of the 10 results replicated by waves 1-3 and wave 4, the results from the digital twins also replicate" — [Marketing Science](https://pubsonline.informs.org/doi/10.1287/mksc.2025.0262); [arXiv](https://arxiv.org/abs/2505.17479) [from search summary].
- "When Can LLM Digital Twins Reduce Human Measurement? From Behavioral Fidelity to Statistical Substitutability" (arXiv 2609.07987, Sept 2026): across behavioural experiments and multiple models, twins "can reproduce average human effects while providing little information about which individuals differ from those averages"; behavioural fidelity is "neither necessary nor sufficient for statistical substitutability"; newer models and richer respondent info "do not reliably translate into human-data savings" — [arXiv 2609.07987](https://arxiv.org/abs/2609.07987) [from search summary].
- "Benchmarking large language model agent societies against human behavioural distributions" (Raad Bin Tareaf, arXiv 2608.28182, 28 Aug 2026) introduces SILICA: five environments with published human anchors plus rule-preserving perturbations and anti-memorisation variants; 12 open-weight models on one consumer GPU; agreement with humans "is confined to starting points": first-round public-goods contributions within the equivalence margin for 8 of 11 models, but "no model matches end-state contributions or the human corridor of cooperation"; code/transcripts on Zenodo — [arXiv 2608.28182](https://arxiv.org/abs/2608.28182) [from search summary].
- "Digital twins are funhouse mirrors: Five systematic distortions" (Science Advances, 2026; arXiv 2509.19088) — [Science Advances](https://www.science.org/doi/10.1126/sciadv.aeh8260) [title only; blocked].
- "Large language models that replace human participants can harmfully misportray and flatten identity groups" (Wang, Morgenstern, Dickerson; Nature Machine Intelligence 2025): human studies with 3,200 participants across 16 demographic identities on 4 LLMs show misportrayal and flattening; inference-time mitigations reduce but do not eliminate harms — [Nature Machine Intelligence](https://www.nature.com/articles/s42256-025-00986-z) [from search summary].
- "Statistical realism is not evidence that LLMs can estimate treatment effects in social science experiments" (Zonghan Li et al., arXiv 2604.02458, v. 27 Jul 2026): 11 interventions fielded to 59,508 respondents in 62 countries; correlation between statistical realism and treatment-effect accuracy is weak and optimising realism can worsen treatment-effect accuracy — [arXiv 2604.02458](https://arxiv.org/abs/2604.02458) [from search summary].
- "This human study did not involve human subjects: Validating LLM simulations as behavioral evidence" (arXiv 2602.15785, Feb 2026) — [arXiv](https://arxiv.org/pdf/2602.15785) [title only].
- Related 2025-2026 benchmarks/datasets (titles only, not read): SimBench (arXiv 2510.17516), SocioBench (arXiv 2510.11131), "Psychometric Comparability of LLM-Based Digital Twins" (arXiv 2601.14264), "Can Open-Weight LLMs Simulate Human Survey Populations?" (arXiv 2609.32638), "Item-Mean Surrogates: Why Richer Persona Data Fail to Improve LLMs as Human Surrogates" (arXiv 2608.29455), HumanLLM (arXiv 2601.15793), SocioVerse (10M-user pool; arXiv 2504.10157) — from [search results](https://arxiv.org/abs/2608.28182).

### Inferences
- On trial-level prediction of laboratory choice behaviour, no published system has been shown to beat Centaur-70B as of Sept 2026; the Centauri result (0.6B-1B parameter models match a reproduced Centaur-70B in-distribution) implies the 70B scale is not what carries the in-distribution fit, which weakens "foundation model" framing but strengthens practicality.
- The 2026 evidence converges on a consistent pattern across both Centaur-style models and digital twins: good aggregate/average reproduction, weak individual-level and out-of-distribution reproduction, and sensitivity to prompt/task perturbation. "Best predictor" therefore depends on level: Centaur for trial-level choices; interview-grounded generative agents for individual attitudes; neither for process/mechanism.
- The Binz-group finding that post-training reduces human-likeness suggests that the best base for a human simulator is a *base* (pre-instruction) model fine-tuned on behavioural data, not a chat model with a persona prompt.

### Gaps
- Exact Centaur fMRI alignment statistics and pseudo-R2 values could not be read (Nature and PMC full text blocked).
- Whether Binz et al. have released a "Centaur-2" trained on Psych-201 with public weights: search returned only the post-training paper and the Psych-201 repo; no confirmed 2026 successor model release. [UNVERIFIED]
- Full quantitative results of Bowers' Centaur breaking experiments were not readable (PsyArXiv/Sciety blocked).

---

## Key Question 2: Which cognitive architectures are still actively developed in 2026 and have open-source code?

### Takeaway
Soar (BSD-2, v9.6.5 released 6 May 2026) and ACT-R (Lisp, reference manual at 7.30+, plus GPL-3 Python port pyactr) are the two classical architectures with confirmed active maintenance and open code; the Common Model of Cognition group (Laird, Lebiere, Rosenbloom, Stocco) is actively publishing extensions (metacognition 2025, consciousness 2025, emotion 2024). CLARION has an experimental Python port (pyClarion); LIDA (Java, Memphis) and Sigma have no confirmed 2026 code activity.

### Cited Findings

**Soar**
- Official repo [github.com/SoarGroup/Soar](https://github.com/SoarGroup/Soar): "A cognitive architecture for developing systems that exhibit intelligent behavior"; licence BSD 2-Clause; 441 stars; ~10,102 commits on development branch with active CI; bindings for Python, Java, C#, Tcl (SWIG) and JavaScript (CMake); C/C++ core (fetched directly).
- Releases: Soar 9.6.5 on 6 May 2026 (CMake build integration, Python SWIG bindings with stable ABI, bug fixes); prior 9.6.4 on 22 July 2023 — [GitHub releases](https://github.com/SoarGroup/Soar/releases) (fetched directly).
- 45th Soar Workshop held 5 May 2025 with recordings online — [soar.eecs.umich.edu](https://soar.eecs.umich.edu/) [from search summary].
- Companion projects: [pysoarlib](https://github.com/Center-for-Integrated-Cognition/pysoarlib) (simplified Python API, Center for Integrated Cognition) and [jsoar](https://github.com/soartech/jsoar) (pure-Java Soar, SoarTech) — [search results](https://github.com/SoarGroup/Soar).

**ACT-R**
- Official software page [act-r.psy.cmu.edu/software](https://act-r.psy.cmu.edu/software/) [blocked]. Current reference manual is titled "ACT-R 7.30+ Reference Manual" (Dan Bothell), implying releases beyond 7.30 — [manual PDF](http://act-r.psy.cmu.edu/actr7.x/reference-manual.pdf) [from search listing]. Wikipedia's infobox still lists 7.21.6 (Dec 2020) as stable, which is stale — [from search summary]. Licence: ACT-R has historically been LGPL [UNVERIFIED — page blocked].
- pyactr ([github.com/jakdot/pyactr](https://github.com/jakdot/pyactr)): Python package "supports symbolic and subsymbolic processes in ACT-R and covers all basic cases of ACT-R modeling, including features that are not often implemented outside of the official Lisp ACT-R software"; GPL-3.0; 112 commits; deps numpy, simpy, pyparsing; companion open-access Springer textbook *Computational Cognitive Modeling and Linguistic Theory* (fetched directly). Last-commit date not visible.
- Other Python ACT-R implementations: [python_actr](https://github.com/CarletonCognitiveModelingLab/python_actr) (Carleton Cognitive Modeling Lab), [gactar](https://github.com/asmaloney/gactar) (single declarative format targeting multiple ACT-R implementations), [pyactr-demo](https://github.com/CentreForDigitalHumanities/pyactr-demo) (browser playground) — [search results](https://github.com/jakdot/pyactr).

**ACT-R x LLM hybrids (2025-2026)**
- "Cognitive LLMs: Toward Human-Like AI by Integrating Cognitive Architectures and LLMs for Manufacturing Decision-Making" (Wu, Oltramari, Francis, Giles, Ritter; Neurosymbolic AI journal 2025, doi 10.1177/29498732251377341; arXiv 2408.09176) and "LLM-ACTR" (AAAI Symposium Series): extracts ACT-R's internal decision process as latent vectors, injects into trainable LLM adapter layers, fine-tunes; reports better representation of human decision behaviour on a Design-for-Manufacturing task than a chain-of-thought LLM baseline; code at [github.com/SiyuWu528/cognitive-llm](https://github.com/SiyuWu528/cognitive-llm) — [AAAI-SS](https://ojs.aaai.org/index.php/AAAI-SS/article/view/35610); [journal](https://doi.org/10.1177/29498732251377341) [from search summaries].
- "Integrating language model embeddings into the ACT-R cognitive modeling framework" — Frontiers in Language Sciences, 2026 — [Frontiers](https://www.frontiersin.org/journals/language-sciences/articles/10.3389/flang.2026.1721326/full) [title only].
- "Human-Like Remembering and Forgetting in LLM Agents: An ACT-R-Inspired Memory Architecture" (HAI 2025): vector activation with temporal decay, semantic similarity and noise — [ACM](https://dl.acm.org/doi/10.1145/3765766.3765803) [from search summary].

**CLARION**
- pyClarion ([github.com/cmekik/pyClarion](https://github.com/cmekik/pyClarion), Can Mekik): "highly experimental" Python package implementing Clarion agents per Ron Sun's *Anatomy of the Mind*; sparse numerical structures, discrete-event simulation; bottom-level (Layer/Pool) and top-level (ChunkStore/RuleStore) with Choice component — [readme](https://github.com/cmekik/pyClarion/blob/main/readme.md) [from search summary]. Licence and last activity not confirmed.
- A 2026 SciTePress paper "Building Intelligent Agents Based on the Clarion Cognitive Architecture" indicates continued use — [SciTePress](https://www.scitepress.org/Papers/2026/144968/144968.pdf) [title only].
- Ron Sun's project page — [sites.google.com/site/drronsun/clarion](https://sites.google.com/site/drronsun/clarion/clarion-project).

**LIDA**
- LIDA Framework (Cognitive Computing Research Group, U. Memphis): Java software framework implementing LIDA's cognitive cycle (perception, attention, memory, action selection, learning) — [CCRG framework page](https://ccrg.cs.memphis.edu/framework.html) [blocked; description from search summary]. Current version, licence and 2026 activity: [UNVERIFIED].

**Sigma**
- Sigma (Paul Rosenbloom, USC): factor-graph-based architecture aimed at "grand unification"; last major system paper is JAGI 2016; "A Case for Cognitive Architectures and Sigma" arXiv 2101.02231 (2021) — [Semantic Scholar](https://www.semanticscholar.org/paper/The-Sigma-Cognitive-Architecture-and-System%3A-Grand-Rosenbloom-Demski/2a6a8056102bff449ec11748b9ac173b33dbcea4). Rosenbloom's 2025 output is on the Common Model and a memoir ("In search of insight: My life as an architectural explorer", JAGI 2025) — [Rosenbloom publications](https://sites.usc.edu/rosenbloom/recent-publications/) [from search summary]. No evidence of active Sigma code releases in 2025-2026. [Open-source status UNVERIFIED]

**Common Model of Cognition (cross-architecture standard)**
- "A Proposal to Extend the Common Model of Cognition with Metacognition" (Laird, Lebiere, Rosenbloom, Stocco; arXiv 2506.07807, June 2025) and a Springer chapter "Unified, Comprehensive Metacognition within the Common Model of Cognition" — [arXiv](https://arxiv.org/abs/2506.07807); [Springer](https://link.springer.com/chapter/10.1007/978-3-032-33195-3_1) [from search summary].
- "Mapping Neural Theories of Consciousness onto the Common Model of Cognition" (AGI 2025) and an emotion extension (2024) — [Springer](https://link.springer.com/chapter/10.1007/978-3-032-00800-8_14) [from search summary].
- "Clarifying System 1 & 2 through the Common Model of Cognition" (arXiv 2305.10654) — [arXiv](https://arxiv.org/pdf/2305.10654).

**LLM-hybrid cognitive architectures (CoALA lineage)**
- CoALA "Cognitive Architectures for Language Agents" (Sumers, Yao, Narasimhan, Griffiths; arXiv 2309.02427, 2023): organises agents by memory (working/long-term), action space (internal/external) and a decision loop with planning/execution; framework, not a runnable human simulator — [arXiv](https://arxiv.org/abs/2309.02427).
- "From Cognitive Architectures to Language Agents: A Mechanism-Level Review of Lineage, Convergence, and Migration Gaps" (arXiv 2607.23942, July 2026) reviews ACT-R, Soar, CLARION, LIDA vs CoALA-style agents; notes CLARION "coordinates explicit and implicit control" and LIDA "requires competition before selective broadcast", execution organisations that language agents have not migrated — [arXiv](https://arxiv.org/html/2607.23942v1) [from search summary; not read in full].
- "Evolving Cognitive Architectures" (arXiv 2601.05277, Jan 2026) — [arXiv](https://arxiv.org/pdf/2601.05277) [title only].
- Humanoid Agents ([github.com/HumanoidAgents/HumanoidAgents](https://github.com/HumanoidAgents/HumanoidAgents), EMNLP 2023 demo; arXiv 2310.05418): adds "System 1" state (basic needs: hunger, health, energy, social, enjoyment; emotions; relationship closeness) to generative agents; Apache-2.0; 324 stars, 24 commits; Unity WebGL front-end; README reports no comparison against human behavioural data (fetched directly).
- Original Stanford generative agents ([github.com/joonspk-research/generative_agents](https://github.com/joonspk-research/generative_agents)): Apache-2.0; 22.2k stars; requires OpenAI API key; 115 open issues / 31 PRs (fetched directly; last commit date not visible).

### Inferences
- The only classical architectures with confirmed 2026 code releases are Soar (May 2026) and ACT-R (7.30+ manual). CLARION/LIDA/Sigma persist mainly as theory and in the Common Model literature.
- Hybrid work in 2025-2026 flows in one direction: ACT-R components (memory activation, decision traces) are being grafted into LLM agents; there is no evidence of an LLM being used to *replace* modules inside a canonical ACT-R/Soar model for psychological simulation.

### Gaps
- Exact ACT-R current version number, release date and licence text could not be verified (official site blocked).
- LIDA Framework version/licence and pyClarion licence/activity unverified.
- No repo-level activity dates for pyactr, genagents, HumanoidAgents were visible in the fetched pages.

---

## Key Question 3: What are the leading 2025-2026 papers on LLMs as models of human cognition, and what did they find about fidelity and failure modes?

### Takeaway
2025-2026 work shows LLMs reproduce many *signatures* of human reasoning (content effects, effort/cost of thinking, most theory-of-mind tasks, several classic biases) while diverging in mechanism and in specific ways: hyper-conservatism on faux pas, non-human biases such as hallucination, missing irreducible semantic-memory structure, shallow verification loops in reasoning traces, and a systematic loss of human-likeness caused by post-training.

### Cited Findings

**Dual-process / System 1-System 2**
- "Dual-process theory and decision-making in large language models" (Nature Reviews Psychology, 2025): concludes LLM reasoning "is not fully analogous to human dual-process cognition", that observed 'cognitive' biases "often reflect patterns in their training data", and that LLMs "exhibit specific non-human biases, such as hallucination" — [Nature Reviews Psychology](https://www.nature.com/articles/s44159-025-00506-1) [from search summary].
- "Reasoning on a Spectrum: Aligning LLMs to System 1 and System 2 Thinking" (arXiv 2502.12470, Feb 2025) and "Giving AI Personalities Leads to More Human-Like Reasoning" (arXiv 2502.14155) — [arXiv](https://arxiv.org/pdf/2502.12470); [arXiv](https://arxiv.org/pdf/2502.14155) [titles only].
- "The role of System 1 and System 2 semantic memory structure in human and LLM biases" (arXiv 2604.12816, Apr 2026): finds semantic-memory structures "are irreducible only in humans", suggesting LLMs lack certain human conceptual knowledge organisation — [listing](https://awesomepapers.io/ai-agents/papers/2604.12816) [from search summary].
- "The cost of thinking is similar between large reasoning models and humans" (de Varda et al., PNAS, Nov 2025; MIT EvLab/McGovern): DeepSeek-R1 reasoning-token counts predict human reaction times within each of 7 tasks (numeric/verbal arithmetic, syllogisms, formal logic, relational, intuitive reasoning, structure mapping) with r = 0.39-0.89 (mean 0.62) vs r = 0.44 for base DeepSeek-V3 — [PNAS](https://www.pnas.org/doi/10.1073/pnas.2520077122); [MIT McGovern](https://mcgovern.mit.edu/2025/11/19/the-cost-of-thinking/) [from search summary]. A 2026 PNAS commentary asks whether thinking traces are "cognitive cost or performative scaffolding" — [PNAS](https://www.pnas.org/doi/10.1073/pnas.2604554123); follow-up "Effort as Ceiling, Not Dial" (arXiv 2605.16938) finds reasoning budget does not modulate the alignment — [arXiv](https://arxiv.org/pdf/2605.16938) [titles/summary only].
- "Language models, like humans, show content effects on reasoning tasks" (Lampinen et al., DeepMind; PNAS Nexus 3(7), July 2024): across NLI, syllogism validity and Wason selection, LMs "mix content into their answers to logic problems" like humans, with parallels down to the relation between model answer distributions and human response times — [PNAS Nexus](https://academic.oup.com/pnasnexus/article/3/7/pgae233/7712372) [from search summary].

**Cognitive-bias replication**
- Knipper et al. (2025): all tested LLMs show cognitive-bias susceptibility, 17.8%-57.3% on average across models and biases — cited in [USC AI Beat](https://libguides.usc.edu/blogs/USC-AI-Beat/bias-patterns-llms) [secondary source].
- "Cognitive Biases in LLMs: A Survey and Mitigation Experiments" (ACM SAC 2025): GPT-3.5/GPT-4 on six biases; "AwaRe" prompting mitigates — [ACM](https://dl.acm.org/doi/10.1145/3672608.3707812) [from search summary].
- Chen et al. (2025) test GPT-3.5/4 against 18 human biases in operations-management vignettes; "Large Language Newsvendor" (arXiv 2512.12552) and "The Bias is in the Details" (arXiv 2509.22856) extend this — [arXiv](https://arxiv.org/pdf/2512.12552); [arXiv](https://arxiv.org/pdf/2509.22856) [titles only].
- "Understanding the Anchoring Effect of LLM with Synthetic Data" (arXiv 2505.15392) — [arXiv](https://arxiv.org/pdf/2505.15392) [title only].
- Comment on Macmillan-Scott & Musolesi (2024) argues LLM biases are not evolutionary-mismatch biases and need comparative framing — [PMC](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC11858747/) [from search summary].

**Theory of mind**
- Strachan et al., "Testing theory of mind in large language models and humans" (Nature Human Behaviour, May 2024): GPT-4 at or above the level of 1,907 humans on false belief, irony, hints/indirect requests and misdirection, but below humans on faux pas; the deficit was traced to "a hyperconservative approach towards committing to conclusions", and rephrasing faux-pas questions as likelihood judgements yielded perfect GPT-4 performance — [Nature Human Behaviour](https://www.nature.com/articles/s41562-024-01882-z); [PsyPost](https://www.psypost.org/stunning-ai-discovery-gpt-4-often-matches-or-surpasses-humans-in-theory-of-mind-tests/) [from search summary].
- Street et al., "LLMs achieve adult human performance on higher-order theory of mind tasks" (Frontiers in Human Neuroscience, published 2 Jan 2026) — [Frontiers](https://www.frontiersin.org/journals/human-neuroscience/articles/10.3389/fnhum.2025.1633272/full) [from search summary]; the article notes "no consensus... about whether LLM theory of mind can be established by LLMs matching human behaviour, or whether they should also match human computations".
- 2026 preprints: "Developmental Trajectories of Situation Modeling and Mentalizing in Transformer Language Models" (arXiv 2606.28524), "Assessing mentalization in humans and LLMs" (arXiv 2608.26291), "Are LLMs Smarter Than Chimpanzees? Perspective Taking and Knowledge State Estimation" (arXiv 2601.12410) — [arXiv](https://arxiv.org/pdf/2606.28524); [arXiv](https://arxiv.org/pdf/2608.26291); [arXiv](https://arxiv.org/pdf/2601.12410) [titles only].

**Where LLM reasoning diverges from humans**
- "Post-training makes large language models less human-like" (Binz et al., May 2026): the processes that make LLMs useful assistants "also make them less accurate models of human behavior"; gap widens with newer generations — [arXiv 2605.07632](https://arxiv.org/abs/2605.07632) [from search summary].
- "Reasoning as Pattern Matching: Shared Mechanisms in Human and LLM Everyday Reasoning" (arXiv 2606.13607, June 2026): humans and 25 LLMs show similar error patterns on everyday common-sense reasoning — [arXiv](https://arxiv.org/pdf/2606.13607) [from search summary].
- "Large Language Model Reasoning Failures" (arXiv 2602.06176, Feb 2026): many LLM failures trace to human cognitive phenomena (distractibility, content effects, order effects), while others are model-specific instabilities — [arXiv](https://arxiv.org/html/2602.06176v1) [from search summary].
- "A Comprehensive Anatomy of Human and DeepSeek-R1 Mathematical Reasoning" (arXiv 2606.07410, June 2026): human solutions "maintain a compact alternation between analysis and deduction, whereas DeepSeek-R1 frequently revisits intermediate results and performs shallow verification without meaningful logical progress" — [arXiv](https://arxiv.org/html/2606.07410) [from search summary].
- "Theory-Grounded Evaluation of Human-Like Fallacy Patterns in LLM Reasoning" (arXiv 2506.11128) and "Dissecting Failure Dynamics in LLM Reasoning" (arXiv 2604.14528; RL can trigger "reasoning collapse" into heuristic guessing) — [arXiv](https://arxiv.org/pdf/2506.11128); [arXiv](https://arxiv.org/html/2604.14528) [from search summary].
- "Revealing emergent human-like conceptual representations from language prediction" (PNAS 2025) — [PNAS](https://www.pnas.org/doi/10.1073/pnas.2512514122) [title only].

**Methodology for evaluating LLMs as cognitive models**
- Ivanova, "How to evaluate the cognitive abilities of LLMs" (Nature Human Behaviour 9:230-233, 15 Jan 2025): 14 methodological considerations for AI-psychology studies — [Nature Human Behaviour](https://www.nature.com/articles/s41562-024-02096-z) [from search summary].
- "On Benchmarking Human-Like Intelligence in Machines" (arXiv 2502.20502) and "Six principles for evaluating cognitive capabilities in AI models" (AI Magazine) — [arXiv](https://arxiv.org/pdf/2502.20502); [ACM](https://dl.acm.org/doi/10.1002/aaai.70061) [titles only].
- ICLR 2025 survey "LLM Simulating Humanity" with curated list — [awesome-llm-human-simulation](https://github.com/Persdre/awesome-llm-human-simulation); [arXiv 2501.08579](https://arxiv.org/abs/2501.08579).

### Inferences
- The most-cited positive fidelity results are *signature-level* (content effects, RT/effort correlations, ToM task accuracy); the most robust negative results are *mechanism- and individual-level* (semantic-memory structure, verification dynamics, individual heterogeneity, post-training drift). This maps onto the Centaur debate: behavioural coverage is high, process fidelity is unestablished.
- The post-training finding implies that popular chat models (GPT-4/5-class, Claude, Gemini) are, by the Binz group's metric, *worse* models of human behaviour than their own base checkpoints; a simulator builder should prefer open base weights.

### Gaps
- Full texts of the Nature Reviews Psychology dual-process review and the 2026 arXiv failure-mode papers were not readable; effect sizes beyond those quoted are missing.
- No 2025-2026 source found that directly compares Centaur to interview-based generative agents on the same task.
- No DeepMind or Stanford HAI lab-page confirmation was retrievable (blocked); DeepMind's contribution here is the Lampinen et al. line of work.

---

## Key Question 4: What open-source code is available for building a human-reasoning simulator?

### Takeaway
A builder in Sept 2026 can assemble a stack entirely from open components: Centaur-70B LoRA adapter (Llama 3.1 licence) or the MIT-licensed Centauri recipe with 0.6B-14B adapters, the Psych-101 (HF) and Psych-201 (Apache-2.0, GitHub) transcript datasets, the MIT-licensed genagents interview-agent code, Apache-2.0 generative_agents and Humanoid Agents, GPL-3 pyactr / BSD Soar for process-level architectures, and Twin-2K-500 for calibrated digital-twin evaluation. The 1,000-person Stanford agent bank itself is not open.

### Cited Findings
| Component | Repo / location | Licence | Status (Sept 2026) | Source |
|---|---|---|---|---|
| Centaur 70B weights + adapter | huggingface.co/marcelbinz/Llama-3.1-Centaur-70B(-adapter) | llama3.1 | Released 2024-25; Nature paper Aug 2025 | [HF](https://huggingface.co/marcelbinz/Llama-3.1-Centaur-70B) [from search summary] |
| Centaur training/eval code | github.com/marcelbinz/Llama-3.1-Centaur-70B | not confirmed | — | [GitHub](https://github.com/marcelbinz/Llama-3.1-Centaur-70B) |
| Psych-101 dataset | huggingface.co/datasets/marcelbinz/Psych-101 (+ gated Psych-101-test, CC-BY-ND-4.0) | see HF card | Released 2024-25 | [Centauri README](https://github.com/socius-org/Centauri) [from search summary] |
| Psych-201 dataset | github.com/marcelbinz/Psych-201 | Apache-2.0 | Active; 416 commits; open PR contributions | [GitHub](https://github.com/marcelbinz/Psych-201) (fetched) |
| Centauri small-model recipe + 117 LoRA adapters | github.com/socius-org/Centauri; HF org "socius" | MIT (adapters inherit base licences) | COLM 2026; 29 commits | [GitHub](https://github.com/socius-org/Centauri) (fetched) |
| Generative agents (Smallville) | github.com/joonspk-research/generative_agents | Apache-2.0 | 22.2k stars; needs OpenAI key; 115 open issues | [GitHub](https://github.com/joonspk-research/generative_agents) (fetched) |
| genagents (interview-based agents of real people) | github.com/joonspk-research/genagents | MIT | 13 commits; agent bank restricted-access | [GitHub](https://github.com/joonspk-research/genagents) (fetched) |
| Humanoid Agents | github.com/HumanoidAgents/HumanoidAgents | Apache-2.0 | 324 stars, 24 commits; EMNLP 2023 demo | [GitHub](https://github.com/HumanoidAgents/HumanoidAgents) (fetched) |
| Soar | github.com/SoarGroup/Soar | BSD-2-Clause | v9.6.5, 6 May 2026 | [GitHub](https://github.com/SoarGroup/Soar/releases) (fetched) |
| pysoarlib | github.com/Center-for-Integrated-Cognition/pysoarlib | not confirmed | — | [search](https://github.com/SoarGroup/Soar) |
| ACT-R (Lisp, official) | act-r.psy.cmu.edu/software | LGPL [UNVERIFIED] | manual at 7.30+ | [manual](http://act-r.psy.cmu.edu/actr7.x/reference-manual.pdf) |
| pyactr | github.com/jakdot/pyactr | GPL-3.0 | 112 commits; last date not visible | [GitHub](https://github.com/jakdot/pyactr) (fetched) |
| python_actr | github.com/CarletonCognitiveModelingLab/python_actr | not confirmed | — | [search](https://github.com/jakdot/pyactr) |
| LLM-ACTR / Cognitive LLMs | github.com/SiyuWu528/cognitive-llm | not confirmed | 2025 journal paper | [search](https://github.com/SiyuWu528/cognitive-llm) |
| pyClarion | github.com/cmekik/pyClarion | not confirmed | "highly experimental" | [readme](https://github.com/cmekik/pyClarion/blob/main/readme.md) [from search summary] |
| LIDA Framework (Java) | ccrg.cs.memphis.edu/framework.html | not confirmed | [UNVERIFIED] | [CCRG](https://ccrg.cs.memphis.edu/framework.html) |
| Twin-2K-500 dataset | Marketing Science 2025 / SSRN 5265253 | not confirmed | Released 2025 | [SSRN](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=5265253) |
| SILICA agent-society benchmark | arXiv 2608.28182; data on Zenodo | open (per abstract) | Aug 2026 | [arXiv](https://arxiv.org/abs/2608.28182) [from search summary] |

- Practical note from Centauri: in-distribution fit to Psych-101 is matched by 0.6B-1B models, and 12 open-weight models can be run through SILICA "on a single consumer graphics card" — [Centauri](https://github.com/socius-org/Centauri); [arXiv 2608.28182](https://arxiv.org/abs/2608.28182) [from search summary].
- Prompt format for Psych-101/201 fine-tuning: human responses are wrapped in "<<" and ">>" in the transcript, and only those tokens are trained on — [Psych-201 README](https://github.com/marcelbinz/Psych-201) (fetched).

### Inferences
- The cheapest credible pipeline for a "human-reasoning simulator" today is: open base model (not instruction-tuned) + LoRA on Psych-101/201 transcripts (Centauri recipe) for choice behaviour, combined with genagents-style interview memory for individual-level attitudes, then validated against Twin-2K-500-style test-retest ceilings and SILICA-style perturbation tests rather than raw accuracy.
- Licensing is mixed: Centaur-70B is bound by the Llama 3.1 community licence; pyactr is GPL-3 (copyleft), which matters if embedding in a distributed product; Soar (BSD) and genagents/Centauri (MIT) are permissive.

### Gaps
- Licences for the Psych-101 training split, marcelbinz/Llama-3.1-Centaur-70B code repo, pysoarlib, python_actr, pyClarion, LIDA and SiyuWu528/cognitive-llm were not confirmed (pages not fetched or licence not shown).
- Last-commit dates for pyactr, genagents, generative_agents and HumanoidAgents were not visible in fetched content; "maintained" status is inferred from open issues/PR counts only.
- No evidence found of an official Python interface to Lisp ACT-R beyond the remote-interface described in the ACT-R 7.x manuals [not read].
