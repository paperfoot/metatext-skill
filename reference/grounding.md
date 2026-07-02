# Grounding — the evidence behind "Why it happens"

Each cause in `SKILL.md` traces to published work. Every arXiv id below was verified to resolve to the stated paper (title, authors, year cross-checked against the abstract page and an independent search). Titles are as they appear on arXiv.

## Verbosity / length bias
- **Singhal, Goyal, Xu, Durrett (2023), "A Long Way to Go: Investigating Length Correlations in RLHF"** — arXiv:2310.03716. A length-only reward reproduces most of the downstream gains of RLHF over the SFT model; reward models are easily driven by length.
- **Dubois, Galambosi, Liang, Hashimoto (2024), "Length-Controlled AlpacaEval: A Simple Way to Debias Automatic Evaluators"** — arXiv:2404.04475. Regressing out length raises the benchmark's agreement with human preference to ~0.98 — length was inflating win-rates.
- **Chen et al. (2024), ODIN — arXiv:2402.07319.** A length-decorrelated reward removes much length-driven reward gaming while preserving quality. (Companion: "Disentangling Length from Quality in Direct Preference Optimization", arXiv:2403.19159.)

## Sycophancy
- **Sharma et al. / Anthropic (2023), "Towards Understanding Sycophancy in Language Models"** — arXiv:2310.13548. Human raters *and preference models* sometimes prefer convincingly-written sycophantic answers over correct ones; optimizing against the PM can trade truth for sycophancy.
- **Perez et al. / Anthropic (2022), "Discovering Language Model Behaviors with Model-Written Evaluations"** — arXiv:2212.09251. Sycophancy increases with model scale and with RLHF steps.
- **Cheng et al. (2025), "ELEPHANT: Measuring and understanding social sycophancy in LLMs"** — arXiv:2505.13995. Flattery and excessive validation in current models, beyond opinion-matching.
- **Fanous et al. / Stanford (2025), "SycEval: Evaluating LLM Sycophancy"** — arXiv:2502.08177. Documents answer-switching under pushback in frontier models.

## Over-caution / disclaimers (distinct from sycophancy)
- **Röttger et al. (2023), "XSTest: A Test Suite for Identifying Exaggerated Safety Behaviours in LLMs"** — arXiv:2308.01263. Models refuse or hedge on safe prompts that merely resemble unsafe ones — the origin of reflexive disclaimers a real instance would not carry.

## Ambiguity under-resolution (the XY problem)
- **Su & Cardie (2026), "Knowing but Not Showing: LLMs Recognize Ambiguity but Rarely Ask Clarifying Questions"** — arXiv:2605.25284. A clear recognition-vs-behaviour gap: models flag ambiguity when asked to judge it, yet in generation overwhelmingly default to a direct answer; retrieved context widens the gap.
- **Zhang & Choi (2023), "Clarify When Necessary: Resolving Ambiguity Through Interaction with LMs"** — arXiv:2311.09469. Frames when to clarify / what to ask / how to use the answer; clarification helps but is not the default.
- **Zhang et al. (2024), "CLAMBER: A Benchmark of Identifying and Clarifying Ambiguous Information Needs"** — arXiv:2405.12063. Even with CoT/few-shot, spontaneous identification of ambiguity is unreliable.

## LLM register / metadiscourse
- **Kobak et al. (2024), "Delving into LLM-assisted writing in biomedical publications through excess vocabulary"** — arXiv:2406.07016. Across 14M PubMed abstracts, an abrupt post-ChatGPT surge in "excess" style words — a measurable register imprint on real documents.
- **Reinhart et al. (2024), "Do LLMs write like humans? Variation in grammatical and rhetorical styles"** — arXiv:2410.16107. LLMs overuse interactional/engagement metadiscourse and discourse markers vs humans. (Note: on genuine hedges LLMs can *under*-produce relative to humans — so the tell is over-produced *structure*, not hedging per se.)
- **Freeburg (2026), "The Last Fingerprint: How Markdown Training Shapes LLM Prose"** — arXiv:2603.27006. Markdown structural features (headers, bullets, em-dashes) leak from training register into prose.

## Format / structure reward bias
- **Zhang et al. (2024), "From Lists to Emojis: How Format Bias Affects Model Alignment"** — arXiv:2409.11704. Reward models and judges prefer lists, bold, headers, emojis independent of content — a distinct reward-gaming axis from length.
- **Liu et al. (2025), "Format as a Prior: Quantifying and Analyzing Bias in LLMs for Heterogeneous Data"** — arXiv:2508.15793 (AAAI 2026). Format acts as a prior that biases model behaviour.

## Default assistant persona leakage (the deepest cause)
- **(2026), "The Assistant Axis: Situating and Stabilizing the Default Persona of Language Models"** — arXiv:2601.10387. Post-training installs a default assistant persona whose register bleeds into outputs.
- **(2026), "As X, Do Y: How Persona and Task Combine in Instruction-Tuned LLMs"** — arXiv:2605.23147. How an assigned persona and the task interact in instruction-tuned models — relevant to "inhabit the artifact's real author".

## Model-specific note (why the taxonomy is audit-only)
Anthropic's Opus 4.8 guidance states positive examples of the target style suppress verbosity/over-explaining better than negative "do not" instructions, and flags rigid ALWAYS/NEVER lists as a yellow flag; OpenAI's GPT-5.5 guidance similarly prefers outcome-first framing and decision rules over prohibition stacks, and exposes a `text.verbosity=low` knob. Hence: use `taxonomy.md` as an after-the-fact audit checklist; when producing, lead with the role frame and a clean exemplar.
- Prompting Claude Opus 4.8 — https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/prompting-claude-opus-4-8
- Claude 4.x best practices — https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-4-best-practices
- OpenAI GPT-5.5 prompt guidance — https://developers.openai.com/api/docs/guides/prompt-guidance
