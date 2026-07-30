# A/B Test — Fintech App Feature Adoption

Experiment design, power analysis, and statistical readout for a simulated onboarding-placement test — the full experimentation workflow end to end, including a guardrail metric that gets breached and has to be reasoned about, not rubber-stamped. Question: does placing the round-up savings feature inside onboarding (vs. leaving it in Settings) increase 30-day adoption, and does it come at a cost to onboarding completion?

## Key results

| # | Step | Key result |
|---|------|------------|
| 1 | Design doc ([`experiment_design.md`](experiment_design.md)) | Power analysis: **492 users/group** required to detect an 8pp lift at 80% power; 4,000 simulated |
| 2 | Analysis ([`notebooks/ab_test_analysis.ipynb`](notebooks/ab_test_analysis.ipynb)) | Chi-square test on the primary metric, 95% CI on the lift, guardrail check |
| 3 | Primary metric | **31.7%** treatment vs. **21.8%** control adoption (p < 0.0001) — a 9.9pp / 45% relative lift |
| 4 | Guardrail metric | Onboarding completion dropped **2.6pp** (93.6% -> 91.0%, p = 0.0025) — **breaches** the pre-registered 2pp threshold |
| 5 | Readout ([`experiment_readout.md`](experiment_readout.md)) | Recommendation: don't ship on the primary metric alone — iterate on a lighter prompt, or ship with an explicit, monitored trade-off decision |

## Notes on results

This is a more useful portfolio result than a clean "ship it": the guardrail actually breaches in this simulation run, which forces a real trade-off decision instead of a rubber-stamp recommendation. Data is simulated to match the design doc's stated assumptions (there's no live fintech app behind this) — the statistical workflow (power analysis -> primary test -> guardrail check -> readout) is the deliverable being demonstrated, not the specific point estimates.

## Structure

```
experiment_design.md         pre-registered hypothesis, metrics, power analysis
notebooks/                   executed analysis notebook
experiment_readout.md        result + recommendation
adoption_by_group.png        adoption rate chart
```

## Setup

```bash
pip install pandas numpy scipy statsmodels matplotlib
python build_notebook.py   # regenerates the notebook
python -m nbconvert --to notebook --execute --inplace notebooks/ab_test_analysis.ipynb
```

## License

MIT — see [LICENSE](LICENSE).
