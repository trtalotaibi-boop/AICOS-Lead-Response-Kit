# Test Checklist — AICOS Clinics Edition v1.0 Free Beta

## Accepted maintainer evidence

The owner's accepted isolated verification dated 2026-10-03 reports 15/15 PASS, clean install PASS, valid LOW/MEDIUM/HIGH, exact-phone update, Owner Review and Arabic drafts. No outbound send was present and the live workflow was unchanged. This report is not a claim of universal n8n compatibility or arbitrary batch/type support.

## Reproduce in your installation

Use an isolated instance, the shipped workflow and a fresh table from DATA_TABLE_SCHEMA.md. Keep inactive/unpublished. Record n8n version, execution status, Owner Review, row counts and timestamps. Use synthetic data only; never contact sample numbers.

| # | Case | Expected |
|---|---|---|
| 1 | Valid lead | VALID / NEW, one row, score and Arabic draft |
| 2 | Duplicate | Exact phone updates one row, touch_count increments |
| 3 | Missing lead_id | missing_lead_id; NOT_SAVED |
| 4 | Whitespace lead_id | Three spaces: missing_lead_id; NOT_SAVED |
| 5 | Invalid phone | abc: invalid_phone; NOT_SAVED |
| 6 | Empty optional fields | Accepted with deterministic defaults; no corruption |
| 7 | Long text | Synthetic long string; no crash; inspect output |
| 8 | Valid LOW | Unknown service/source + empty time: 0 / LOW |
| 9 | Valid MEDIUM | أسنان + واتساب + مساء: 55 / MEDIUM |
| 10 | Valid HIGH | تجميل + حجز مباشر + مساء: 75 / HIGH; no immediate-contact promise |
| 11 | Multiple leads | Three independent sequential executions; no contamination |
| 12 | Repeat run | Repeat one exact phone; same row count, updated fields |
| 13 | Mixed Arabic/English | Readable text and substituted placeholders |
| 14 | Extra unknown field | Not persisted in the saved mapping |
| 15 | Actual null phone | JSON null, not the string null: invalid_phone; no write |

Inspect Owner Review: lead_id, name, phone, service_type, source, score, priority, validation_status, record_status, result, reject_reason, draft_message, sla_minutes. Inspect the table before/after: rejected inputs do not write; repeats do not add a row; touch_count increments and last_seen updates; other test rows retain their values.

Multiple leads in this release were tested sequentially, not as a simultaneous batch. Null phone was verified; arbitrary object/number values in optional text fields are outside the input contract. If you change input mode for an actual null test, save the workflow first because mode switching may remove assignments. Restore the original sample after testing.

Inspect the nine supplied nodes to confirm no outbound sending/payment/API action has been added. Report deviations using sanitized evidence. Do not clear rows to manufacture a passing result.
