# Asset Insights Case Study

## Problem and solution

Infrastructure planners need a repeatable view of condition, backlog, maintenance, and renewal pressure across disconnected operational tables. The project generates a synthetic council dataset, loads relational data, calculates documented KPIs, and exports dashboard-ready CSVs.

## Architecture

```mermaid
flowchart LR
    Generator[seeded synthetic generator] --> Raw[relational CSV tables]
    Raw --> SQLite[in-memory SQLite analysis]
    SQL[documented SQL queries] --> SQLite
    SQLite --> KPIs[KPI and trend preparation]
    KPIs --> Outputs[six dashboard CSVs]
    Outputs --> BI[Power BI, Tableau, or Excel]
```

## Trade-offs

- Synthetic data makes the work shareable and deterministic but cannot demonstrate real council data quality.
- CSV outputs are tool-neutral but do not preserve semantic models or interactive dashboards.
- Renewal ranking is a transparent prioritisation aid, not an engineering condition assessment.

## Measured validation

- Regeneration produced 114 assets, 456 inspections, 467 maintenance records, and 510 cost records.
- Six required dashboard outputs were rebuilt; all contained headers and data rows (114 total lines including headers).

## Limitations and failure modes

- Results depend on synthetic distributions and should not be generalized to a real portfolio.
- Geographic analysis is suburb-level rather than coordinate-level.
- Cost and condition assumptions need domain-owner validation before operational use.

## Reproduce

```bash
python scripts/generate_sample_data.py
python scripts/prepare_dashboard_outputs.py
wc -l outputs/dashboard/*.csv
```
