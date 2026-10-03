# Configuration Guide — AICOS Clinics Edition v1.0 Free Beta

Edit **Clinic Config** after saving a copy of your workflow. Execute synthetic checks after configuration changes. The acceptance evidence covers the shipped defaults only.

| Setting | Default | Meaning |
|---|---|---|
| service_weights | تجميل 40; أسنان 30; استشارة 20 | Points by exact service key; unknown = 0 |
| source_weights | حجز مباشر 30; واتساب 20; إنستغرام 15 | Points by exact source key; unknown = 0 |
| preferred_time_bonus | 5 | Added for a nonempty supplied preferred time |
| priority_thresholds | high 70; medium 40 | HIGH ≥70; MEDIUM ≥40; otherwise LOW |
| sla_minutes | HIGH 5; MEDIUM 30; LOW 120 | Informational targets only |
| channels | HIGH اتصال هاتفي; MEDIUM/LOW واتساب | Informational labels; do not send |
| followup_templates | Arabic text by priority | Draft output for human review |

Keep numeric weights and thresholds numeric and medium below high. Service/source keys must match input values exactly. Keep template keys `high`, `medium`, `low` and placeholders `{{name}}`, `{{service_type}}`, `{{preferred_time}}`. Empty time renders `غير محدد`; empty name/service render blank strings.

Review every template for commitments your clinic can honor. HIGH does not promise immediate contact. LOW currently says within one business day, and MEDIUM says soon; these are editable wording, not guarantees implemented by the workflow. Nothing schedules or enforces the SLA.

Validation is computed in **Normalize & Score** and routed by **Valid Lead?**. Exact-phone lookup/upsert, cross-node expressions, status preservation and touch_count logic should remain unchanged during beta evaluation. Renaming referenced nodes may break expressions. Adding intake/sending nodes changes the verified scope. Report problems through the repository feedback forms after publication rather than assuming paid support exists.
