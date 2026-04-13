# Monte Carlo Assumptions — Illicit Drug Trade / Prohibition Profit Floor

All values in $B USD (annualized). Every parameter traces to paper §4–§5
or the citations in `data_sources.md`. Run `python mc_simulation.py` to
reproduce bit-identical results.

---

## Simulation Parameters

| Parameter | Value | Justification |
|-----------|-------|---------------|
| Seed | 42 | Fixed for reproducibility |
| N draws | 100,000 | 4-decimal CI stability |
| Cross-channel correlation ρ | 0.3 | Shared macro drivers (GDP, population, regulation) |
| Private payoff Π | $275.0B/yr | Annual industry revenue — see `data_sources.md` |
| β_W median (result) | 13.01 | Confirmed by N=100,000 draws |
| ΔW median (result) | $3,579.1B/yr | Sum of channel medians (correlated) |

**Π = revenue, not profit.** SAPM Iron Law: βW = ΔW/Π where Π is annual
revenue. Using profit would inflate βW by 5–20× for low-margin industries.

---

## Channel Parameters

| Channel | Dist | Low | Mid | High | Description |
|---------|------|-----|-----|------|-------------|
| `C1_public_health` | lognormal | $1,800B | $2,400B | $3,200B | Overdose deaths, addiction treatment, disease transmission |
| `C2_violence_capture` | lognormal | $350B | $420B | $500B | Cartel violence, state capture, homicides |
| `C3_criminal_justice` | normal | $180B | $230B | $280B | Incarceration, policing, courts |
| `C4_money_laundering` | lognormal | $150B | $250B | $350B | Financial system distortion, laundering costs |
| `C5_producer_country` | lognormal | $100B | $165B | $250B | Development destruction in producer countries |
| `C6_governance` | lognormal | $60B | $100B | $160B | Institutional failure, corruption, regulatory evasion |


All ranges represent [P5, P95] of the channel-specific distribution as
calibrated from literature in paper §4.

---

## Impossibility Floor

The floor β_W ≥ 3.0 is the minimum ratio achievable while the industry operates.
This bounds the simulation from below: the theorem holds regardless of parameter values,
because even best-case scenarios exceed the floor.

In 100,000 draws: P(β_W < 3.0) = 0.0000%

## Sensitivity (VSL × Double-Counting Grid)

Central VSL (1.0×): no DC adj β_W = 12.96 | 20% DC adj = 10.37 | 40% DC adj = 7.78

See `mc_results.json` → `sensitivity_matrix` for full 5×5 grid.

## Distribution Robustness

The simulation uses a lognormal/normal mix calibrated to channel-specific
uncertainty structure. Results are robust: the central β_W changes by less
than ±0.3 under all-lognormal or all-normal configurations.

---

## Plausibility Checks (SAPM IL#28)

- **Annual flow**: All W_i are $/yr flows ✓
- **GDP bound**: ΔW = $3,579B = 3.4% of world GDP ($106T) ✓
- **β_W range**: 13.01 is within the [0.5, 100] plausible range ✓
- **P(β_W < 1)**: 0.0000% ✓
