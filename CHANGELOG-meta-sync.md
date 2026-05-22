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
| `concept.balance-type` | string | The balance type of a concept. This can be either debit, credit or not defined. |
| `concept.is-abstract` | boolean | Identifies if the concept is an abstract concept. If a primary concept (Not an axis or dimension) is an abstract it cannot have a value associated with it. |
| `cube.member-value` | string | Typed value or local-name of the member depending on the dimension type. |
| `document.documentset` | boolean | Boolean attribute that indicates if the document is part of the document set, i.e. an inline document. |
| `document.id` | integer | An internal unique identifier of the document. |
| `entity.code` | array[string] | The entity identifier from its associated source (ie. SEC entity codes are the Central Index Code or CIK; FERC entity codes are Company Identifier or CID). All entity identifiers are in this field. |
| `entity.scheme` | string | The scheme of the identifier associated with a fact, report or DTS. A fact could have multiple entity identifiers and this indicates the identifier that was used. |
| `fact.numerical-value` | number | The numerical value of the fact that was reported. |
| `footnote.role` | string | The role used for the footnote. |
| `footnote.text` | string | The text content of the footnote. |
| `network.role-description-like` | string | The human readable description of the network role. This is used to do a text search on components of the text string. |
| `period.instant` | date | Instant in time at which the fact was measured, only applicable for facts with a period type of instant. |
| `relationship.target-label` | string | The label of the concept under the source relationship. |
| `report.accepted-timestamp` | date-time | Date that the report was accepted at the regulator. |
| `report.base-taxonomy` | string | Base taxonomy used for the filing, i.e. US-GAAP 2020. |
| `report.documentset-num` | integer | The number of inline xbrl documents associated with the filing. |
| `report.event-items` | string | The SEC 8-K event items associated with the report - see https://xbrl.us/8-k-items. |
| `report.hash` | string | A hash string that is generated based on the semantic meaning of the report. Two identical reports expressed as XBRL JSON, XML or inline XBRL will have an identical hash string. This makes it possible to determine if a report is a duplicate. |
| `report.html-url` | string | The URL of the HTML version of the report. |
| `report.period-focus` | string | The period the report was reported for. |
| `report.submission-type` | string | A FERC filing identifier indicating if it's the first time it was filed or a subsequent one. (O = Original; R = Restated) |
| `report.year-focus` | string | The reporting year for the filing. |
| `report.zip-url` | string | The url where the zip containing all the files of a filing can be accessed. |

## New Schema Definitions Added to `components/schemas`

| Schema | Type | Description |
|--------|------|-------------|
| `entity.code` | string | The entity identifier from its associated source (ie. SEC entity codes are the Central Index Code or CIK; FERC entity codes are Company Identifier or CID). All entity identifiers are in this field. |
| `footnote.text` | string | The text content of the footnote. |
| `relationship.target-label` | string | The label of the concept under the source relationship. |
| `report.event-items` | string | The event items associated with the report. |
| `report.html-url` | string (uri) | The URL of the HTML version of the report. |
| `report.period-focus` | string | The period the report was reported for. |
| `report.submission-type` | string | A FERC filing identifier indicating if it's the first time it was filed or a subsequent one. (O = Original; R = Restated) |
| `report.year-focus` | string | The reporting year for the filing. |
| `report.zip-url` | string (uri) | The url where the zip containing all the files of a filing can be accessed. |

---

## Endpoint Filter Changes

### `/api/v1/fact/search`
Added filters: `concept.balance-type`, `entity.code`, `entity.name`, `entity.scheme`, `fact.numerical-value`, `footnote.role`, `footnote.text`, `period.instant`, `report.documentset-num`, `report.event-items`, `report.hash`, `report.html-url`, `report.is-most-current`, `report.period-focus`, `report.submission-type`, `report.year-focus`

### `/api/v1/fact/oim/search`
Added filters: `concept.balance-type`, `entity.code`, `entity.name`, `entity.scheme`, `fact.numerical-value`, `footnote.role`, `footnote.text`, `period.instant`, `report.document-type`, `report.document-index`, `report.documentset-num`, `report.event-items`, `report.hash`, `report.html-url`, `report.is-most-current`, `report.period-focus`, `report.submission-type`, `report.year-focus`

### `/api/v1/report/search`
Added filters: `entity.code`, `entity.name`, `entity.scheme`, `report.accepted-timestamp`, `report.base-taxonomy`, `report.creation-software`, `report.documentset-num`, `report.event-items`, `report.hash`, `report.html-url`, `report.period-focus`, `report.period-index`, `report.submission-type`, `report.year-focus`, `report.zip-url`

### `/api/v1/report/{report.id}/fact/search`
Added filters: `concept.balance-type`, `entity.code`, `entity.name`, `entity.scheme`, `fact.numerical-value`, `footnote.role`, `footnote.text`, `period.instant`, `report.accepted-timestamp`, `report.base-taxonomy`, `report.document-type`, `report.document-index`, `report.documentset-num`, `report.entity-name`, `report.entry-type`, `report.event-items`, `report.filer-category`, `report.hash`, `report.html-url`, `report.is-most-current`, `report.period-focus`, `report.period-index`, `report.submission-type`, `report.year-focus`, `report.zip-url`

### `/api/v1/report/fact/search`
Added filters: `concept.balance-type`, `dimensions.count`, `entity.code`, `entity.name`, `entity.scheme`, `entity.ticker`, `fact.numerical-value`, `footnote.role`, `footnote.text`, `period.instant`, `report.accepted-timestamp`, `report.base-taxonomy`, `report.documentset-num`, `report.event-items`, `report.hash`, `report.html-url`, `report.period-focus`, `report.submission-type`, `report.year-focus`, `report.zip-url`

### `/api/v1/entity/search`
Added filters: `entity.code`

### `/api/v1/entity/{entity.id}/report/search`
Added filters: `report.accepted-timestamp`, `report.base-taxonomy`, `report.creation-software`, `report.documentset-num`, `report.entity-name`, `report.event-items`, `report.hash`, `report.html-url`, `report.period-focus`, `report.submission-type`, `report.year-focus`, `report.zip-url`

### `/api/v1/entity/report/search`
Added filters: `entity.code`, `entity.name`, `entity.scheme`, `report.accepted-timestamp`, `report.base-taxonomy`, `report.creation-software`, `report.documentset-num`, `report.event-items`, `report.hash`, `report.html-url`, `report.period-focus`, `report.submission-type`, `report.year-focus`, `report.zip-url`

### `/api/v1/assertion/search`
Added filters: `entity.cik`, `entity.code`, `entity.scheme`, `report.base-taxonomy`, `report.period-focus`, `report.year-focus`, `report.zip-url`

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
Added: `dimension-pair`, `entity.code`, `footnote.id`, `footnote.lang`, `footnote.role`, `footnote.text`, `report.documentset-num`, `report.event-items`, `report.hash`, `report.html-url`, `report.is-most-current`, `report.period-focus`, `report.submission-type`, `report.year-focus`

### `report_fields`
Added: `entity.code`, `entity.name`, `entity.scheme`, `report.documentset-num`, `report.event-items`, `report.hash`, `report.html-url`, `report.period-focus`, `report.submission-type`, `report.year-focus`, `report.zip-url`

### `entity_only_fields`
Added: `entity.code`

### `entity_fields`
Added: `entity.code`, `report.documentset-num`, `report.event-items`, `report.hash`, `report.html-url`, `report.period-focus`, `report.submission-type`, `report.year-focus`, `report.zip-url`

### `assertion_fields`
Added: `entity.code`, `entity.scheme`, `report.period-focus`, `report.year-focus`, `report.zip-url`

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
Added: `dimension-pair`, `entity.code`, `entity.ticker`, `fact.accuracy-index` (reordered), `footnote.id`, `footnote.lang`, `footnote.role`, `footnote.text`, `report.documentset-num`, `report.event-items`, `report.hash`, `report.html-url`, `report.period-focus`, `report.submission-type`, `report.type`, `report.year-focus`, `report.zip-url`

---

## Other Changes

- Fixed `report/fact/search` fields schema reference from `report_details_with_facts` to `report_and_fact_fields` (consistent with `report/{report.id}/fact/search`)
- Normalized trailing whitespace and blank lines throughout edited sections
- Alphabetized parameter references within endpoints for consistency
