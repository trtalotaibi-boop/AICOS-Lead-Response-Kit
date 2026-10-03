# v1.0 Free Beta — AICOS Lead Response Kit, Clinics Edition

An n8n workflow for manually evaluating clinic lead validation, rule-based scoring, LOW/MEDIUM/HIGH priority, exact-phone duplicate updates, Owner Review and Arabic follow-up drafts.

The product is free to try. No payment, paid API or credential is required by the supplied workflow. Separate hosting charges are not included.

## Verification

The owner accepted isolated local verification on 2026-10-03: 15/15 regression PASS; clean install PASS; accepted scores 0/LOW, 55/MEDIUM and 75/HIGH; deduplication, data integrity, Owner Review and Arabic drafts PASS. Outbound send: NONE. The live environment was unchanged. Multiple leads were verified through separate manual runs. The latest test n8n version was not recorded; test compatibility in your own version.

## Limits

Manual sample input only. No automatic messaging, AI/LLM call, email validation, live intake connector, phone normalization, scheduler or medical/business outcome guarantee. Exact-phone matching does not merge pre-existing duplicates; batch/concurrent writes are not verified. Drafts are suggestions: review all commitments, including the LOW within-one-business-day wording, before manual use.

Use synthetic records until you validate suitability for sensitive real customer/patient data and review your environment's access and retention. Do not post sensitive records or secrets in feedback.

Try the Quick Start, repeat a lead, test rejection and tell us what worked, failed or was unclear through the repository issue forms after publication. Beta evaluation terms are in LICENSE_OR_USAGE_TERMS.md. No future price or support-response commitment is promised.
