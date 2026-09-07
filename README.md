# Dundersign — boards

Dundersign's analytics warehouse is BigQuery, project `internal-dataface-eng`.
dbt writes to datasets `dundersign` (core), `dundersign_staging`, and
`dundersign_serving` (`daily_metrics`, `monthly_metrics`). This repo is for the
dashboards on top of it; nothing here yet.

## Boards

Published to dbt charts Cloud — organization `r3-05`, project
`dundersign-bq-boards`: https://dbtcharts.com/r3-05/dundersign-bq-boards/

Boards live in `charts/`. Cloud reads BigQuery through the `dundersign-bigquery`
connection (service account `dct-r3-05-reader@internal-dataface-eng`), which the
`warehouse` source maps to.

To render locally, point `DCT_BQ_KEYFILE` at a service-account JSON key with
read access to `dundersign_serving`, then `dct serve`. Cloud ignores that key
and uses the mapped connection instead.

Ship a change with `git push` followed by `dct cloud project sync` — a push
alone does not publish.
