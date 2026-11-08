# Part 3 - Visualization, EDA and Business Thinking

## Data source
Program-provided files that mirror the public "Trending YouTube Video Statistics" dataset (Kaggle): USvideos.csv, GBvideos.csv, INvideos.csv and categories.csv, in the `data/` folder. 46,230 rows are loaded (US 16,080, GB 15,075, IN 15,075).

## How to install and run
1. Open `part3_visualization_eda.ipynb` in Google Colab.
2. Dependencies: `pip install -r requirements.txt` (numpy, pandas, matplotlib, plotly; all already installed in Colab).
3. Click Runtime > Restart session and run all. The first cell clones this repository branch to read the files in `data/`.

## Where everything is
The notebook is organised in numbered sections with Markdown cells under each chart. Every required written interpretation is in the notebook:
1. Profile the data (shape, data types, missing-value percentages)
2. Cleaning and category names
3. Five Matplotlib charts (category bar chart, log-views histogram, views vs likes scatter, trending records per day line chart, views by category box plot)
4. Interpretation of each chart (2-4 sentences plus why that chart type fits)
5. Two Plotly interactive charts (scatter coloured by category with title on hover, average views per category by country)
6. Distributions and outliers
7. Correlation heatmap
8. Funnel analysis
9. Retention analysis and curve
10. Cohort view
11. Content strategy briefing

## Profile and cleaning
Missing values: likes 12 (0.03%), comment_count 36 (0.08%), description 1,624 (3.51%).
Cleaning: 230 duplicates removed (same video_id, trending_date and country); 92 removed/errored videos dropped; blank likes and comments filled with 0; blank descriptions with an empty string; dates converted to datetimes; category names attached with a left merge (no rows lost). 45,908 records remain.

## Distributions
Views: mean 1,180,232 > median 318,570 > mode 16,000, so right-skewed. 5,073 IQR outliers (11.1%).
Likes: mean 45,861 > median 10,206 > mode 0, so right-skewed. 5,255 IQR outliers (11.4%).
Decision: outliers are kept, because they are the genuinely viral videos this analysis is about.

## Correlation
The two strongest pairs are views and likes (0.921) and views and comment_count (0.916). Correlation does not prove that likes cause views; both follow audience size.

## Funnel (unique videos)
| Stage | Videos | Conversion from previous stage |
|---|---|---|
| 1. All videos that ever trended | 14,688 | - |
| 2. Above the median peak views | 7,344 | 50.0% |
| 3. Above the 90th percentile of peak views | 1,469 | 20.0% |
| 4. 1,000+ comments (within stage 3) | 1,440 | 98.0% |
The largest real drop-off is from stage 2 to stage 3 (20.0%): reaching very high view counts is rare.

## Retention (day 1 = first trending day)
| Day | All | US | GB | IN | Music | Entertainment | News & Politics |
|---|---|---|---|---|---|---|---|
| Day 2 | 62.8% | 64.8% | 68.8% | 56.8% | 79.8% | 69.9% | 40.4% |
| Day 3 | 41.6% | 43.5% | 49.1% | 34.7% | 64.8% | 50.7% | 16.1% |
| Day 5 | 19.2% | 20.1% | 25.8% | 13.7% | 42.8% | 26.3% | 3.7% |
| Day 7 | 9.7% | 10.8% | 14.2% | 5.6% | 28.8% | 13.2% | 0.9% |

## Cohorts
Weekly cohorts from 2017-11-13 to 2018-01-15 look alike (about 1,300 videos, lifespan 3.0 to 3.2 days). The last two cohorts look lower, but this is explained by the fixed end of the data window and the small last cohort (253 videos).

## Content strategy briefing
Entertainment (26.7% of trending records) and Music (22.4%) together make up about half of everything on the trending list. The median video trends 3 days after publishing, and 55.3% trend within 3 days. Category separates videos that stay from those that vanish: 28.8% of Music videos are still trending on day 7, against 0.9% of News & Politics. GB has the highest average views (about 1.58 million) and the best retention (14.2% on day 7); IN has the lowest average views (about 0.95 million) and the shortest retention (5.6%). Only 20% of above-median videos pass the 90th percentile of peak views. Limitation: the data covers only 14 November 2017 to 1 February 2018 and only videos that did trend, so lifespans near the end of the window are cut short and we cannot say what stops a video from trending.
