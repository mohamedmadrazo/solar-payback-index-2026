# Post-Credit Solar Payback Index 2026

Residential solar simple payback for all 50 US states, recomputed after the 30% federal
tax credit (Section 25D) expired on 31 December 2025.

One formula, applied identically to every state, from four public inputs. The CSV in this
repository is the same file published at
<https://watt-guide.com/assets/data/solar-payback-index-2026.csv>.

- **Canonical page (method, sortable table, limits):** <https://watt-guide.com/guides/solar-payback-by-state-2026>
- **Version:** 1.0 · **Published:** 2026-07-05 · **Last verified:** 2026-07-26
- **Licence:** [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) — reuse it, cite it.

## The formula

```
annual production  = peak sun hours x 365 x 0.80          (per kW installed)
annual savings     = production x retail rate x value factor
payback (years)    = installed cost / annual savings
```

`value factor` is how a state credits exported power:

| Regime | Factor | States |
|---|---|---|
| Full-retail net metering | 1.00 | 28 |
| Net billing / avoided cost | 0.58 | 4 |
| No statewide mandate | 0.46 | 18 |

**Payback does not depend on system size.** Cost and savings both scale linearly with kW,
so the ratio cancels. The `_11kw_` columns are a worked reference case (11 kW at $2.58/W =
$28,380); any other size gives the same payback years.

## Columns

| Column | Unit | Meaning |
|---|---|---|
| `state` | — | US state name |
| `rate_c_kwh` | cents/kWh | Residential retail electricity rate |
| `psh` | hours/day | NREL PVWatts peak sun hours |
| `kwh_per_kw_yr` | kWh | Annual production per kW installed (`psh x 365 x 0.80`) |
| `net_metering` | enum | `full` / `net_billing` / `none` |
| `value_factor` | ratio | Export credit factor applied to savings |
| `payback_now_yrs` | years | Simple payback with no federal credit |
| `payback_with_credit_yrs` | years | Simple payback as it was with the 30% credit |
| `delta_yrs` | years | Years added by the credit expiring |
| `sys_cost_11kw_usd` | USD | Installed cost of the 11 kW reference system |
| `annual_savings_11kw_now_usd` | USD | Year-1 savings of that system, no credit |

## Sources

- **Retail rates:** EIA residential electricity prices, April 2026 (via ChooseEnergy).
- **Peak sun hours:** [NREL PVWatts](https://pvwatts.nrel.gov/) v8.
- **Net-metering regime:** statewide policy status, April 2026.
- **Installed cost:** EnergySage 2026 national median, $2.58/W.

## Honest limits — read before citing

- **These are statewide averages.** Your utility, roof orientation and tariff will differ.
- **Simple payback.** No electricity-price inflation (which would shorten it) and no
  discounting (which would lengthen it). It is not an NPV or IRR.
- **California is modelled with the generic net-billing factor.** Its NEM 3.0 export rates
  are lower still, so real California payback is likely somewhat longer than shown.
- **"No statewide mandate" states vary widely by utility.** Some plans beat the average
  comfortably. Treat that tail as a pessimistic edge, not a floor.
- **This is modelling, not field measurement.** No system was installed or metered to
  produce these numbers.

### Two rounding characteristics

1. `annual_savings_11kw_now_usd` is computed from unrounded production, while
   `kwh_per_kw_yr` is rounded to one decimal. Recomputing savings from the rounded column
   can differ by one or two dollars.
2. `payback_now_yrs`, `payback_with_credit_yrs` and `delta_yrs` are each rounded to one
   decimal independently, so in 11 of the 50 rows `now - with_credit` differs from `delta`
   by exactly 0.1 years.

Neither affects any ranking or conclusion, but if you rebuild the numbers you will see them.

## How to cite

> de Madrazo, B. (2026). *Post-Credit Solar Payback Index 2026: residential solar simple
> payback for the 50 U.S. states after the federal credit expired* (Version 1.0) [Data set].
> Watt Guide. https://watt-guide.com/guides/solar-payback-by-state-2026

```bibtex
@dataset{demadrazo2026solarpayback,
  author    = {de Madrazo, Bruno},
  title     = {Post-Credit Solar Payback Index 2026},
  year      = {2026},
  version   = {1.0},
  publisher = {Watt Guide},
  url       = {https://watt-guide.com/guides/solar-payback-by-state-2026},
  note      = {CSV: https://watt-guide.com/assets/data/solar-payback-index-2026.csv. Licence CC BY 4.0}
}
```

## Corrections

Errors found in this dataset or its companion pages are logged publicly at
<https://watt-guide.com/corrections>.
