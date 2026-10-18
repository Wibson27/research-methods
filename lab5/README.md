# Lab 5 — Scoping a Grounded Research Gap in LLM4APR

**Deliverable:** [Lab5_Research_Gap_Statement.pdf](Lab5_Research_Gap_Statement.pdf) (2 pages).
**Source:** [source/Lab5_Research_Gap_Statement.html](source/Lab5_Research_Gap_Statement.html).

**Title:** *Does In-Loop LLM Review Make Patches Correct, or Only Make Them Pass? A Research Gap in Repository-Level LLM4APR*

**Bottleneck selected:** patch correctness, with cost. It is drawn from the MAGIS paper (Tao et al., NeurIPS 2024) and the LLM4APR systematic literature review (Zhang et al., ACM TOSEM 2026).

## Summary

Repository-level repair pipelines such as MAGIS add an in-loop LLM reviewer and credit it with resolution gains. Those gains are measured only by SWE-bench's original tests. Peer-reviewed studies show these tests accept many incorrect patches:

- about 11% of plausible patches are incorrect, inflating reported resolution by 6.4 points (ICSE 2026);
- 345 mislabelled patches were found (ACL 2025);
- top agents' resolved rates drop by 4.2–9.0% under augmented tests (ASE 2026).

Whether LLM review makes patches more *correct*, or mostly makes more of them *pass*, has not been measured.

The statement proposes **differential review**: before deciding, the reviewer sees executed inputs on which the original and the patched program behave differently, and must justify each difference against the issue. It is evaluated against a strengthened oracle.

## Research questions

| | Question | Independent variable(s) | Dependent variable(s) |
|---|---|---|---|
| RQ1 | How much of text-only in-loop review's resolution gain persists under a strengthened oracle? | review (none / text-only); oracle (original / strengthened) | resolution rate; illusory gain |
| RQ2 | Does differential review raise correct resolution and reduce plausible-but-incorrect patches vs text-only review? | reviewer type (text-only / differential) | correct-resolution rate; incorrect-plausible share; reviewer false-approval and false-rejection rates |
| RQ3 | What does each review design cost per *correctly* resolved issue? | review condition (none / text-only / differential) | tokens, US$, wall-clock time per correct resolution |
