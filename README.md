# AICOS Lead Response Kit — Clinics Edition v1.0

**Free Beta · Manual n8n workflow · Arabic follow-up drafts**

Validate, score and review a synthetic clinic lead in your own n8n environment. Repeat entries with the same phone update the existing record. The beta is free to try; no payment or paid API is required. Separate hosting costs, if you choose a paid host, are your responsibility.

## The problem and the workflow

Lead details can be inconsistent, repeated and difficult to review. This template provides a repeatable way to check the supplied identifier and phone format, assign a configured priority, store the record and prepare a draft for human review.

```text
Manual Trigger → Clinic Config → Lead Input (Sample) → Normalize & Score
  → Valid Lead?
    accepted → Find Existing Lead → Prepare Follow-Up → Save Lead (Upsert)
    rejected → no table write
  → Owner Review Output
```

## What it does

- Checks a non-whitespace string `lead_id` and phone format.
- Adds configured service, source and preferred-time points.
- Assigns LOW, MEDIUM or HIGH, with an informational SLA preview.
- Looks up and upserts by exact phone string in `aicos_clinic_leads`.
- Preserves existing status, increments `touch_count` and updates `last_seen`.
- Shows identity, source, score, validation, priority, record state, result and rejection reason.
- Prepares an editable Arabic draft for accepted leads.

It has no automatic Email, WhatsApp or SMS send, no AI/LLM calls, no external CRM integration and no payment step. It does not validate email, verify phone ownership, schedule an actual callback or guarantee business results.

## Prerequisites

- An n8n instance with Data Tables and permission to import workflows/create tables.
- A separate test table and synthetic data for evaluation.
- No paid API, credentials or messaging account required by the supplied workflow.

The legacy documentation lists n8n 2.31.5 as a historical target; the exact version of the latest isolated test was not captured. Compatibility is therefore not claimed across all versions. Verify import and the checklist in your own installed version.

## Installation

1. Import `workflow.json` using n8n's **Import from File** action.
2. Keep the workflow inactive/unpublished. Its trigger is manual.
3. Create `aicos_clinic_leads` using all 13 custom columns in [DATA_TABLE_SCHEMA.md](DATA_TABLE_SCHEMA.md). n8n adds `id`, `createdAt` and `updatedAt`.
4. Confirm both **Find Existing Lead** and **Save Lead (Upsert)** resolve this table by name. If unresolved, re-select the new table in both nodes and verify mappings.
5. Review **Clinic Config**, including the wording and response-time expectations in the templates.
6. Execute the shipped sample and inspect **Owner Review Output** and the table.
7. Repeat the same sample to verify an update rather than another row. Run an invalid sample to verify no write.

See [QUICK_START.md](QUICK_START.md) and [FULL_SETUP_GUIDE.md](FULL_SETUP_GUIDE.md). The JSON retains the legacy internal workflow title ending in `SELLABLE`; product availability is Free Beta. The exported logic is unchanged.

## Sample input

The included sample is synthetic. Never contact its example phone number.

```json
{
  "lead_id": "LEAD-T2-0001",
  "name": "سارة",
  "phone": "+966500000001",
  "service_type": "أسنان",
  "source": "واتساب",
  "message": "أريد حجز موعد أسنان",
  "preferred_time": "مساء",
  "branch": "الفرع الرئيسي"
}
```

## Expected output and owner review

For the first run in an empty table:

```json
{
  "lead_id": "LEAD-T2-0001",
  "name": "سارة",
  "phone": "+966500000001",
  "source": "واتساب",
  "service_type": "أسنان",
  "score": 55,
  "priority": "MEDIUM",
  "validation_status": "VALID",
  "record_status": "NEW",
  "result": "محفوظ",
  "reject_reason": null,
  "draft_message": "مرحبًا سارة، شكرًا لتواصلك بخصوص أسنان. سنتواصل معك قريبًا لتأكيد موعدك المفضل (مساء).",
  "sla_minutes": "30"
}
```

The table records `touch_count = 1` and a generated `last_seen`. A repeated exact phone shows `UPDATED_EXISTING` and `مكرر — تم التحديث`; the row count stays the same and `touch_count` increases. Owner output and stored table fields are separate; `sla_minutes` is exported as a string in Owner Review.

## Validation and deduplication

`lead_id` must be a string containing a non-whitespace character. `phone` must be a string matching `^\+?[0-9]{8,15}$`. Missing/blank identifiers reject with `missing_lead_id`; invalid phones reject with `invalid_phone`. Rejected leads are not saved and have no draft/SLA in Owner Review. Scores may still be computed before rejection; rejected leads are not proof of successful scoring.

Name, service, source and other optional fields are not acceptance gates. Supply strings for provided text fields; arbitrary objects and numbers are outside the documented contract. Empty optional fields are allowed. Unknown service/source values add zero points. There is no trimming or phone normalization: a plus-prefixed phone and the same digits without plus are separate keys. `lead_id` is not a unique key. Existing duplicate rows are not automatically merged, and concurrent-write safety has not been established.

## Default scoring

Score = service points + source points + 5 if preferred time is nonempty.

| Component | Values |
|---|---|
| Service | تجميل 40; أسنان 30; استشارة 20; unknown 0 |
| Source | حجز مباشر 30; واتساب 20; إنستغرام 15; unknown 0 |
| Priority | HIGH ≥70; MEDIUM ≥40 and <70; LOW <40 |
| Informational SLA | HIGH 5; MEDIUM 30; LOW 120 minutes |

Accepted test vectors: unknown service/source with empty time = **0/LOW**; أسنان + واتساب + مساء = **55/MEDIUM**; تجميل + حجز مباشر + مساء = **75/HIGH**. These are rule-based priorities, not predictions of conversion or medical urgency.

## Arabic drafts and limitations

Drafts substitute `name`, `service_type` and `preferred_time`; empty time uses `غير محدد`. Review the text before any manual use. The HIGH default says the team will contact the lead to confirm the appointment and does not promise immediate contact. The LOW default contains a within-one-business-day phrase: change that configuration if your clinic cannot honor it. SLA values are previews; no scheduler or response guarantee is implemented.

The shipped workflow processes a sample lead manually. Multiple leads were verified through separate executions, not a simultaneous batch or intake integration. No patient record system, consent management, automated intake, telemetry or email validation is included.

## Test status

The owner's accepted isolated local verification on 2026-10-03 reports **15/15 regression cases passed**, accepted LOW/MEDIUM/HIGH, exact-phone update, Owner Review and Arabic drafts. **Clean install passed**, outbound send was **NONE**, and the live instance was unchanged. This is maintainer evidence for the tested setup, not a compatibility guarantee. Case 11 used three separate executions. The release candidate preserves the tested workflow bytes. See [TEST_CHECKLIST.md](TEST_CHECKLIST.md).

## Security and feedback

Data stays in your configured n8n table and execution logs according to your environment's settings. The supplied workflow contains no outbound send or external API node. Check permissions, backups and retention before evaluating suitability for real data. Use synthetic records until you have validated that suitability.

After the owner publishes the repository, use its **Issues → New issue** chooser for Bug Report, Setup Problem, Feature Request or General Feedback. Until then, use the copyable template in [BETA_FEEDBACK.md](BETA_FEEDBACK.md). Never share customer/patient data, credentials, private phone lists or API keys. There is no hidden usage tracking.

## Free Beta usage and next steps

See [FREE_BETA.md](FREE_BETA.md) and [LICENSE_OR_USAGE_TERMS.md](LICENSE_OR_USAGE_TERMS.md). No payment is required. The beta is intended for evaluation and feedback; future plans may change without a pricing promise. Support has no guaranteed response time.

The immediate plan is to collect installation outcomes and prioritize documented setup problems. No additional feature or delivery date is promised.
