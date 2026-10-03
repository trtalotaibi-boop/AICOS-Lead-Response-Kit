# Free Beta FAQ — AICOS Clinics Edition v1.0

**Is there a price?** No. Evaluation is free; no payment or card is required. Paid hosting, if chosen separately, is not included.

**Does it send messages?** No. It prepares a draft for owner review. Sending is a separate human action.

**Does it call an AI service or paid API?** No. Scores and drafts use configured rules and templates. No credentials are required by the shipped workflow.

**What n8n version works?** You need Data Tables. Historical docs list 2.31.5; the latest isolated test version was not recorded. Test the import/checklist in your version. Cloud compatibility was not part of the isolated verification.

**Can I feed a form or WhatsApp conversation directly?** The supplied workflow uses a manual sample input. Intake integrations are outside this beta's tested scope.

**Does it validate email or verify phones?** No email validation exists. Phone checks are format checks only.

**What creates a duplicate?** The identical phone string. No normalization occurs, and lead_id is not unique. Existing duplicates are not merged automatically.

**Can I change weights or drafts?** Yes, in Clinic Config; rerun synthetic checks afterward. Review the LOW one-business-day wording before use.

**Can I run a batch?** The verified mode is one lead per manual execution. Three independent leads passed in separate runs; batch and concurrency are not established.

**Can I deploy it to clients or production?** The current grant is beta evaluation in your own test environment. Broader rights are not established; see LICENSE_OR_USAGE_TERMS.md.

**What about privacy?** Table and execution data follow your n8n configuration. There is no built-in external send or hidden telemetry; this alone does not establish production suitability.

**How do I get help?** Use the repository issue forms after publication or BETA_FEEDBACK.md. No support response time is promised. Use synthetic examples only.
