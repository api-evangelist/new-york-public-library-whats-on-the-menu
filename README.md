# New York Public Library What's On The Menu (new-york-public-library-whats-on-the-menu)

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
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

The New York Public Library's What's On The Menu project is a crowdsourced digital collection of over 17,000 historical restaurant menus from the New York City area dating back to the 1850s, with more than 1.3 million transcribed dishes. The dataset is modeled as four related entities (Menu, MenuPage, MenuItem, Dish) and distributed as bulk CSV downloads. A companion HTTP API formerly provided programmatic access to menus, pages, and dishes; the live site and api.menus.nypl.org were retired in January 2025, but the crowdsourced dataset remains available as a gzip archive on Amazon S3 alongside a data dictionary.

**URL:** [Visit APIs.json URL](https://raw.githubusercontent.com/api-evangelist/new-york-public-library-whats-on-the-menu/refs/heads/main/apis.yml)

## Scope

- **Type:** Contract
- **Position:** Consuming
- **Access:** 3rd-Party

## Tags

- Libraries
- Menus
- Restaurants
- History
- Open Data
- Food
- Datasets
- Cultural Heritage

## Timestamps

- **Created:** 2024-11-14
- **Modified:** 2026-06-03

## Data Model

The dataset is four related tables. Foreign keys join them into a Menu → MenuPage → MenuItem → Dish hierarchy.

| Entity | Description | Joins to |
|---|---|---|
| **Menu** | One digitized physical menu object (restaurant, hotel, banquet, steamship, etc.) | root |
| **MenuPage** | One scanned page of a menu | `menu_id` → Menu.id |
| **MenuItem** | One transcribed dish-on-page line item, with price and (x, y) position | `menu_page_id` → MenuPage.id, `dish_id` → Dish.id |
| **Dish** | One normalized/deduplicated dish with appearance counts and price range | referenced by MenuItem.dish_id |

## Artifacts

- **OpenAPI** (`openapi/`) — documents the historical `api.menus.nypl.org` HTTP contract (retired Jan 2025), retained for reference.
- **JSON Schema** (`json-schema/`) — one schema per data entity: Menu, MenuPage, MenuItem, Dish.
- **JSON Structure** (`json-structure/`) — single dataset structure describing all four tables and their relationships.
- **JSON-LD** (`json-ld/`) — linked-data context aligning fields to schema.org and Dublin Core.
- **Examples** (`examples/`) — representative record for each entity.
- **Vocabulary** (`vocabulary/`) — domain taxonomy, controlled values, and semantic alignments.
- **Plans / Rate Limits / FinOps** — capture the historical token-based access policy (5,000 requests/day, 2 requests/second) of the retired API.

## APIs

### NYPL What's On The Menu API

The NYPL What's On The Menu API exposed the full Menus dataset for programmatic exploration. Endpoints covered menus and their pages, dishes, search across both, and filtering by year, status, and other properties. Responses were JSON or XML, with token-based authentication, daily rate limits, and pagination headers. The live API at api.menus.nypl.org was retired in January 2025; the OpenAPI definition here documents the historical contract, and the four-table CSV dataset (Menu, MenuPage, MenuItem, Dish) remains downloadable from the Amazon S3 archive as the durable data interface.

**Human URL:** [http://nypl.github.io/menus-api/](http://nypl.github.io/menus-api/)

**Base URL:** `http://api.menus.nypl.org`

#### Tags

- Libraries
- Menus
- Restaurants
- History
- Open Data

#### Properties

- [Documentation](http://nypl.github.io/menus-api/)
- [OpenAPI](https://raw.githubusercontent.com/api-evangelist/new-york-public-library-whats-on-the-menu/refs/heads/main/openapi/new-york-public-library-whats-on-the-menu-openapi-original.yaml)
- [Project Site](https://www.nypl.org/research/support/whats-on-the-menu)
- [DataAPI (S3 bulk CSV export)](https://s3.amazonaws.com/menusdata.nypl.org/gzips/)
- [DataDictionary](http://curatingmenus.org/data_dictionary/)
- JSONSchema, JSONStructure, JSONLD, Vocabulary (see artifact folders)

#### Contact

- **FN:** NYPL Menus Project
- **Email:** menus@nypl.org

## Common Properties

- [GitHubOrganization](https://github.com/NYPL)
- [Website](https://www.nypl.org/research/support/whats-on-the-menu)
- [Documentation](http://nypl.github.io/menus-api/)
- [DataDictionary](http://curatingmenus.org/data_dictionary/)

## Maintainers

**FN:** Kin Lane

**Email:** kin@apievangelist.com
