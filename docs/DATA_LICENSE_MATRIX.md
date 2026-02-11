# Data License Matrix

This matrix tracks legal/compliance constraints for external datasets considered for Thucydides.

> **Status legend**
> - **Approved**: legal reviewed and approved for intended use.
> - **Conditional**: can be used only if listed conditions are met.
> - **Blocked**: not permitted for current use.
> - **Pending review**: not yet reviewed by legal.


## Current development stance

For the current web-app planning phase, CIA World Factbook and Global Firepower are used as **reference inputs for defining baseline country-standing metrics**, not as directly embedded in-game content. Production ingestion remains gated by the compliance workflow below.

## Source-by-source matrix

| Source | Allowed uses | Attribution | Scraping / API rules | Commercial use | Sublicensing / redistribution | Current status | Notes / required actions |
|---|---|---|---|---|---|---|---|
| CIA World Factbook | Internal analysis, transformation into normalized indicators, in-app display of derived country profile metrics. Direct republication of large verbatim passages should be avoided until legal confirms scope. | Include source credit in app/legal page and internal provenance records. | Must verify current access terms before automated ingestion. Respect robots.txt and published technical limits if scraping is used. Prefer official bulk/API export if available. | **Pending review** (likely permissive for many U.S. government works, but must confirm any exceptions and embedded third-party content). | **Pending review**. Assume no sublicensing rights for third-party embedded content unless explicitly granted. | Pending review | Legal to confirm copyright/terms status for data, text, images, and seals/logos. Engineering to separate numeric indicators from media assets. |
| Global Firepower | Treat as restricted until explicit permission/license is obtained. Use only for evaluation prototyping in non-production if terms allow. | Likely requires visible attribution if any permitted use is granted by license. | Do **not** scrape or automate collection until terms explicitly permit it. Assume anti-scraping restrictions by default. | **Unknown / likely restricted** without commercial license. | **Unknown / likely prohibited** unless license explicitly allows redistribution/sublicensing. | Pending review | Contact provider for written commercial/data redistribution terms. Prepare replacement dataset path if licensing is denied or cost-prohibitive. |

## Field definitions for this matrix

- **Allowed uses**: Exactly what product behaviors are permitted (internal analytics, model training, user-facing display, caching, exports).
- **Attribution**: Mandatory citations, display location, and wording obligations.
- **Scraping / API rules**: Whether crawling/automation is allowed, rate limits, robots.txt obligations, and API key terms.
- **Commercial use**: Whether paid app/SaaS monetization is allowed.
- **Sublicensing / redistribution**: Whether data can be redistributed to end-users, partners, or downstream developers.

## Required compliance workflow (before production ingestion)

1. Capture a terms snapshot (URL/PDF + date) for each data source.
2. Record legal interpretation and risk rating in this file.
3. Define engineering guardrails (allowed fields, blocked fields, retention rules).
4. Implement provenance metadata in the pipeline:
   - `source_name`
   - `source_url`
   - `retrieval_timestamp`
   - `license_status`
   - `attribution_required`
   - `redistribution_allowed`
5. Block deploys for datasets marked **Blocked** or unresolved **Pending review**.

## Suggested fallback strategy

If a source remains restricted:

- Replace with open/permissively licensed alternatives for equivalent indicators.
- Keep provider adapters pluggable so restricted sources can be swapped with minimal downstream schema changes.
- Store method notes explaining indicator substitutions to preserve simulation transparency.
