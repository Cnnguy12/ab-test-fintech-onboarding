# Experiment Readout: Round-Up Feature Onboarding Placement

*(Simulated data for portfolio purposes — see `experiment_design.md` for the pre-registered design and `notebooks/ab_test_analysis.ipynb` for the full analysis.)*

## Result

The treatment group (round-up savings prompted during onboarding) showed a statistically significant lift in 30-day adoption: **31.7% vs. 21.8% in control** (p < 0.0001, 95% CI on the difference: [7.1pp, 12.6pp]). That's a **9.9-point absolute lift, a 45% relative increase** — well above the 8-point lift the experiment was powered to detect.

## Guardrail

This is where the result gets more interesting than a clean "ship it." Onboarding completion was **93.6% in control vs. 91.0% in treatment — a 2.6-point drop, and it's statistically significant** (p = 0.0025). The pre-registered guardrail threshold was a maximum 2-point drop. **The guardrail was breached, narrowly.**

## Recommendation

**Do not ship as-is without a follow-up decision on the guardrail.** The primary metric result is strong and unambiguous, but the guardrail exists precisely to catch this scenario: a feature that drives real adoption at some cost to top-of-funnel completion. Two reasonable paths:

1. **Investigate and iterate**: the extra onboarding step likely adds friction for a subset of users. A/B test a lighter-weight version of the prompt (e.g., a single toggle instead of a multi-screen explainer) to see if adoption lift can be preserved while recovering completion.
2. **Ship with a monitored exception**: if 2.6 points of completion is judged an acceptable trade for a 45% relative adoption gain (a product/business call, not a statistics call), ship it but monitor completion rate closely post-launch and set a rollback trigger if the gap widens.

What we should *not* do is quietly ignore the guardrail breach because the primary metric looks good — that defeats the purpose of pre-registering it.

## Caveats

- Data is simulated to match the design doc's assumptions, not pulled from a real app — there's no live fintech product behind this project. The statistical workflow (power analysis → primary test → guardrail check → readout) is the deliverable, not these specific point estimates.
- A real rollout should re-validate with a holdout after 60-90 days to rule out novelty effects on the adoption lift.
- The guardrail breach here happened to land just past the 2pp threshold at this sample size and random seed; a production experiment would want to look at the confidence interval on the guardrail delta too, not just the point estimate, before deciding how alarmed to be.
