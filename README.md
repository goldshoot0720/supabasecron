# supabasecron

GitHub Actions workflows for periodically reading data from Supabase.

## Workflows

| Workflow | Supabase table | Schedule (UTC) |
| --- | --- | --- |
| Fetch Supabase Food Every 6h6m | `food` | 00:06, 06:06, 12:06, 18:06 |
| Fetch Supabase Subscription Every 6h7m | `subscription` | 00:07, 06:07, 12:07, 18:07 |
| Credit 鋒兄銀行 Daily | `bank_accounts` | 00:00 Asia/Taipei (16:00 UTC) |

Both workflows can also be run manually from the Actions tab.

## Required repository secrets

Set these repository secrets before enabling the scheduled workflows:

- `SUPABASE_URL` — the URL of the Supabase project.
- `SUPABASE_KEY` — the Supabase service-role key used by these server-side
  workflows. Do not expose this key in browser code.

Each run fetches the table's JSON response and writes it to the workflow log. The response is not committed back to the repository.

## 鋒兄銀行每日入帳

Apply [`supabase/migrations/20260915000000_create_feng_brother_bank_credit.sql`](supabase/migrations/20260915000000_create_feng_brother_bank_credit.sql)
to the Supabase project before enabling the workflow. It creates the
`bank_accounts` table and the `credit_feng_brother_bank` database function.

The first run creates `鋒兄銀行` with a balance of NT$0. On each following
calendar day in the `Asia/Taipei` timezone, it adds NT$33. The database function
records the credited date, so GitHub Actions retries or manual runs do not add
more than NT$33 on the same day.
