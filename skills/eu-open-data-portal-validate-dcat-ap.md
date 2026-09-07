---
name: eu-open-data-portal-validate-dcat-ap
description: Validate a DCAT-AP RDF graph against the official EU SHACL shapes before publishing it to data.europa.eu, and read the SHACL report.
api: eu-open-data-portal:eu-open-data-portal-mqa-shacl-validation-api
operations:
  - validationReport
generated: '2026-09-07'
method: generated
source: openapi/eu-open-data-portal-mqa-shacl-openapi.yaml
---

# Validate DCAT-AP metadata

Base URL: `https://data.europa.eu/api/mqa/shacl`. Anonymous; nothing you send is stored.

## The one operation

`POST /validation/report` (`validationReport`) — send a DCAT-AP graph, receive a SHACL validation report.

Parameters from the published contract:

- `shapeModel` — which DCAT-AP shape version to validate against. Set it to `customized` to use the `customized` parameter below.
- `customized` — an array combining aspects, valid only when `shapeModel=customized` (otherwise ignored). Customised models always run against the latest DCAT-AP SHACL shapes:
  - `range` — evaluate the range (class) of resources
  - `recommended` — warn about missing recommended fields
  - `vocabularies` — check correct use of the controlled vocabularies

## Why to run it first

This is the only genuine dry-run surface in the portal's API set. Publishing is a `PUT` upsert straight into the EU's public metadata record; a SHACL report costs one request and tells you what the MQA scorer will penalise before anything is written.

Pair it with the vocabularies endpoint (`GET https://data.europa.eu/api/hub/search/vocabularies/{vocabulary}`) — the `vocabularies` aspect fails exactly on values that are not in those authority tables.

## Rules

- Serialise the graph in any common RDF format the registry accepts: Turtle, RDF/XML, JSON-LD, N-Triples, TriG or N3.
- `400` means the graph could not be parsed — fix the serialisation before reading the report.
- A clean report is not a guarantee of a good MQA score: SHACL checks conformance, while the MQA additionally scores accessibility (are the distribution URLs reachable?) and contextuality.
