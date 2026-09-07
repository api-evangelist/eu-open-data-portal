# EU Open Data Portal (eu-open-data-portal)

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->
# EU Open Data Portal

data.europa.eu is the official portal for European open data, operated by the Publications Office of the European Union. It federates roughly 1.9 million dataset records from EU institutions, the national open data portals of the member states and international organisations, and republishes them as DCAT-AP metadata. Six machine-readable APIs sit on top of that corpus: a hub-search metadata search service, a hub-repo DCAT-AP registry for publishers, a Virtuoso SPARQL endpoint, and the Metadata Quality Assurance metrics cache, metrics reporter and SHACL validation services. Read access is public and unauthenticated; publishing into a catalogue requires an EU Login account or a service account issued by the portal team.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/eu-open-data-portal/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/eu-open-data-portal/refs/heads/main/apis.yml)

## Tags

- Government
- Open Data
- SPARQL
- EU
- Regulatory
- Linked Data
- DCAT-AP
- Data Quality
- Metadata
- Catalogs

## Timestamps

- **Created:** 2026-04-28
- **Modified:** 2026-09-07

## APIs

### EU Open Data Portal Search API (hub-search)

The hub-search metadata search service for data.europa.eu. Provides full-text and faceted search over ~1.9 million dataset, data service, dataset series, catalogue, vocabulary and organisation records harvested from EU institutions and national portals, plus Atom/RSS feeds, sitemaps, a gazetteer autocomplete and a CKAN-compatible package API. Read operations are public and unauthenticated; write operations require an API key or JWT bearer token.

- **Human URL:** [https://data.europa.eu/api/hub/search/](https://data.europa.eu/api/hub/search/)
- **Base URL:** `https://data.europa.eu/api/hub/search`

#### Tags

- Search
- Datasets
- Catalogues
- DCAT-AP
- Open Data
- CKAN

#### Properties

- [OpenAPI](openapi/eu-open-data-portal-hub-search-openapi.yaml)
- [APIReference](https://data.europa.eu/api/hub/search/)
- [Documentation](https://dataeuropa.gitlab.io/data-provider-manual/api-documentation/)
- [Overlay](overlays/eu-open-data-portal-hub-search-overlay.yaml)
- [SourceCode](https://gitlab.com/dataeuropa/hub/search)
- [Examples](https://gitlab.com/dataeuropa/api-usage-examples)

### EU Open Data Portal Registry API (hub-repo)

The piveau hub-repo registry service: the DCAT-AP write surface of data.europa.eu. Manages catalogues, DCAT resources (datasets, data services, dataset series), distributions, drafts, vocabularies, quality metrics and persistent identifiers in the Virtuoso triplestore, in RDF/XML, Turtle, JSON-LD, N-Triples, N-Quads, TriG, TriX and N3. Writes require a catalogue-scoped API key or an EU Login / service-account party token.

- **Human URL:** [https://data.europa.eu/api/hub/repo/](https://data.europa.eu/api/hub/repo/)
- **Base URL:** `https://data.europa.eu/api/hub/repo`

#### Tags

- Registry
- DCAT-AP
- RDF
- Catalogues
- Publishing

#### Properties

- [OpenAPI](openapi/eu-open-data-portal-hub-repo-openapi.yaml)
- [APIReference](https://data.europa.eu/api/hub/repo/)
- [Documentation](https://dataeuropa.gitlab.io/data-provider-manual/api-documentation/)
- [Overlay](overlays/eu-open-data-portal-hub-repo-overlay.yaml)
- [SourceCode](https://gitlab.com/dataeuropa/hub/repo)
- [ChangeLog](https://gitlab.com/dataeuropa/hub/repo/-/blob/main/CHANGELOG.md)

### EU Open Data Portal MQA Metrics Cache API

The Metadata Quality Assurance (MQA) metrics cache. Serves DCAT-AP quality scores for every catalogue, country, dataset and distribution across five dimensions — findability, accessibility, interoperability, reusability and contextuality — on a 450-point scale, with historic series, distribution reachability and SHACL violation reports. Read operations are public; admin refresh operations require an API key.

- **Human URL:** [https://data.europa.eu/api/mqa/cache/](https://data.europa.eu/api/mqa/cache/)
- **Base URL:** `https://data.europa.eu/api/mqa/cache`

#### Tags

- Data Quality
- MQA
- DCAT-AP
- Metrics

#### Properties

- [OpenAPI](openapi/eu-open-data-portal-mqa-metrics-cache-openapi.yaml)
- [APIReference](https://data.europa.eu/api/mqa/cache/)
- [Documentation](https://dataeuropa.gitlab.io/data-provider-manual/api-documentation/)
- [Overlay](overlays/eu-open-data-portal-mqa-metrics-cache-overlay.yaml)
- [SourceCode](https://gitlab.com/dataeuropa/mqa/cache)

### EU Open Data Portal SHACL Validation API

A public RDF validation service that runs a submitted DCAT-AP graph against the official DCAT-AP SHACL shapes and returns a SHACL validation report. Supports the DCAT-AP 2.x and 3.x shape models plus customised runs that add range, recommended-field and controlled-vocabulary checks. Unauthenticated, single POST operation.

- **Human URL:** [https://data.europa.eu/api/mqa/shacl/](https://data.europa.eu/api/mqa/shacl/)
- **Base URL:** `https://data.europa.eu/api/mqa/shacl`

#### Tags

- Validation
- SHACL
- DCAT-AP
- RDF

#### Properties

- [OpenAPI](openapi/eu-open-data-portal-mqa-shacl-openapi.yaml)
- [APIReference](https://data.europa.eu/api/mqa/shacl/)
- [Documentation](https://dataeuropa.gitlab.io/data-provider-manual/api-documentation/)
- [Overlay](overlays/eu-open-data-portal-mqa-shacl-overlay.yaml)
- [SourceCode](https://gitlab.com/dataeuropa/mqa/validating-shacl)

### EU Open Data Portal MQA Metrics Reporter API

The MQA metrics reporter renders catalogue quality reports for data.europa.eu in a requested language and format, and triggers report generation. Public read operations; the spec ships with an unresolved ${project.version} placeholder in info.version.

- **Human URL:** [https://data.europa.eu/api/mqa/reporter/](https://data.europa.eu/api/mqa/reporter/)
- **Base URL:** `https://data.europa.eu/api/mqa/reporter`

#### Tags

- Data Quality
- MQA
- Reporting

#### Properties

- [OpenAPI](openapi/eu-open-data-portal-mqa-reporter-openapi.yaml)
- [APIReference](https://data.europa.eu/api/mqa/reporter/)
- [Documentation](https://dataeuropa.gitlab.io/data-provider-manual/api-documentation/)
- [Overlay](overlays/eu-open-data-portal-mqa-reporter-overlay.yaml)
- [SourceCode](https://gitlab.com/dataeuropa/mqa/reporter)

### EU Open Data Portal Statistics API

The hub statistics service exposes portal-wide counts over time — datasets per category, per catalogue, per country, per format and per licence — behind a Swagger 2.0 contract served from a Flask/flask-apispec application. Read operations are public; the maintenance reset operation requires an X-API-KEY header.

- **Human URL:** [https://data.europa.eu/api/hub/statistics/](https://data.europa.eu/api/hub/statistics/)
- **Base URL:** `https://data.europa.eu/api/hub/statistics`

#### Tags

- Statistics
- Open Data
- Reporting

#### Properties

- [Swagger](openapi/eu-open-data-portal-hub-statistics-swagger.json)
- [APIReference](https://data.europa.eu/api/hub/statistics/)
- [Documentation](https://dataeuropa.gitlab.io/data-provider-manual/api-documentation/)
- [SourceCode](https://gitlab.com/dataeuropa/hub/statistics)

### EU Open Data Portal SPARQL API

The OpenLink Virtuoso SPARQL endpoint for data.europa.eu. Every harvested dataset is stored in its own named graph alongside DCAT-AP controlled vocabularies, NUTS codes and MQA quality measurements, and can be queried with SPARQL 1.1 returning HTML, XML, JSON, Turtle, CSV, TSV and other RDF serialisations. Public and unauthenticated; there is no OpenAPI for this surface because the contract is the SPARQL 1.1 protocol itself.

- **Human URL:** [https://data.europa.eu/sparql](https://data.europa.eu/sparql)
- **Base URL:** `https://data.europa.eu/sparql`

#### Tags

- SPARQL
- Linked Data
- RDF
- Open Data

#### Properties

- [APIReference](https://data.europa.eu/sparql)
- [Documentation](https://dataeuropa.gitlab.io/data-provider-manual/how-to-search/sparql/)
- [GettingStarted](https://data.europa.eu/en/about/sparql)

## Common Properties

- [Portal](https://data.europa.eu/)
- [DeveloperPortal](https://dataeuropa.gitlab.io/data-provider-manual/api-documentation/)
- [Documentation](https://dataeuropa.gitlab.io/data-provider-manual/)
- [APIReference](https://data.europa.eu/api/hub/search/)
- [GettingStarted](https://dataeuropa.gitlab.io/data-provider-manual/api-documentation/)
- [Support](https://data.europa.eu/en/contact-us)
- [HelpCenter](https://data.europa.eu/en/faq)
- [Blog](https://data.europa.eu/en/news-events/news)
- [TermsOfService](https://data.europa.eu/en/legal-notice)
- [PrivacyPolicy](https://data.europa.eu/en/legal-notice)
- [SourceCode](https://gitlab.com/dataeuropa)
- [LinkedIn](https://www.linkedin.com/company/publications-office-of-the-european-union)
- [AgenticAccess](agentic-access/eu-open-data-portal-agentic-access.yml)
- [Authentication](authentication/eu-open-data-portal-authentication.yml)
- [Conventions](conventions/eu-open-data-portal-conventions.yml)
- [ErrorCatalog](errors/eu-open-data-portal-problem-types.yml)
- [Lifecycle](lifecycle/eu-open-data-portal-lifecycle.yml)
- [ChangeLog](changelog/eu-open-data-portal-changelog.yml)
- [Conformance](conformance/eu-open-data-portal-conformance.yml)
- [DataModel](data-model/eu-open-data-portal-data-model.yml)
- [Packages](packages/eu-open-data-portal-packages.yml)
- [Vocabulary](vocabulary/eu-open-data-portal-vocabularies.yml)
- [AgentSkill](skills/_index.yml)
- [LLMsTxt](llms/eu-open-data-portal-llms.txt)
- [Plans](plans/eu-open-data-portal-plans-pricing.yml)
- [RateLimits](rate-limits/eu-open-data-portal-rate-limits.yml)
- [DomainSecurity](security/eu-open-data-portal-domain-security.yml)
- [JSONSchema](json-schema/eu-open-data-portal-dataset-schema.json)
- [JSONLDContext](json-ld/eu-open-data-portal-context.jsonld)
- [FinOps](finops/eu-open-data-portal-finops.yml)
- [Rules](rules/eu-open-data-portal-jsonschema-spectral-rules.yml)

