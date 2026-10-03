# Full Setup Guide — AICOS Clinics Edition v1.0 Free Beta

## 1. Prepare

Use n8n with Data Tables and permission to import/create tables. No credentials or paid API are required. Use an isolated environment and synthetic records. The legacy docs name n8n 2.31.5; the latest isolated test version was not captured, so run the checks in your own version. Save a copy of any files/configuration before editing them.

## 2. Import

Import `workflow.json` from the workflow **Import from File** action. Confirm nine nodes and connections. The legacy title is `AICOS - Lead Response Kit - Clinics Edition v1.0 - SELLABLE`; this does not imply a paid offer. Keep inactive/unpublished. Do not replace an existing workflow or reuse a table containing real records for testing.

## 3. Create the table

Create a table named exactly `aicos_clinic_leads`. Follow [DATA_TABLE_SCHEMA.md](DATA_TABLE_SCHEMA.md): all 13 custom columns must exist. Add each column with the correct type. `score` and `touch_count` are Number; `last_seen` is Date/Time; all remaining custom fields are String. Let n8n create `id`, `createdAt` and `updatedAt`.

## 4. Verify bindings and mappings

The export references the table by name, not by an installation-specific table ID. In **Find Existing Lead**, verify Get Row(s), `aicos_clinic_leads`, phone Equals the sample phone expression, and limit 1. In **Save Lead (Upsert)**, verify Upsert, the same table and match condition, and all 13 manually mapped fields. If the table is unresolved, re-select it in each node and refresh/check mappings without replacing the expressions. Confirm numeric types before executing.

## 5. Review configuration and input

Use [CONFIGURATION_GUIDE.md](CONFIGURATION_GUIDE.md). Check the Arabic wording against what your team can honor. SLA values and channel labels are informational. The LOW template mentions one business day; revise that configuration if inappropriate. No actual contact is scheduled.

Keep **Lead Input (Sample)** in Manual Mapping with its eight string fields, and Include Other Input Fields off. Edit sample values there for tests. Do not switch input modes merely to change one value: n8n may discard assignments when switching. Use the saved export to recover the sample if needed. Actual null values require an explicit test input; the text `null` is not a JSON null.

## 6. First valid run

Execute the original sample documented in [README.md](README.md). Expect score 55/MEDIUM, `VALID`, `NEW`, result `محفوظ`, no reject reason, Arabic draft and SLA 30. In the table confirm one new row, touch_count 1 and last_seen set. Compare Owner Review fields listed in the README; it is a separate output from the stored row.

## 7. Duplicate and rejection

Execute again with the identical phone. Expect one updated row, incremented touch_count and last_seen, preserved status, `UPDATED_EXISTING` and `مكرر — تم التحديث`.

Set lead_id to three spaces; expect `missing_lead_id` and no write. Restore lead_id and set phone to `abc`; expect `invalid_phone` and no write. Restore the original input afterward. Never delete rows to hide a result.

## 8. Acceptance and evaluation

Run [TEST_CHECKLIST.md](TEST_CHECKLIST.md) and record table counts before/after. Evaluate one lead per manual execution; batch/concurrent behavior is not established. Check the LOW/MEDIUM/HIGH vectors. Inspect all nodes to confirm no outbound action was added.

Do not use sensitive real records until you have validated suitability, access and retention in your environment. Submit sanitized feedback using [BETA_FEEDBACK.md](BETA_FEEDBACK.md). Connecting an intake source or real messaging service is outside this supplied beta and its verification.

## Recovery

Keep a prior export before edits. Restore that export in a separate workflow if assignments or expressions are damaged, and verify it against the test table. Do not overwrite real workflows or delete existing tables. See [TROUBLESHOOTING.md](TROUBLESHOOTING.md).
