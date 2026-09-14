# supabasecron

GitHub Actions workflows for periodically reading data from Supabase.

## Workflows

| Workflow | Supabase table | Schedule (UTC) |
| --- | --- | --- |
| Fetch Supabase Food Every 6h6m | `food` | 00:06, 06:06, 12:06, 18:06 |
| Fetch Supabase Subscription Every 6h7m | `subscription` | 00:07, 06:07, 12:07, 18:07 |

Both workflows can also be run manually from the Actions tab.

## Required repository secrets

Set these repository secrets before enabling the scheduled workflows:

- `SUPABASE_URL` — the URL of the Supabase project.
- `SUPABASE_KEY` — a key with read access to the `food` and `subscription` tables.

Each run fetches the table's JSON response and writes it to the workflow log. The response is not committed back to the repository.
