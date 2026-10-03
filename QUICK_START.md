# Quick Start — AICOS Clinics Edition v1.0 Free Beta

Use a fresh test environment and synthetic leads. No payment or paid API is required.

1. **Import:** Use **Import from File** and choose `workflow.json`. Confirm nine nodes; the legacy internal title ends in `SELLABLE`. Keep it inactive/unpublished.
2. **Create the table:** Create `aicos_clinic_leads`. Add all 13 custom columns from [DATA_TABLE_SCHEMA.md](DATA_TABLE_SCHEMA.md): ten String, two Number, one Date/Time. Do not create the system columns.
3. **Verify binding:** In **Find Existing Lead** and **Save Lead (Upsert)**, confirm the new table resolves by name. If it does not, select it in both nodes and refresh/check the mapped columns. Phone matching must use `phone` Equals the sample phone expression.
4. **Review defaults:** Open **Clinic Config**. Check weights, thresholds and draft wording, particularly the LOW within-one-business-day phrase. Use the original sample in **Lead Input (Sample)**.
5. **Execute:** Run the manual workflow. Owner Review should show `VALID`, `NEW`, score `55`, priority `MEDIUM`, result `محفوظ`, an Arabic draft and SLA `30`. The table should contain one row, `touch_count = 1` and a timestamp in `last_seen`.
6. **Repeat:** Execute the same phone again. Expect `UPDATED_EXISTING`, `مكرر — تم التحديث`, the same row count and `touch_count = 2`.
7. **Reject:** Change only `lead_id` to three spaces and execute. Expect `REJECTED`, `NOT_SAVED`, `missing_lead_id`, no draft and no new row. Restore the sample afterward.

The sample phone is fictional test data, not a contact instruction. This workflow prepares output only; it never sends a message. See [FULL_SETUP_GUIDE.md](FULL_SETUP_GUIDE.md), [TEST_CHECKLIST.md](TEST_CHECKLIST.md) and [TROUBLESHOOTING.md](TROUBLESHOOTING.md).
