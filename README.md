# Data Transformation Examples

![Tests](https://github.com/YOUR-USERNAME/data-transformation-examples/actions/workflows/tests.yml/badge.svg)
![Python](https://img.shields.io/badge/python-3.10%2B-blue)
![License](https://img.shields.io/badge/license-MIT-green)

A small, well-tested collection of **pandas data transformation examples**: cleaning, feature engineering,
merging, aggregation and reshaping, applied to a deliberately messy sales dataset.

## Table of Contents
- [What You'll Find Here](#what-youll-find-here)
- [Repository Structure](#repository-structure)
- [Getting Started](#getting-started)
- [Usage](#usage)
- [Transformations Covered](#transformations-covered)
- [Example Output](#example-output)
- [Testing](#testing)
- [Author](#author)
- [License](#license)

## What You'll Find Here
- Reusable, documented transformation functions in `src/transformations/`
- Two walkthrough Jupyter notebooks with outputs
- A one-command pipeline from raw CSV to processed data
- Unit tests and a GitHub Actions workflow (CI)

## Repository Structure
```
data-transformation-examples/
├── data/
│   ├── raw/                  # Messy input CSVs (sales, customers)
│   └── processed/            # Pipeline outputs (git-ignored)
├── notebooks/
│   ├── 01_data_cleaning.ipynb
│   └── 02_feature_engineering_and_reshaping.ipynb
├── src/transformations/      # cleaning, feature_engineering, aggregation, reshaping, merging
├── scripts/run_pipeline.py   # End-to-end pipeline
├── tests/                    # pytest unit tests
├── docs/transformations_guide.md
├── .github/workflows/tests.yml
├── requirements.txt
└── LICENSE
```

## Getting Started
```bash
git clone https://github.com/YOUR-USERNAME/data-transformation-examples.git
cd data-transformation-examples
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt
```

## Usage
**Run the pipeline**
```bash
python scripts/run_pipeline.py
```
Outputs are written to `data/processed/`.

**Explore the notebooks**
```bash
jupyter notebook notebooks/
```

**Use the functions in your own code**
```python
import pandas as pd
from transformations import standardize_columns, clean_text_columns, add_revenue

df = (pd.read_csv("data/raw/sales.csv")
        .pipe(standardize_columns)
        .pipe(clean_text_columns, ["product", "region"])
        .pipe(add_revenue))
```

## Transformations Covered
| Category | Functions |
|---|---|
| Cleaning | `standardize_columns`, `clean_text_columns`, `drop_duplicate_rows`, `parse_dates`, `fill_missing`, `remove_outliers_iqr` |
| Feature engineering | `add_revenue`, `add_date_parts`, `add_order_size_bucket` |
| Aggregation | `monthly_revenue`, `revenue_by` |
| Reshaping | `pivot_revenue`, `melt_to_long` |
| Merging | `enrich_with_customers` |

Full details: [docs/transformations_guide.md](docs/transformations_guide.md)

## Example Output
Before (raw):

| product | region | unit_price |
|---|---|---|
| `"  laptop "` | `north` | 950.00 |
| `Pen Set` | `East` | *(missing)* |

After (clean): `Laptop`, `North`, 950.00, with missing prices imputed and `revenue`, `quarter`, `order_size` added.

## Testing
```bash
pytest -v
```

## Author
**YOUR NAME** - [GitHub](https://github.com/YOUR-USERNAME)

## License
Released under the [MIT License](LICENSE).
