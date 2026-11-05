# Part 1 - Python Foundations

## Data source
Program-provided files that mirror the public "Trending YouTube Video Statistics" dataset (Kaggle): USvideos.csv, GBvideos.csv, INvideos.csv and categories.csv. The files are in the `data/` folder. 46,230 records are loaded in total (US 16,080, GB 15,075, IN 15,075).

## How to install and run
1. Open `part1_python_foundations.ipynb` in Google Colab.
2. Install dependency: `pip install pandas` (already installed in Colab).
3. Click Runtime > Restart session and run all. The first cell clones this repository branch to read the `data/` files.

## Cleaning rules
- Bad or blank `views`: the record is dropped (none were dropped here).
- Bad or blank `likes`, `dislikes`, `comment_count`: replaced with 0, so no other data in the record is lost. Failures found: likes 12, comment_count 36.
- `trending_date` (format yy.dd.mm) and `publish_time` are converted to real dates. No failures.
- `comments_disabled` and `ratings_disabled` are converted to booleans.

## Classification thresholds
| Setting | Value |
|---|---|
| Viral Hit views | 2,000,000 or more (about the 90th percentile) |
| Low Engagement views | below 130,000 (about the 25th percentile) |
| Minimum like ratio | 0.90 |
Records with ratings disabled, or with likes + dislikes equal to 0, are labelled Unrated, so there is no division by zero.

## Design decisions
Records are kept as a list of dictionaries; key fields are also stored as tuples; sets compare videos across countries; dictionaries count channels and categories. The reasons are explained in the notebook.
