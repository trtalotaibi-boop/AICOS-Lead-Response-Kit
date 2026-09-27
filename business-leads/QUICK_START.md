# AICOS Business Lead Opportunity Scorer — FREE

A lightweight n8n workflow for turning local-business lead data into a prioritized sales-opportunity queue.

## What it does

Input business data → normalize → validate → score opportunity → HIGH / MEDIUM / LOW priority → owner-review output.

The score considers available contact data, website presence, online booking, rating, and review volume. All weights are visible in the Code node and can be edited.

## Quick start

1. Download `AICOS_Business_Lead_Opportunity_Scorer_FREE.json`.
2. Import it into n8n.
3. Open **Business Lead Input** and replace the demo values.
4. Run **Start Business Lead Scoring**.
5. Read **Owner Review Output**.

Example from the runtime-tested build:

`Demo Local Business | Barbershop | Score: 80 | Priority: HIGH | Valid: true`

## Input fields

`business_name`, `category`, `city`, `phone`, `email`, `website`, `rating`, `reviews`, `online_booking`, `maps_url`, `source`.

## Important

This FREE workflow does **not** scrape Google Maps or other websites. It scores business-lead data that you provide or obtain from sources you are permitted to use.

No credentials and no external AI API are required.

The separate Clinics Edition remains available and unchanged.
