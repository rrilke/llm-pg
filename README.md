# LLM public goods game

First test of Study 1 (see memo below): groups of 4 LLM players (Claude, GPT, Grok, Gemini) play a 5-period linear
public goods game, in two treatments. See `public_goods_llm.ipynb`.

| Treatment | Groups | Runs |
|---|---|---|
| `homogeneous` | 4 instances of the same model | 1 per model = 4 |
| `mixed` | composition of the 4 models drawn at random (balanced, seeded) | 4 |

Players are not told who the other players are unless `DISCLOSE_COMPOSITION = True`. Each player instance is a
stateless API call that sees its own history and the group totals only.

1. `pip install -r requirements.txt`
2. Copy `.env.example` to `.env` and fill in the API keys (`ANTHROPIC_API_KEY`, `OPENAI_API_KEY`, `XAI_API_KEY`, `GOOGLE_API_KEY`).
3. Run the notebook.

Outputs: `results.csv` (one row per player and period), `beliefs.csv` (period-1 beliefs), `raw_answers.csv`
(verbatim model answers), `groups.csv` (compositions), `contributions.png`.


# Preliminary research memo: Cooperation between LLMs and humans

**Discussion:** Call with Alexandros Karakostas (ESSCA), 19 October 2026

## Motivation and scope

This project will investigate how cooperation varies with the identity of an LLM's interaction partner. The longer-term goal is a paper comprising two complementary studies: one on cooperation among LLMs and another comparing LLM cooperation with human and LLM partners.

## Study 1: Cooperation across model identities

**Research question:** Do LLMs cooperate differently when paired with the same model, another version from the same provider, or a model from a different provider?

This study would test whether cooperation exhibits a form of model homophily. The initial hypothesis is that models cooperate more with partners that are similar to themselves, particularly models from the same provider, than with models from other providers. The design should distinguish exact model/version matches from broader provider-level similarity, since these are different forms of similarity.

## Study 2: Cooperation with human partners

**Research question:** Do LLMs cooperate more with human partners than with other LLMs?

This study would compare LLM behavior across human-partner and LLM-partner conditions. It complements Study 1 by asking whether partner identity matters across the human–LLM boundary, rather than only among models.

## Potential implementation

One proposed approach is to treat each model-version combination as a distinct participant identity and include a broad range of available models. OpenRouter was suggested as a potential platform for accessing multiple models. This approach would require documenting model versions and settings, and defining how models are sampled and compared. The analysis should also account for repeated observations from each model-version combination.

## Open design questions

- Which public-goods-game protocol and cooperation measure should be used across both studies?
- How should partner composition, role assignment, prompts, and interaction history be standardized?
- Which model versions should be included, and how will provider similarity be separated from model-level differences?
- For the human comparison, how will human participants be recruited and matched to LLMs, and how will incentives be made comparable?
- What sample size and number of repeated interactions are needed to distinguish partner effects from variation across model versions?