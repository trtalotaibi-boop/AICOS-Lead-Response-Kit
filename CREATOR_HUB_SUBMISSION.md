# n8n Creator Hub Submission Copy

## Title
Clinic Lead Qualification & Priority Scoring — No AI API Required

## Short description
Validate clinic leads, calculate a configurable qualification score, assign HIGH/MEDIUM/LOW priority, and produce a clean owner-review output — without external AI APIs or credentials.

## Problem
Clinics and small teams often receive inquiries from multiple sources but lack a simple, repeatable way to decide which leads need attention first.

## What this workflow does
1. Starts with a sample clinic lead.
2. Loads configurable service and source weights.
3. Validates the lead ID and phone format.
4. Calculates a lead score.
5. Assigns HIGH, MEDIUM, or LOW priority.
6. Returns a clean owner-review result.

## Setup
No credentials are required for the FREE workflow. Import the JSON, edit the sample lead or scoring weights if desired, and run Manual Trigger.

## Example output
```json
{
  "lead_id": "DEMO-0001",
  "name": "Demo Lead",
  "service_type": "Dental",
  "score": 55,
  "priority": "MEDIUM",
  "valid": true,
  "reject_reason": null
}
```

## Good for
Clinics, small businesses, agencies, and n8n users who want a lightweight lead-qualification starting point.

## Notes
The FREE version intentionally excludes persistence, duplicate detection/upsert, full follow-up preparation, SLA/channel logic, and the commercial documentation.

Repository: https://github.com/trtalotaibi-boop/AICOS-Lead-Response-Kit
