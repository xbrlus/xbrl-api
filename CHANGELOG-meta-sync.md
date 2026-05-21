# xbrlapi.yaml Changes — Meta Endpoint Sync

**Date:** 2026-05-21
**Source of truth:** `/api/v1/meta/{object}` endpoints (18 objects)
**Files updated:** `xbrlapi.yaml`, `xbrlapi.json`
**Scope:** 580 insertions, 73 deletions across endpoint parameters, field enum schemas, and component definitions

---

## Summary

Updated `xbrlapi.yaml` to include all filter (searchable) and field options as defined by the live `/meta` query responses from the XBRL US API. The meta endpoints were fetched for all 18 objects: `fact`, `report`, `entity`, `assertion`, `dts`, `concept`, `label`, `cube`, `dimension`, `document`, `relationship`, `network`, `dts/concept`, `dts/network`, `entity/report`, `network/relationship`, `report/fact`, and `report/network`.

---

## New Parameters Added to `components/parameters`

The following parameter definitions were created to support filters that exist in the API but were previously missing from the spec:

| Parameter | Type | Description |
|-----------|------|-------------|
| `concept.balance-type_Param` | string | Balance type of a concept (debit, credit, or not defined) |
| `concept.is-abstract_Param` | boolean | Whether the concept is abstract |
| `cube.member-value_Param` | string | Typed value or local-name of the member |
| `document.documentset_Param` | boolean | Whether the document is part of the document set |
| `document.id_Param` | integer | Internal unique identifier of the document |
| `entity.code_Param` | array[string] | Entity identifier for any source (superset of CIK) |
| `entity.scheme_Param` | string | Identifier scheme (e.g., SEC CIK, LEI) |
| `entity.ticker2_Param` | array[string] | Stock exchange ticker |
| `fact.numerical-value_Param` | number | Numerical value of the fact |
| `footnote.role_Param` | string | Role used for the footnote |
| `footnote.text_Param` | string | Text content of the footnote |
| `network.role-description-like_Param` | string | Text search on network role description |
| `period.instant_Param` | date | Instant measurement date for the fact |
| `relationship.target-label_Param` | string | Label of the target concept in a relationship |
| `report.accepted-timestamp_Param` | date-time | Date report was accepted at the regulator |
| `report.base-taxonomy_Param` | string | Base taxonomy used for the filing |
| `report.checks-run_Param` | boolean | Whether DQC checks have run |
| `report.documentset-num_Param` | integer | Number of inline XBRL documents |
| `report.event-items_Param` | string | Event items associated with the report |
| `report.form-type_Param` | string | FERC report document type |
| `report.hash_Param` | string | Hash unique to each filing |
| `report.html-url_Param` | string | URL of the HTML version of the report |
| `report.period-focus_Param` | string | Period the report was reported for |
| `report.submission-type_Param` | string | FERC filing identifier (O = Original, R = Restated) |
| `report.year-focus_Param` | string | Year the report was reported for |
| `report.zip-url_Param` | string | URL of the filing ZIP file |

## New Schema Definitions Added to `components/schemas`

| Schema | Type | Description |
|--------|------|-------------|
| `entity_code` | string | Entity identifier for any source |
| `entity_ticker2` | string | Stock exchange ticker |
| `footnote_role` | string | Footnote role |
| `footnote_text` | string | Footnote text content |
| `relationship_target-label` | string | Label of target concept in relationship |
| `report_event-items` | string | Event items associated with the report |
| `report_form-type` | string | FERC report document type |
| `report_html-url` | string (uri) | URL of HTML version of report |
| `report_period-focus` | string | Period the report was reported for |
| `report_submission-type` | string | FERC filing identifier |
| `report_year-focus` | string | Year the report was reported for |
| `report_zip-url` | string (uri) | URL of filing ZIP file |

---

## Endpoint Filter Changes

### `/api/v1/fact/search`
Added filters: `concept.balance-type`, `entity.code`, `entity.name`, `entity.scheme`, `fact.numerical-value`, `footnote.role`, `footnote.text`, `period.instant`, `report.documentset-num`, `report.event-items`, `report.form-type`, `report.hash`, `report.html-url`, `report.is-most-current`, `report.period-focus`, `report.submission-type`, `report.year-focus`

### `/api/v1/fact/oim/search`
Added filters: `concept.balance-type`, `entity.code`, `entity.name`, `entity.scheme`, `fact.numerical-value`, `footnote.role`, `footnote.text`, `period.instant`, `report.document-type`, `report.document-index`, `report.documentset-num`, `report.event-items`, `report.form-type`, `report.hash`, `report.html-url`, `report.is-most-current`, `report.period-focus`, `report.submission-type`, `report.year-focus`

### `/api/v1/report/search`
Added filters: `entity.code`, `entity.name`, `entity.scheme`, `entity.ticker2`, `report.accepted-timestamp`, `report.base-taxonomy`, `report.checks-run`, `report.creation-software`, `report.documentset-num`, `report.event-items`, `report.form-type`, `report.hash`, `report.html-url`, `report.period-focus`, `report.period-index`, `report.submission-type`, `report.year-focus`, `report.zip-url`

### `/api/v1/report/{report.id}/fact/search`
Added filters: `concept.balance-type`, `entity.code`, `entity.name`, `entity.scheme`, `fact.numerical-value`, `footnote.role`, `footnote.text`, `period.instant`, `report.accepted-timestamp`, `report.base-taxonomy`, `report.checks-run`, `report.document-type`, `report.document-index`, `report.documentset-num`, `report.entity-name`, `report.entry-type`, `report.event-items`, `report.filer-category`, `report.form-type`, `report.hash`, `report.html-url`, `report.is-most-current`, `report.period-focus`, `report.period-index`, `report.submission-type`, `report.year-focus`, `report.zip-url`

### `/api/v1/report/fact/search`
Added filters: `concept.balance-type`, `dimensions.count`, `entity.code`, `entity.name`, `entity.scheme`, `entity.ticker`, `entity.ticker2`, `fact.numerical-value`, `footnote.role`, `footnote.text`, `period.instant`, `report.accepted-timestamp`, `report.base-taxonomy`, `report.checks-run`, `report.documentset-num`, `report.event-items`, `report.form-type`, `report.hash`, `report.html-url`, `report.period-focus`, `report.submission-type`, `report.year-focus`, `report.zip-url`

### `/api/v1/entity/search`
Added filters: `entity.code`, `entity.ticker2`

### `/api/v1/entity/{entity.id}/report/search`
Added filters: `report.accepted-timestamp`, `report.base-taxonomy`, `report.checks-run`, `report.creation-software`, `report.documentset-num`, `report.entity-name`, `report.event-items`, `report.form-type`, `report.hash`, `report.html-url`, `report.period-focus`, `report.submission-type`, `report.year-focus`, `report.zip-url`

### `/api/v1/entity/report/search`
Added filters: `entity.code`, `entity.name`, `entity.scheme`, `entity.ticker2`, `report.accepted-timestamp`, `report.base-taxonomy`, `report.checks-run`, `report.creation-software`, `report.documentset-num`, `report.event-items`, `report.form-type`, `report.hash`, `report.html-url`, `report.period-focus`, `report.submission-type`, `report.year-focus`, `report.zip-url`

### `/api/v1/assertion/search`
Added filters: `entity.cik`, `entity.code`, `entity.scheme`, `report.base-taxonomy`, `report.form-type`, `report.period-focus`, `report.year-focus`, `report.zip-url`

### `/api/v1/dts/search`
Added filter: `report.hash`

### `/api/v1/cube/search`
Added filters: `concept.balance-type`, `cube.member-value`, `entity.code`, `entity.id`, `fact.accuracy-index`, `fact.numerical-value`, `fact.ultimus`, `footnote.role`, `footnote.text`, `report.base-taxonomy`, `report.document-type`, `report.entity-name`, `report.source-id`, `report.source-name`, `report.year-focus`

### `/api/v1/dimension/search`
Added filters: `report.document-type`, `report.id`, `report.source-id`, `report.source-name`

### `/api/v1/document/search`
Added filters: `document.documentset`, `document.id`, `entity.cik`, `entity.code`, `entity.name`, `entity.scheme`, `report.hash`, `report.id`, `report.source-id`, `report.source-name`

### `/api/v1/label/{dts.id}/search` and `/api/v1/label/search`
Added filter: `concept.is-abstract`

### `/api/v1/network/{network.id}/relationship/search` and `/api/v1/network/relationship/search`
Added filters: `network.role-description-like`, `relationship.target-label`

### `/api/v1/relationship/search` and `/api/v1/relationship/tree/search`
Added filters: `network.role-description-like`, `relationship.target-label`

### `/api/v1/dts/{dts.id}/network/search`
Added filters: `network.role-description`, `network.role-description-like`, `relationship.target-is-abstract`, `relationship.target-label`

---

## Field Enum Schema Changes

### `fact_fields`
Added: `aspect`, `dimension-pair`, `entity.code`, `footnote.id`, `footnote.lang`, `footnote.role`, `footnote.text`, `report.documentset-num`, `report.event-items`, `report.form-type`, `report.hash`, `report.html-url`, `report.is-most-current`, `report.period-focus`, `report.submission-type`, `report.year-focus`

### `report_fields`
Added: `entity.code`, `entity.name`, `entity.scheme`, `entity.ticker2`, `report.checks-run`, `report.documentset-num`, `report.event-items`, `report.form-type`, `report.hash`, `report.html-url`, `report.period-focus`, `report.submission-type`, `report.year-focus`, `report.zip-url`

### `entity_only_fields`
Added: `entity.code`, `entity.ticker2`

### `entity_fields`
Added: `entity.code`, `entity.ticker2`, `report.checks-run`, `report.documentset-num`, `report.event-items`, `report.form-type`, `report.hash`, `report.html-url`, `report.period-focus`, `report.submission-type`, `report.year-focus`, `report.zip-url`

### `assertion_fields`
Added: `entity.code`, `entity.scheme`, `report.form-type`, `report.period-focus`, `report.year-focus`, `report.zip-url`

### `dts_fields`
Added: `report.hash`

### `cube_fields`
Added: `concept.balance-type`, `cube.member-value`, `dimension-pair`, `entity.code`, `entity.id`, `fact.accuracy-index`, `fact.inline-negated`, `fact.ultimus`, `footnote.id`, `footnote.lang`, `footnote.role`, `footnote.text`, `report.base-taxonomy`, `report.document-type`, `report.entity-name`, `report.source-id`, `report.source-name`, `report.year-focus`

### `dimension_fields`
Added: `report.document-type`, `report.id`, `report.source-id`, `report.source-name`

### `document_fields`
Added: `document.content`, `document.documentset`, `document.id`, `document.text-search`, `dts.content`, `entity.cik`, `entity.code`, `entity.name`, `entity.scheme`, `report.filing-date`, `report.hash`, `report.id`, `report.source-id`, `report.source-name`

### `label_fields`
Added: `concept.is-abstract`

### `network_fields`
Added: `network.role-description-like`

### `network_con_relationship_fields`
Added: `network.role-description-like`, `relationship.target-label`

### `relationship_fields`
Added: `network.role-description-like`, `relationship.target-label`

### `report_and_fact_fields`
Added: `aspect`, `dimension-pair`, `entity.code`, `entity.ticker`, `entity.ticker2`, `fact.accuracy-index` (reordered), `footnote.id`, `footnote.lang`, `footnote.role`, `footnote.text`, `report.checks-run`, `report.documentset-num`, `report.event-items`, `report.form-type`, `report.hash`, `report.html-url`, `report.period-focus`, `report.submission-type`, `report.type`, `report.year-focus`, `report.zip-url`

---

## Other Changes

- Fixed `report/fact/search` fields schema reference from `report_details_with_facts` to `report_and_fact_fields` (consistent with `report/{report.id}/fact/search`)
- Normalized trailing whitespace and blank lines throughout edited sections
- Alphabetized parameter references within endpoints for consistency
