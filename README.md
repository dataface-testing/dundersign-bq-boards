# Dundersign — boards

Dundersign's analytics warehouse is BigQuery, project `internal-dataface-eng`.
dbt writes to datasets `dundersign` (core), `dundersign_staging`, and
`dundersign_serving` (`daily_metrics`, `monthly_metrics`). This repo holds the
dashboards on top of it, as [dbt charts](https://dbtcharts.com) board YAML.

## Boards

| Board | What it answers |
|---|---|
| [`charts/overview.yaml`](charts/overview.yaml) | Company at a glance: active users, signups, revenue, document completion, and three years of monthly trend. |
| [`charts/signing_funnel.yaml`](charts/signing_funnel.yaml) | The document lifecycle: how far recipients get through signing, how long completion takes, and which devices and countries the sessions come from. |
| [`charts/growth.yaml`](charts/growth.yaml) | Go-to-market: paid signup conversion, pipeline vs. closed-won, subscription starts against cancellations, and acquisition mix. |

`charts/meta.yaml` sets the defaults shared by every board — currently just the
`warehouse` source, so no board has to repeat it.

### A convention worth keeping

The warehouse is loaded through a fixed end date, so the newest month and quarter
are always partial. Every trend here drops that trailing period rather than
plotting it, so the last point is never a cliff that is really just a short
month. The KPI rows compare the last **complete** month against the one before
it for the same reason.

## Running the boards locally

Boards read BigQuery through a service account; the key is never committed, and
`dbt_charts.yml` carries no credential field at all (see the comment there for
why). Authenticate with Application Default Credentials, pointing at a key file
that lives outside this repo:

```bash
export GOOGLE_APPLICATION_CREDENTIALS=/path/to/key.json
dct validate
dct serve
```

The service account only needs to read the `dundersign*` datasets:
`roles/bigquery.jobUser` on the project, plus `roles/bigquery.dataViewer`
restricted by an IAM condition to resources under
`projects/internal-dataface-eng/datasets/dundersign`.

## Cloud

The boards are published to dbt charts Cloud under the `onboard-05`
organization, project `dundersign-bq-boards`. Cloud pulls from `main`, so every
push re-renders. The `warehouse` source maps to the `internal-dataface-eng`
connection there, which carries its own copy of the credential.
