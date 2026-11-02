# Lab 8 — Capstone Research Proposal

**Deliverable:** [FEAther_Proposal.pdf](FEAther_Proposal.pdf) (4 pages, IEEE two-column).
**Source:** [source/main.tex](source/main.tex) and [source/refs.bib](source/refs.bib), compiled with Tectonic (XeTeX).
**Pitch deck:** [FEAther_Pitch.pptx](FEAther_Pitch.pptx) ([PDF](FEAther_Pitch.pdf)), 7 slides for the
3-minute pitch plus the references; the pitch script is in the speaker notes.

**Title:** *FEAther: A Self-Learning Multi-Agent System for Lightweight Load-Bearing Part Design with Finite Element Analysis*

## Summary

LLMs can now write CAD programs, but they are trained and judged on whether a shape *looks* right, not
whether the part *holds its load*. The proposal trains an open-weight LLM with reinforcement learning
(GRPO with QLoRA on Qwen3-8B), rewarded by a finite element analysis of each part it designs. The
designer sits in a multi-agent system: an untrained parser turns a request into a spec, and a sandboxed
checker grades each program and reports where it fails. At run time the designer revises its design
until the part passes, then removes material while it still passes.

Closest work: COSMO-Agent (arXiv 2026) trains with a solver in the loop, but only sizes 25 fixed
templates. Son et al. (arXiv 2026) give FEA feedback to frontier agents at run time without training
them. FEAther trains the model that chooses the *configuration*.

## Research questions

| | Question | Independent variable(s) | Dependent variable(s) |
|---|---|---|---|
| RQ1 | Does GRPO with an FEA-graded reward raise the share of held-out specs fully passed, compared with SFT alone and with a shape-similarity reward? | training: SFT only; GRPO with shape, FEA, or both rewards | full pass rate; requirements met; invalid rate |
| RQ2 | Does run-time FEA feedback improve designs beyond training, and is the gain from feedback or from more attempts? | designer (SFT / GRPO / GRPO with revise and lighten prompts); one-shot / best-of-k / loop; k = 1, 3, 5, 10 | specs passed within k; mass of lightest pass; tokens per solved spec |
| RQ3 | How much material do passing designs use, and what does the mass term change? | reward with or without the mass term | mass relative to sizing-only and topology-optimized references |

## Pilot results in the proposal

- The checker's FEA agrees with hand calculations within 10% on ten reference parts; refining the mesh
  moves each value by under 4%.
- 40 generated specs, each proven solvable by a reference the checker passes.
- Untrained Qwen3-1.7B and Qwen3-8B pass none of them. About 80% of their revisions repeat the program
  they were asked to fix, so independent samples beat the feedback loop at an equal budget.
