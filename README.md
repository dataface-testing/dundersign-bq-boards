# Dundersign — boards

Dundersign's analytics warehouse is BigQuery, project `internal-dataface-eng`.
dbt writes to datasets `dundersign` (core), `dundersign_staging`, and
`dundersign_serving` (`daily_metrics`, `monthly_metrics`). This repo holds the
dbt charts boards on top of it.

## dbt charts Cloud

- Organization: `r2-05`
- Project: `dundersign-bq-boards`
- Published at: https://dbtcharts.com/r2-05/dundersign-bq-boards/
- Warehouse connection: `dundersign-bq` (BigQuery `internal-dataface-eng`,
  default dataset `dundersign_serving`)

Boards live in `charts/`. To render locally you need a BigQuery credential:
set `DCT_BQ_KEYFILE` to a service-account JSON key with read access to
`dundersign_serving`, then `dct serve`. On Cloud the mapped connection supplies
the credential instead, so that env var is not needed there.

Ship a change with `git push` followed by `dct cloud project sync` — a push
alone does not publish.
