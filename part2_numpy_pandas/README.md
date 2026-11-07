# Part 2 - NumPy and Pandas

## Data source
Program-provided files that mirror the public "Trending YouTube Video Statistics" dataset (Kaggle): USvideos.csv, GBvideos.csv, INvideos.csv and categories.csv, in the `data/` folder. 46,230 rows are loaded (US 16,080, GB 15,075, IN 15,075) and 46,000 remain after removing duplicates.

## How to install and run
1. Open `part2_numpy_pandas.ipynb` in Google Colab.
2. Dependencies: `pip install numpy pandas` (both already installed in Colab).
3. Click Runtime > Restart session and run all. The first cell clones this repository branch to read the files in `data/`. No other network access is needed.

## Engagement score weights
engagement = 0.2 x views_norm + 0.4 x likes_norm + 0.4 x comments_norm (each normalised with min-max to 0..1).
- Views (0.2): show reach, but many viewers do not engage, so the smallest weight.
- Likes (0.4): an active choice by the viewer.
- Comments (0.4): take the most effort, so the strongest sign of engagement.
The weights add up to 1, so the score stays between 0 and 1.

## Data-quality issues and decisions
| Issue | Count | Handling |
|---|---|---|
| Duplicate rows (same video_id, trending_date and country) | 230 | Removed |
| Missing likes | 12 (0.03%) | Filled with 0 |
| Missing comment_count | 36 (0.08%) | Filled with 0 |
| Missing description | 1,615 (3.51%) | Filled with empty string |
| Removed or errored videos | 92 | Kept and flagged |
| Dates stored as text | all rows | Converted with pd.to_datetime |
| "Published after trending" | 6,164 | Checked: all were published on the same day as they trended, so no real error |

## Missing values and duplicates
A duplicate is the same video_id on the same trending_date in the same country. A video can legitimately trend on many days and in many countries, so those are not duplicates. Blank likes and comment counts were filled with 0 because the numbers are tiny and a blank most likely means none were recorded.

## Category merge
A left merge on category_id. The row count stayed at 46,000 and no records were lost.
