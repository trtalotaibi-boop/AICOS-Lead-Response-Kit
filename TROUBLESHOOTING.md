# Troubleshooting — AICOS Clinics Edition v1.0 Free Beta

These checks address observed setup/input behavior and failure modes directly implied by the shipped mappings. Do not delete existing data to resolve a setup problem.

| Symptom | Check and action |
|---|---|
| Table unresolved after import | Create `aicos_clinic_leads` with all 13 columns. Confirm name resolution; re-select it in both Data Table nodes if needed. |
| Mappings missing/wrong column | Resolve the table first, refresh/check mappings, then verify phone Equals and numeric/date types. Preserve expressions. |
| Save fails on score/touch_count | Check both are Number. Build a correct separate test table instead of deleting production columns. |
| A repeat creates a new row | Compare exact phone strings, plus prefix and whitespace. There is no normalization. lead_id is not the duplicate key. |
| touch_count stays 1 | Check exact-phone match, existing row and Number type; inspect both lookup and upsert conditions. |
| status changes unexpectedly | Verify the shipped status_final mapping preserves the existing status. Compare your copy with the unchanged package. |
| Lead rejected | Inspect reject_reason. missing_lead_id requires a non-whitespace string; invalid_phone requires optional plus and 8–15 ASCII digits. |
| Low score with otherwise valid input | Unknown/empty service/source contribute zero. Match keys exactly to Clinic Config. |
| Empty time renders غير محدد | Expected fallback. Supply a string preferred_time if available. |
| Literal placeholders appear | Restore exact double-brace placeholders in Clinic Config. |
| Manual assignments disappeared after changing input mode | Mode switching can discard assignments. Recover from your saved export in a separate workflow; edit values within Manual Mapping for normal tests. |
| The workflow does not run automatically | Expected: Manual Trigger only. Keep inactive/unpublished and use Execute Workflow. |

If unresolved, use Setup Problem or Bug Report after repository publication. Include n8n version, install type, node, expected/actual result and synthetic reproduction steps. Screenshots are optional and must be sanitized. Do not post full execution dumps containing customer records or secrets.
