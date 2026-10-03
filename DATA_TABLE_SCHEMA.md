# Data Table Schema — AICOS Clinics Edition v1.0 Free Beta

Create `aicos_clinic_leads` with **all 13** custom columns. Every column is needed by the shipped upsert mapping; this is separate from which input values are mandatory.

| Column | n8n type | Purpose |
|---|---|---|
| lead_id | String | Supplied identifier; not a unique key |
| name | String | Supplied name; may be empty |
| phone | String | Exact-string duplicate key |
| service_type | String | Service scoring component |
| source | String | Source scoring component |
| message | String | Supplied message; may be empty |
| preferred_time | String | Time bonus/draft value; may be empty |
| branch | String | Supplied branch; may be empty |
| status | String | `new` on insert; existing status preserved on update |
| priority | String | LOW / MEDIUM / HIGH |
| score | Number | Configured numeric score |
| touch_count | Number | 1 on insert; increments on repeat |
| last_seen | Date/Time | Generated latest activity timestamp |

Ten String, two Number and one Date/Time column. n8n creates `id`, `createdAt`, `updatedAt`; do not add them manually. Phone must remain String to preserve `+` and zeros. Number columns must not be String.

Verify table resolution in **Find Existing Lead** and **Save Lead (Upsert)**. Refresh/check upsert mappings if needed. The export uses table name resolution.

## Runtime contract

`lead_id` and `phone` are string inputs. Identifier must contain a non-whitespace character; phone matches `^\+?[0-9]{8,15}$`. The regex checks formatting, not ownership, reachability or validity in a particular country. Empty optional fields are allowed; provided text fields should be strings. Missing/unknown service/source score zero; empty preferred time uses `غير محدد` in drafts.

Extra fields are not part of the saved mapping. The shipped sample input does not pass through unknown incoming fields. Arbitrary text-field objects/numbers are outside the documented contract; null phone was verified to reject safely, not to establish arbitrary null/type support.

Deduplication matches exactly on phone. No trimming or country-code normalization is implemented. Repeating lead_id with a different phone creates a different record. Existing multiple rows with the same phone and concurrent inserts are outside verified behavior; use a clean test table and sequential runs.
