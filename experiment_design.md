# Experiment: Onboarding Placement of Round-Up Savings Feature

## Hypothesis
Placing the automatic round-up savings feature inside the onboarding flow (vs. only surfacing it later in Settings, the current state) increases 30-day feature adoption.

## Metrics
- **Primary**: 30-day feature adoption rate (did the user turn on round-up savings within 30 days of signup)
- **Guardrail**: onboarding completion rate (must not drop by more than 2 percentage points — we don't want to trade adoption for a worse signup funnel)

## Design
- **Unit of randomization**: user, at signup
- **Split**: 50/50 control (Settings-only) vs. treatment (prompted during onboarding)
- **Minimum sample size**: see power analysis below

## Power Analysis
Assuming a baseline adoption rate of 24% (control) and wanting to detect a lift to 32% (treatment) — an 8-point absolute lift — at α = 0.05 and 80% power:

**Required sample size: 492 users per group (984 total)** — see `notebooks/ab_test_analysis.ipynb` for the calculation. The simulation below uses 4,000 total users (2,000/group), comfortably powered.

## Rollout Plan
Run for a minimum of 2-3 weeks to reach the required sample per group and let the 30-day adoption window mostly play out before the readout; monitor the guardrail metric daily to allow for early stop on a serious regression.
