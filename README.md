# CFB Model — site

Static front end for the CFB prediction model. No build step: it reads JSON from
`data/` at runtime, so a refresh of the data is a deploy.

## What is here and what is not

This repo is public. It carries **outputs** — ratings, picks, schedule — and no
model code. The exporter (`58_export_site.R`, in the private model repo) enforces
that: it refuses to write, and deletes, any file containing a fitted coefficient
or correction parameter.

Phase B will add the matchup calculator by shipping per-team component values
**already converted to points**, so the browser can re-weight them without ever
seeing a coefficient. Shipping coefficients and multiplying in JS would publish
the model — that shortcut is deliberately not taken.

## Data files

| file | contents |
|---|---|
| `data/ratings.json` | power ratings for the current week |
| `data/bestbets.json` | free plays, read from the published card |
| `data/schedule.json` | upcoming games |
| `data/meta.json` | season, week, published accuracy figures |

Best Bets are read from the card that was published to the ledger, not
recomputed here, so the site and the public record cannot disagree.

The Track Record view embeds <https://wagne6tc.github.io/cfb-ledger/>, which is
the hash-chained ledger of every pick.
