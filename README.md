# How to Price Art

> They do not teach you this at art school. Everyone is too embarrassed to talk about how much to charge for art.

**[Open the calculator](https://grantaj.github.io/how-to-price-art/)**

The [main website](https://grantaj.github.io/how-to-price-art/) is an intentionally simple **artwork asking-price guide**. Enter career stage, width, and height to get a suggested Australian gallery asking price and a comparison range. It reads the checked-in gallery price CSV; it does not ask the artist to estimate demand, studio time, or elasticity.

No build is necessary; GitHub Pages serves `index.html` from `main`.

### Main price calculator

For the chosen career stage, select gallery records with researched stage assignments (excluding `unverified`). Convert each observed asking price to the proposed artwork area using

```text
size_adjusted_price = observed_asking_price * (new_area / observed_area)^0.55
```

Take the **median size-adjusted price for each artist**, then take the **median across artists**. This gives each artist equal weight even when one has many listed artworks. The displayed price is rounded to a consumer-friendly increment. The displayed range is the 25th–75th percentile of artist-level estimates, not a statistical confidence interval. The size exponent 0.55 is a simplifying assumption; it is *not* a fitted estimate from the sample.

Only advertised gallery asking prices are used on the homepage; the app never treats a sold label as a verified sale amount. As of this snapshot, the early-career subset has just **3 identifiable artists**, so its recommended price is especially uncertain. The 116 gallery observations are selected examples and not a representative survey. Gallery listings can include commissions, framing and negotiation margins. The result is a starting point to discuss with your gallery, not an authoritative valuation or expected real sale price.


## Open, anonymised data

Every plotted market anchor is calculated from checked-in CSVs:

| File | Contents |
| --- | --- |
| [`data/auction_comparables.csv`](data/auction_comparables.csv) | 48 sampled auction lots from two Lawsons catalogues, including sold and passed works |
| [`data/gallery_floorsheets.csv`](data/gallery_floorsheets.csv) | 116 sampled artworks and advertised prices from four gallery listings |
| [`data/stage_evidence.csv`](data/stage_evidence.csv) | Biography source URL, stage and confidence for **93** individually annotated price observations |
| [`data/sources.csv`](data/sources.csv) | Date, source catalogue, price semantics and source URL for each anonymised group |

The price/size CSVs omit artist names, titles and original lot numbers. The `artist_key` column pseudonymously groups repeat observations of the same identified artist across sources; five ambiguous gallery observations have an empty key rather than a guessed identity. Their `row_id` keys link to stage evidence where available. Because publicly available source catalogues and biography URLs are also provided, this is **pseudonymisation, not irreversible anonymisation**: distinctive dimensions and prices can be matched to original listings. Source links are intentionally retained for auditability. No personal or private art sales records are included.

### Price basis: **do not conflate asking and sale prices**

- **Auction:** `price_basis=reported_sale`, `status=reported_sold` means a reported auction transaction. No systematic harmonisation of buyer's premium or GST; `passed` lots have a blank price, not zero.
- **Gallery:** `price_basis=advertised_asking` indicates a public *asking price*, not the final cash received by an artist. `sold_label` means the site marks the work sold, but does **not** reveal a negotiated price or when the work sold. `listed` means a displayed asking price, not confirmed unsold inventory.
- The source-filter dropdown always keeps these populations separate, because secondary-market sales do not reliably predict primary-market retail prices.

### Researched career stage

Career stage is researched from each artist's publicly documented CV, exhibitions, gallery representation, institutional collection, grants and prizes. Classifications use [NAVA's creative career-stage guidelines](https://code.visualarts.net.au/payment-rates/how-to-use-payment-standards/creative-career-stages):

- `early`: early professional practice, recent emergence or explicit gallery characterisation.
- `mid`: established independent practice over multiple years, with state or national industry recognition, but no strong evidence of national/international prominence on the scale NAVA describes as established.
- `established`: substantial professional body of work and sustained national or international acclaim.
- `unverified`: no sufficiently clear supporting artist biography was found or a work-to-artist match could not be audited.

NAVA's criteria are **qualitative**, not based on age or prices. `stage_confidence` in the price files and `stage_evidence.csv` record our degree of confidence and links for each row. Stage assignments are **researcher judgments**, not official certifications or a universal rule. For example, an artist having practiced for twenty years does not automatically make them established, and a successful selling exhibition is not proof of the artist's lifetime market status.

At this snapshot, **93 of 164 rows have a researched career-stage assignment**; the remaining 71 remain `unverified`. Repeated works by a single artist are highly correlated and do not amount to 93 independent artists. The sampled works represent **75 identifiable distinct artist keys** (not 75 independent random draws from the Australian artist population).

## Data collection and limitations

The current records are **hand-selected convenience samples**, not exhaustive gallery catalogues, cross-sectional random samples or a representative Australian art market. A Side Gallery sample contains 28 works by **one artist**; repeated artists, gallery selection, the distinct auction resale mechanism and price/medium confounding all matter. A gallery's publicly marked `sold` works do not identify actual transaction values or time at risk. Frame dimensions and work dimensions may differ, and medium classification is intentionally approximate. Mutable stockroom date stamps are snapshot *access dates*, not dates of sale.

A next version should ingest a dated, full-catalogue primary-market dataset, ideally with actual sold prices, listing durations, buyer enquiries, offer prices, commissions, artist-specific pseudonymous identifiers and unsold exposures. That information would be needed before any defensible sales-demand model could be developed.

## References

- [NAVA: Career stage criteria](https://code.visualarts.net.au/payment-rates/how-to-use-payment-standards/creative-career-stages)
- [NAVA: Commercial gallery representation](https://code.visualarts.net.au/selling-and-marketing/commercial-galleries-and-representation/detailed-discussion)
- [Creative Workplaces: Working out fees and pricing](https://creativeworkplaces.gov.au/contracts-and-payment/independent-contractors-artists-and-arts-workers/working-out-fees-payment-and)
- [Original data source URLs, with source IDs](data/sources.csv)

The application is dependency-free and does its calculations locally. The open data files are served by GitHub Pages.
