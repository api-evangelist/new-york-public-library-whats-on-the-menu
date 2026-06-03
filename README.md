# New York Public Library What's On The Menu (new-york-public-library-whats-on-the-menu)

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
