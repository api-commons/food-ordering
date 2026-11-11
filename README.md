# Food Ordering

The common food-ordering vocabulary -- the restaurants and locations that cook, the menus they publish, the items and modifier groups on them and the orders placed against them -- distilled from the APIs that already exist. Delivery belongs to the shipping context. Part of [Schema Commons](https://github.com/api-commons/schema-commons),
published by the [API Commons](https://apicommons.org).

Built from the providers tagged Restaurant, Food Delivery, Online Ordering, Mobile Ordering, Ordering, Restaurant Technology, QSR in [APIs.io](https://apis.io) that
publish their own OpenAPI. Only harvested contracts count -- nothing API Evangelist
generated. Every number below is a count of providers.

## What the market already agrees on

<!-- commons:summary -->
| Concept | Expose it | Readable schema | Core properties (share) | Collection named |
| --- | ---: | ---: | --- | --- |
| restaurant | 34 | 34 | name 79%, id 59% | locations 14, stores 12, restaurants 8, location 4 |
| menu | 11 | 11 | name 73%, id 64% | menus 8, menu 7 |
| menu_item | 8 | 7 | name 86%, description 71% | items 5, menuitems 3, dishes 1 |
| food_order | 18 | 18 | restaurant_id 67%, items 56% | orders 14, order 6 |

Cohort: 77 providers with harvested OpenAPI, 35 crosswalks. Of the providers exposing a restaurant: 29% create, 88% list, 56% fetch, 21% update, 12% delete. Generated 2026-11-11 by build.py.
<!-- /commons:summary -->

Shares are of the providers with a readable resource schema for that concept. The
extended tier and the long tail of every concept are in [profile.yml](profile.yml).

## What the measurement shows

- A food order agrees only on the restaurant and its items -- aggregators (DoorDash, Just Eat), ordering platforms and kitchen systems each model the totals and the fulfilment type differently, the same divergence as orders in commerce.
- A restaurant agrees only on name and id; hours and address are carried by too few to share, because many APIs take the restaurant as given from their own onboarding.
- Modifier groups -- the min/max choice rules that make a menu orderable -- are almost never a resource of their own (2 providers); they live inside the menu item.

## Artifacts

- [openapi.yml](openapi.yml) -- OpenAPI 3.1 of the shared operations. No one serves it; it
  is the shape to map to. Lints clean against the
  [naming ruleset](https://github.com/api-commons/schema-commons/blob/main/ruleset/schema-commons-naming.yaml).
- [schema/](schema) -- JSON Schema 2020-12 per concept; each property carries
  `x-commons-tier`, `x-commons-share`, `x-commons-providers` and the spellings seen.
- [crosswalk/](crosswalk) -- one per provider, common name -> their name, with the harvested
  spec and operations each mapping was read from.
- [adopters.yml](adopters.yml) -- who exposes which concept, linked to their APIs.io page.
- [concepts.yml](concepts.yml) -- the only hand-written input: concepts, path segments and
  their qualifiers, aliases, reviewed exclusions, merged duplicates, and the decisions below.
- [census/](census) -- the cohort and the raw census the profile is built from.

## Decisions

These are calls, not measurements, recorded so they can be revisited as the method matures.

- Orders are `/food-orders`: `/orders` is commerce's (and trading's).
- A restaurant covers stores, locations, venues and outlets in this cohort.
- A menu item covers items and products beneath a menu, store or restaurant.
- Delivery is the shipping context's: a delivery job is a shipment.

## Rebuild

```bash
../schema-commons/scripts/run.sh .
```

## License

Artifacts CC BY-NC-SA 4.0 ([LICENSE](LICENSE)); code Apache 2.0 ([LICENSE-CODE](LICENSE-CODE)).
