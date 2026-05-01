# EU Open Data Portal (eu-open-data-portal)

The EU Open Data Portal (data.europa.eu) is the official portal for European Union open data, operated by the Publications Office of the European Union. It provides SPARQL and REST APIs for accessing statistical datasets, legislative documents, and institutional data from EU institutions under open licenses.

**URL:** [Visit APIs.json URL](https://raw.githubusercontent.com/api-evangelist/eu-open-data-portal/refs/heads/main/apis.yml)

## Timestamps

- **Modified:** 2026-04-28

## APIs

### EU Open Data Portal SPARQL API

The EU Open Data Portal SPARQL endpoint provides structured queries against linked open data from European Union institutions. Based on OpenLink Virtuoso, the endpoint enables querying of RDF datasets using SPARQL with output in HTML, XML, JSON, Turtle, CSV, TSV, and other formats.

**Human URL:** [https://data.europa.eu/](https://data.europa.eu/)

**Base URL:** `https://data.europa.eu/sparql`

#### Tags

- EU, Government, Linked Data, Open Data, Regulatory, SPARQL

#### Properties

- [Documentation](https://data.europa.eu/sparql)
- [Reference](https://data.europa.eu/sparql)

### EU Open Data Portal Search API

The EU Open Data Portal Search API provides REST access for discovering and querying European open datasets following DCAT-AP metadata standards. The API supports dataset search, filtering, and harvesting workflows for data publishers and consumers.

**Human URL:** [https://data.europa.eu/](https://data.europa.eu/)

**Base URL:** `https://data.europa.eu/api/hub/search/`

#### Tags

- DCAT-AP, EU, Government, Open Data, REST, Search

#### Properties

- [Reference](https://data.europa.eu/api/hub/search/)
- [Documentation](https://dataeuropa.gitlab.io/data-provider-manual/)
- [OpenAPI](openapi/eu-open-data-portal-search-openapi.yml)

## Common Properties

- [Portal](https://data.europa.eu/)
- [Documentation](https://dataeuropa.gitlab.io/data-provider-manual/)
- [Getting Started](https://data.europa.eu/sparql)
- [Terms of Service](https://data.europa.eu/en/legal-notice)
- [Privacy Policy](https://data.europa.eu/en/legal-notice)
- [Website](https://data.europa.eu/)
- [OpenAPI](openapi/eu-open-data-portal-search-openapi.yml)
- [JSONSchema](json-schema/eu-open-data-portal-dataset-schema.json)
- [JSONLDContext](json-ld/eu-open-data-portal-context.jsonld)

## Maintainers

**FN:** Kin Lane

**Email:** kin@apievangelist.com
