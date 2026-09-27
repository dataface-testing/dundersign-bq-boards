# Dundersign — boards

Dundersign's analytics warehouse is BigQuery, project `internal-dataface-eng`.
dbt writes to datasets `dundersign` (core), `dundersign_staging`, and
`dundersign_serving` (`daily_metrics`, `monthly_metrics`). This repo is for the
dashboards on top of it; nothing here yet.

## dbt Charts Cloud

This project is published to the `cx4-05` organization as
`dundersign-bq-boards`. After changing a board, commit and push to `main`,
then run `dct cloud project sync` to publish the update.
