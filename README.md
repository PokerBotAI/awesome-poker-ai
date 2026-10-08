# Awesome Poker AI [![Awesome](https://awesome.re/badge.svg)](https://awesome.re)

> A curated list of AI poker research, open-source tools, solvers, and educational resources. Updated for 2026.

Poker is one of the most challenging domains for AI due to imperfect information, hidden cards, bluffing, and multi-player dynamics. This list covers the key research breakthroughs, open-source projects, and tools that have shaped the field.

## Contents

- [Research Papers](#research-papers)
- [LLMs vs Poker: The 2025-2026 Wave](#llms-vs-poker-the-2025-2026-wave)
- [Open-Source Frameworks](#open-source-frameworks)
- [Hand Evaluators](#hand-evaluators)
- [Open-Source Solvers](#open-source-solvers)
- [Commercial Solvers](#commercial-solvers)
- [Training Platforms](#training-platforms)
- [AI Poker Bots](#ai-poker-bots)
- [LLM Poker Projects](#llm-poker-projects)
- [Benchmarks & Evaluation](#benchmarks--evaluation)
- [Educational Resources](#educational-resources)
- [Notable Commentary & Analysis](#notable-commentary--analysis)

## Research Papers

### Landmark Papers

- [DeepStack](https://arxiv.org/abs/1701.01724) — First AI to defeat professional poker players in heads-up no-limit Hold'em using recursive reasoning and deep learning (University of Alberta, 2017). Published in [Science](https://www.science.org/doi/10.1126/science.aam6960).

- [Libratus](https://www.science.org/doi/10.1126/science.aao1733) — Defeated four top human pros in a 120,000-hand HUNL competition using blueprint strategy, real-time sub-game solving, and self-improvement (CMU, 2017).

- [Pluribus](https://www.science.org/doi/10.1126/science.aay2400) — First superhuman AI for six-player no-limit Hold'em, trained in 8 days on a 64-core server using Linear CFR (Meta + CMU, 2019). [Author PDF](https://noambrown.github.io/papers/19-Science-Superhuman.pdf).

- [ReBeL](https://arxiv.org/abs/2007.13544) — General self-play RL + search framework that converges to Nash equilibrium in two-player zero-sum games; achieves superhuman HUNL poker (Meta, 2020). [Official code](https://github.com/facebookresearch/rebel).

### Post-2020 Papers

- [Student of Games](https://arxiv.org/abs/2112.03178) — Unified algorithm for both perfect and imperfect information games; achieves strong performance in chess, Go, and HUNL poker (DeepMind + Alberta, 2023). Published in [Science Advances](https://www.science.org/doi/10.1126/sciadv.adg3256).

- [AlphaHoldem](https://ojs.aaai.org/index.php/AAAI/article/view/20394) — End-to-end RL framework using a pseudo-siamese architecture; beats Slumbot and DeepStack after 3 days training on a single PC (Tsinghua, AAAI 2022).

- [DecisionHoldem](https://arxiv.org/abs/2201.11580) — Open-source HUNL AI combining blueprint strategy and real-time safe depth-limited solving. [GitHub](https://github.com/AI-Decision/DecisionHoldem).

- [PokerGPT](https://arxiv.org/abs/2401.06781) — End-to-end lightweight solver for multi-player Texas Hold'em via fine-tuning a pre-trained LLM (OPT-1.3B) with RLHF on real game logs. Demonstrates that small language models can learn poker decision-making without expensive CFR computation (Huang et al., 2024).

- [SpinGPT](https://arxiv.org/abs/2509.22387) — First LLM specifically trained for Spin & Go poker tournaments. Two-stage training: supervised fine-tuning on 320,000 expert decisions + reinforcement learning on 270,000 solver-generated hands. Achieves 78% solver agreement and 13.4 BB/100 vs Slumbot in heads-up play. Accepted at ACG 2025, published in LNCS (Maugin & Cazenave, 2025).

## LLMs vs Poker: The 2025-2026 Wave

The explosion of general-purpose LLMs created massive public interest in whether ChatGPT, Claude, and Grok could play poker. Short answer: they can't — not at a competitive level. But the experiments were fascinating.

### Events

- **[Kaggle AI Poker Showdown](https://www.kaggle.com/game-arena)** (February 2026) — Google DeepMind and Kaggle organized the first major LLM-vs-LLM poker exhibition. Ten flagship models (GPT-5.2, GPT-o3, GPT-5 mini, Grok-4, Grok 4.1 Fast Reasoning, Gemini 3 Pro, Gemini 3 Flash, Claude Opus 4.5, Claude Sonnet 4.5, DeepSeek-V3.2) played 900,000+ hands of heads-up NLHE. GPT-5.2 was the most profitable overall; o3 won the exhibition bracket. All models played without solvers or CFR — pure text-pattern decisions. Doug Polk, Nick Schulman, and Liv Boeree provided commentary.

- **[PokerBattle.ai](https://pokerbattle.ai/about)** (October-November 2025) — Five-day LLM cash game marathon organized by Max Pavlov. Nine models played Texas Hold'em around the clock. OpenAI o3 won with $36,691 profit over 3,799 hands. Meta LLAMA 4 performed worst, busting its entire $100K bankroll. Demonstrated the same fundamental LLM weaknesses: excessive aggression, poor bluffing comprehension, inability to fold.

### Key Takeaways

The consensus from Kaggle, PokerBattle.ai, and professional analysis is clear:

1. **LLMs do not understand poker mathematics.** They generate plausible-sounding text about poker but cannot reliably calculate equity, pot odds, or EV.
2. **LLMs hallucinate hand strength.** They confuse suits, misread boards, and misidentify winning hands — even when they answer correctly in isolation.
3. **LLMs cannot adapt to opponents.** No cross-hand memory, no range construction, no exploitative adjustments.
4. **Specialized poker AI (CFR-based) solved this years ago.** Libratus (2017) and Pluribus (2019) achieved superhuman play through game theory, not language modeling. LLMs represent a step backward for poker AI, not forward.

SpinGPT is the notable exception — but it requires solver-generated training data and works only in a severely constrained format (3-player Spin & Go with short stacks).

## Open-Source Frameworks

- [OpenSpiel](https://github.com/google-deepmind/open_spiel) — Google DeepMind's collection of environments and algorithms for RL research in games, with extensive poker support (Kuhn, Leduc, ACPC universal poker interface) and CFR/MCCFR implementations.

- [RLCard](https://github.com/datamllab/rlcard) — Toolkit for RL in card games; supports Limit/No-Limit Hold'em, Leduc, Blackjack, Mahjong, UNO, and more. [Website](https://rlcard.org/).

- [PokerRL](https://github.com/EricSteinberger/PokerRL) — Multi-agent deep RL framework implementing NFSP, Deep CFR, Single Deep CFR, and RPG; supports distributed computing via Ray.

- [PyPokerEngine](https://github.com/ishikota/PyPokerEngine) — Lightweight Python poker engine for AI development with an Emulator class for RL and a browser-based GUI.

- [PokerKit](https://github.com/uoftcprg/pokerkit) — Comprehensive Python library supporting Texas Hold'em, Omaha, Stud, Razz, and custom game variants (University of Toronto). [Paper](https://arxiv.org/abs/2308.07327).

- [clubs](https://github.com/fschlatt/clubs) — Python poker engine with OpenAI Gym interface; supports arbitrary community card game configurations (~714K hand evaluations/sec).

- [neuron_poker](https://github.com/dickreuter/neuron_poker) — Texas Hold'em OpenAI Gym environment with Keras-RL and a C++ equity module (~500x faster than Python).

- [deepcfr-texas-no-limit-holdem-6-players](https://github.com/dberweger2017/deepcfr-texas-no-limit-holdem-6-players) — Deep CFR implementation for 6-player NLHE with progressive training phases (random opponents → self-play → mixed pools), GRU-based opponent modeling, and a PyQt5 GUI. 80+ stars (2024-2025).

## Hand Evaluators

- [PokerHandEvaluator](https://github.com/HenryRLee/PokerHandEvaluator) — High-performance C/C++ evaluator using a perfect hash algorithm; supports 5-7 card hands and Omaha (PLO4/5/6). Python bindings available.

- [treys](https://github.com/ihendley/treys) — Python 3 hand evaluator using bit arithmetic and lookup tables; evaluates 5/6/7 card hands (~250K evaluations/sec).

- [deuces](https://github.com/worldveil/deuces) — Original pure-Python hand evaluation library, written for the MIT Pokerbots Competition.

## Open-Source Solvers

- [TexasSolver](https://github.com/bupticybee/TexasSolver) — Free open-source Texas Hold'em GTO solver with a GUI (Windows/macOS/Linux); performance comparable to PioSOLVER. [Website](https://bupticybee.github.io/texassolver_page/).

- [postflop-solver](https://github.com/b-inary/postflop-solver) — Rust-based postflop GTO solver using Discounted CFR. Also available as a [web app](https://wasm-postflop.pages.dev/) and [desktop app](https://github.com/b-inary/desktop-postflop).

- [slumbot2019](https://github.com/ericgjackson/slumbot2019) — C++ CFR implementations (CFR+, MCCFR, Targeted CFR) by the creator of Slumbot, a multi-year ACPC champion.

- [ReBeL](https://github.com/facebookresearch/rebel) — Meta's official open-source implementation of the ReBeL algorithm for imperfect-information games.

## Commercial Solvers

| Name | Website | Description |
|------|---------|-------------|
| PioSOLVER | [piosolver.com](https://piosolver.com/) | Industry-standard NLHE postflop solver |
| GTO+ | [gtoplus.com](https://www.gtoplus.com/) | Fast, memory-efficient NLHE solver with multi-way support |
| MonkerSolver | [monkerware.com](https://monkerware.com/solver.html) | Industry standard for PLO and multi-way spots |
| Deepsolver | [deepsolver.com](https://deepsolver.com/) | Cloud-based solver, solves any spot on-demand |
| HRC | [holdemresources.net](https://www.holdemresources.net/) | Tournament (ICM) preflop analysis |

## Training Platforms

| Name | Website | Description |
|------|---------|-------------|
| GTO Wizard | [gtowizard.com](https://gtowizard.com/) | AI-powered solver + trainer with on-demand solving. In 2025, partnered with GGPoker, WPN, and WPT Global for [anti-RTA detection](https://blog.gtowizard.com/towards-a-safer-poker-ecosystem/) — tracking real-time solver use during play |
| PokerSnowie | [pokersnowie.com](https://www.pokersnowie.com/) | Neural network poker coach with play-against-AI mode |

## AI Poker Bots

### Commercial

- [PokerBotAI](https://pokerbotai.com/) — AI poker bot platform since 2016; supports 20+ rooms (PPPoker, GGPoker, ClubGG, WePoker, etc.) using the TriBrain Engine — a three-component architecture combining hand history analysis, neural networks (7B+ hands), and expert algorithms.
  - [How AI Poker Bots Make Decisions](https://pokerbotai.com/docs/how-bots-think-decision-tree/) — TriBrain Engine architecture, adaptation curve, opponent modeling.
  - [Types of Poker Bots](https://pokerbotai.com/docs/types-of-poker-bots/) — Classification: rule-based, GTO, exploitative, AI, and hybrid.
  - [Bot vs RTA vs Solver vs Trainer](https://pokerbotai.com/docs/bot-vs-rta-vs-solver-vs-trainer/) — Key differences between poker assistance tools.
  - [How Poker Rooms Detect Bots](https://pokerbotai.com/docs/how-poker-rooms-catch-bots/) — Detection methods in 2026 and anti-detection techniques.
  - [Poker Bot Costs in 2026](https://pokerbotai.com/docs/how-much-do-poker-bots-cost/) — Pricing comparison across solvers, trainers, RTA, and AI bots.
  - [ROI and Realistic Expectations](https://pokerbotai.com/docs/poker-bot-roi-realistic-expectations/) — Real performance data: 150-500% ROI, winrate benchmarks.
  - [FAQ: Top 10 Questions](https://pokerbotai.com/docs/faq-top-10-questions-about-poker-bots/) — Safety, earnings, cost, experience, and getting started.
 
- [PokerBot.com](https://www.pokerbot.com/) — Bot technology for private clubs and operators: liquidity bots and bot detection.

### Historical

- [Slumbot](http://www.slumbot.com/) — Multi-year Annual Computer Poker Competition champion by Eric Jackson; plays HUNL against humans for free online.

## LLM Poker Projects

A growing number of projects attempt to use general-purpose LLMs for poker. None are competitive with CFR-based solvers, but they serve as research tools and benchmarks for LLM reasoning capabilities.

- [poker_LLM](https://github.com/whmmy/poker_LLM) — AI-powered Texas Hold'em framework where LLMs (OpenAI, Claude, DeepSeek, QWen) act as players. Includes a Vue 3 replay visualization system and AI self-reflection on decisions. Python + Vue 3 (2024-2025).

- [HarperJonesGPT/PokerGPT](https://github.com/HarperJonesGPT/PokerGPT) — PokerStars screen-reading bot using GPT-4 API for decision-making via OCR + prompt engineering. Not fine-tuned — pure API calls. A hobby project, not competitive.

## Benchmarks & Evaluation

- [poker-eval](https://github.com/superagent-ai/poker-eval) — TypeScript framework for evaluating AI agent performance in simulated NLHE cash games. Uses standard poker KPIs (BB/100, EV, VPIP). Supports Vercel AI SDK, OpenAI, Mastra, LlamaIndex, and Langchain. Includes a [leaderboard](https://github.com/superagent-ai/poker-eval) of LLM performance (2024).

  Current leaderboard (1000 hands vs 2x GPT-4o baseline):
  | Model | BB/100 |
  |-------|--------|
  | mistral-large-latest | +11.26 |
  | gpt-4o | -14.78 |
  | claude-3-5-sonnet | -19.95 |
  | gpt-4o-mini | -45.09 |
  | gemini-1.5-pro | -166.85 |

- [AI Poker Bots vs Rule-Based Bots](https://poker-ai.org/ai-poker-bots-vs-rule-based-bots/) — Six commercial bots at one PPPoker table, 26,395 hands. AI bots won +29.2 bb/100, rule-based bots lost −24.3 (95% intervals). Hand histories included.

## Educational Resources

### Poker Math & Strategy (by PokerBotAI)

- [EV and Equity: Why Bots Don't Care About Luck](https://pokerbotai.com/docs/ev-and-equity/) — Expected value and equity in AI decision-making.

- [Pot Odds and Implied Odds in 5 Minutes](https://pokerbotai.com/docs/pot-odds-and-implied-odds/) — How bots compute pot odds in real-time.

- [GTO Strategy for Poker Bots](https://pokerbotai.com/docs/gto-strategy-poker-bot/) — Combining GTO-base protection with exploitative play.

- [Variance and Sample Size](https://pokerbotai.com/docs/variance-and-sample-size/) — Why short-term results are deceiving and what the distance threshold means.

### Getting Started

- [PokerBotAI in 5 Minutes](https://pokerbotai.com/docs/pokerbotai-in-5-minutes/) — Quick start guide to AI poker bot platforms.

- [Create a Poker Bot Using Python](https://pokerbotai.com/blog/how-to-create-a-poker-bot-using-python/) — Tutorial: building a poker bot with Python and CFR.

- [Pluribus: The AI That Changed Poker](https://pokerbotai.com/blog/pluribus-poker-the-ai-bot-thats-taking-the-poker-world-by-storm/) — How Facebook's Pluribus beat six human pros at once.

## Notable Commentary & Analysis

Coverage and analysis of the LLM-poker intersection from industry voices:

- [Nate Silver — "ChatGPT is shockingly bad at poker"](https://www.natesilver.net/p/chatgpt-is-shockingly-bad-at-poker) — Silver Bulletin deep dive: GPT-o3 fails to simulate an 8-player NLHE hand, miscalculates pots, and misidentifies winning hands on a QQ445 board.

- [Pokerfuse — "Why the AI Poker Challenge Is a Red Herring — Albeit a Funny One"](https://pokerfuse.com/latest-news/2026/2/why-ai-poker-challenge-red-herring-albeit-funny/) — Industry analysis arguing that LLM poker tournaments are entertainment, not progress in poker AI.

- [Poker.org — "Hyper-aggressive OpenAI bots reign supreme"](https://www.poker.org/latest-news/hyper-aggressive-openai-bots-reign-supreme-as-silicon-poker-battle-concludes-aM9TD0I6XqAu/) — Kaggle Game Arena recap with Polk, Schulman, and Boeree commentary.

- [GTO Wizard — "Towards a Safer Poker Ecosystem"](https://blog.gtowizard.com/towards-a-safer-poker-ecosystem/) — GTO Wizard's public announcement of cooperation with poker rooms to detect real-time solver use. Partnership with GGPoker led to 31 immediate account bans (March 2025).

---

## Contributing

Contributions welcome! Please submit a pull request or open an issue to suggest additions.

## License

[![CC0](https://licensebuttons.net/p/zero/1.0/88x31.png)](https://creativecommons.org/publicdomain/zero/1.0/)
