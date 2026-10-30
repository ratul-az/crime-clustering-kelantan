# Dataset Information

## Required file

The notebook loads:

`Kelantan_Crime_Statistic.csv`

## Dataset availability

The CSV file was not included with the uploaded notebook. The notebook does not identify a direct source URL, publisher or dataset licence. This package therefore does not bundle a dataset or claim an unverified source.

Before sharing the CSV publicly, confirm its source, permitted use and redistribution licence.

## Fields referenced by the notebook

The notebook references these fields:
- `date` — parsed as a datetime value; a `year` feature is extracted.
- `state` — dropped during the cleaning section.
- `district` — used to aggregate crime records and identify districts.
- `category` — crime category; used as pivot-table columns.
- `crimes` — numeric crime count, aggregated by district and category.

The K-Means workflow creates a district-by-category matrix by summing `crimes` and filling missing district/category combinations with zero. Hierarchical clustering also uses district-level features. Review the notebook's data-preparation cells for the exact matrix construction.

## Setup

### Google Colab

Upload `Kelantan_Crime_Statistic.csv` to the session before running the notebook.

### Local Jupyter

Place the CSV in the notebook's working directory, or update each `pd.read_csv(...)` path to point to its location.

## Data handling

Do not include confidential, restricted or personally identifiable records in a public repository. Use only data you are authorised to access and redistribute.
