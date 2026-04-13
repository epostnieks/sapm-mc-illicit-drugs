# SAPM Monte Carlo — Illicit Drug Trade / Prohibition Profit Floor

**Public replication repository for quantitative results in:**

> Postnieks, E. (2026). *Illicit Drug Trade (Prohibition Profit Floor).* SAPM Working Paper. SSRN.

This repository provides everything needed to independently reproduce, audit,
and extend the Monte Carlo simulation underlying the paper's core results.
The paper is available on SSRN.

---

## Results (N = 100,000 draws, seed = 42)

| Statistic | Value |
|-----------|-------|
| **β_W median** | **13.01** |
| β_W mean | 13.15 |
| β_W std | 1.83 |
| **90% CI** | **[10.4, 16.4]** |
| 99% CI | [9.5, 18.1] |
| P(β_W < 1) | 0.0000% |
| **ΔW median** | **$3,579.1B/yr** |
| Π (revenue) | $275.0B/yr |

**β_W = 13.01** means the illicit drug trade industry destroys **$13.01 in system
welfare for every $1.00 in revenue** — across 6 channels and 100,000 Monte Carlo draws.

**Classification**: Class 2 — Intractability

---

## What Is β_W?

```
β_W = ΔW / Π
```

- **ΔW** = total annualized welfare destruction ($B/yr) across all channels
- **Π** = annual industry **revenue** ($B/yr) — not profit

β_W > 1: industry destroys more welfare than it captures in revenue.
β_W > 3: Strong Intractability threshold — reform requires structural replacement.

---

## Quick Start

```bash
git clone https://github.com/epostnieks/sapm-mc-illicit-drugs.git
cd sapm-mc-illicit-drugs
pip install numpy scipy
python mc_simulation.py
```

Expected output: `β_W median : 13.01` and `ΔW median : $3,579.1B/yr`

---

## Welfare Channels

| Channel | Median ($B/yr) | 90% CI | Distribution |
|---------|---------------|--------|--------------|
| C1_public_health | $2,397.7B | [$1,796.3B, $3,196.6B] | Lognormal |
| C2_violence_capture | $419.9B | [$352.6B, $500.6B] | Lognormal |
| C3_criminal_justice | $230.0B | [$180.0B, $279.9B] | Normal |
| C4_money_laundering | $250.2B | [$178.4B, $349.7B] | Lognormal |
| C5_producer_country | $164.7B | [$109.1B, $249.2B] | Lognormal |
| C6_governance | $99.9B | [$62.6B, $160.0B] | Lognormal |
| **Total ΔW** | **$3,579.1B** | **[$2,860.2B, $4,506.8B]** | Correlated (ρ=0.3) |

---

## Impossibility Floor

The floor β_W ≥ 3.0 cannot be breached by any policy while the
industry continues to operate. In 100,000 draws, only **0.0000%**
fall below this floor — confirming the structural constraint.

## Repository Contents

| File | Description |
|------|-------------|
| `mc_simulation.py` | Self-contained simulation — no private pipeline imports |
| `mc_results.json` | Pre-run results (100K draws, seed=42) — matches paper |
| `mc_histogram.json` | Binned β_W distribution (80 bins) for companion chart |
| `assumptions.md` | Every parameter: value, derivation, source |
| `data_sources.md` | Full citation list for all empirical inputs |

---

## Replication Notes

Results are seeded and deterministic. Tested with:
```
numpy==1.26.4  scipy==1.12.0  Python 3.11.9
```

The `median` and `ci_90` (to 1 decimal) match exactly across compatible versions.

---

## License

CC BY 4.0. Cite as:

> Postnieks, E. (2026). *SAPM Monte Carlo — Illicit Drug Trade (Prohibition Profit Floor)*.
> GitHub: epostnieks/sapm-mc-illicit-drugs.
> https://github.com/epostnieks/sapm-mc-illicit-drugs
