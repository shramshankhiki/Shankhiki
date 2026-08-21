# Shram Sankhyiki: PLFS production data integration

This build replaces the illustrative PLFS values in the portal with the uploaded PLFS dataset.

## Data source

`data/PLFS.txt` is the uploaded tab-separated PLFS dataset. The file contains the following fields:

- Source
- Indicator
- Type of Estimate
- Year
- Frequency
- State
- Gender
- Sector
- Age-group
- Value

The portal reads the file dynamically in the browser. Filter choices on `indicator.html` are generated from the values actually present in the dataset.

## Files

- `index.html` - portal landing page. Key indicator cards are populated from the latest annual PLFS observations for India, Person, Total, age 15 & above, PS+SS.
- `indicator.html` - data explorer. Filtering, table, charts and downloads operate on actual PLFS observations.
- `data/PLFS.txt` - production PLFS data file used by the web pages.

## Important

The pages must be served through HTTP/HTTPS. Do not open `index.html` or `indicator.html` directly with `file://`, because browsers normally block `fetch()` requests to local files.

For local testing:

```bash
python -m http.server 8000
```

Then open:

`http://localhost:8000/index.html`

For GitHub Pages, keep `data/PLFS.txt` in the repository and deploy the repository as a static site.

## Current source status

PLFS is connected to the production data file. EPFO and ESIC remain visible as source options but are intentionally not populated with fabricated values. They should be enabled only after their production datasets are supplied.

## Data model

The observation file remains in long/tidy form. The frontend treats each row as one statistical observation identified by the combination of source, indicator, estimate type, year, frequency, state, gender, sector and age group.
