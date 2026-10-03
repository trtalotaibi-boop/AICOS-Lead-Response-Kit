# Demo — one synthetic clinic lead

Use the sample in `demo/sample_input.json` and an isolated fresh table. It is a synthetic fixture, never a contact instruction. Copy its values into the existing Lead Input (Sample) fields; the JSON file does not add a new intake mechanism.

1. Show the imported nine-node workflow, manual trigger and inactive/unpublished state.
2. Show the test table schema and baseline row count.
3. Execute the sample. Explain that the identifier and phone format passed.
4. Show score 55: أسنان 30 + واتساب 20 + preferred time 5. Priority is MEDIUM; compare `demo/expected_first_output.json`.
5. Show Owner Review identity, source, validation, NEW, result and Arabic draft. SLA is an informational preview; no message was sent.
6. Show one stored row with touch_count 1 and last_seen.
7. Execute the same phone again. Show UPDATED_EXISTING and one row with touch_count 2 and refreshed last_seen.
8. Change lead_id to three spaces. Show REJECTED / NOT_SAVED / missing_lead_id and unchanged row count; restore input.
9. Invite voluntary feedback on installation, clarity and usefulness.

## Screenshot plan

All are **SCREENSHOT_NEEDED**. No new launch screenshots have been captured or fabricated.

- Workflow canvas: nine nodes, inactive state; hide personal account details.
- Table schema: all 13 custom columns/types.
- Accepted Owner Review: synthetic sample, score55/MEDIUM/draft.
- Duplicate Owner Review and table: one row, touch_count2.
- Rejected Owner Review: missing_lead_id, NOT_SAVED.

Use only the isolated demo environment and sanitize browser/account details. Screenshots are optional supporting assets; the text demo is usable now.
