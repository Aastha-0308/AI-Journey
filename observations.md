# Anime Analysis

# Day 1 Findings

## Dataset Overview
- Loaded and explored the anime dataset using Pandas.
- Examined the available columns and identified key attributes such as score, members, genre, studio, source, and type.

## Genre Analysis
- Initially, Hentai appeared to be the most common genre.
- Further investigation revealed that the genre column contains multiple genres in a single row, making direct counting misleading.
- After splitting genre values, Comedy, Action, and Fantasy emerged among the most common genres.

## Popular Anime
- Analyzed anime with the highest member counts.
- Popular titles such as Attack on Titan and other well-known series appeared near the top of the rankings.
- Popularity rankings aligned with expectations from the anime community.

## Learning Outcomes
- Learned how to use:
  - `read_csv()`
  - `head()`
  - `value_counts()`
  - `sort_values()`
  - dictionaries
  - lambda functions
- Gained experience exploring a real-world dataset and validating results instead of accepting them blindly.



# Day 2 Findings

## Popularity vs Rating
- Created a scatter plot to analyze the relationship between anime popularity and ratings.
- Calculated a correlation coefficient of approximately 0.31 between members and score.
- Found a moderate positive relationship, suggesting that popular anime tend to have higher scores, but popularity alone does not determine quality.

## Members vs Favorites
- Calculated the correlation between members and favorites.
- Obtained a strong positive correlation of approximately 0.78.
- This suggests that anime with larger audiences generally accumulate more favorites.

## Studio Analysis
- Discovered that many anime are produced by multiple studios.
- Split studio names and used `explode()` to create separate entries for each studio.
- This allowed studio-level analysis using average scores.

## Sample Size Bias
- Initial studio rankings were dominated by studios with only one or two anime.
- Added anime counts for each studio and filtered out very small sample sizes.
- After filtering, rankings became more meaningful and highlighted established studios such as Bones, A-1 Pictures, and Studio Ghibli.

## Learning Outcomes
- Learned:
  - `groupby()`
  - `agg()`
  - `corr()`
  - `explode()`
  - scatter plots
  - data reshaping
- Understood that data often requires cleaning and restructuring before meaningful analysis can be performed.


# Day 3 Findings - Source Material Analysis

## Source Distribution

The most common source categories in the dataset were:

* Unknown (4210 anime)
* Original (3368 anime)
* Manga (3120 anime)

This indicates that Original and Manga adaptations make up a significant portion of the dataset.

---

## Average Score by Source

Initial analysis showed that Light Novel adaptations had the highest average score among major source categories.

| Source      | Average Score |
| ----------- | ------------- |
| Light Novel | 6.80          |
| Manga       | 6.76          |
| Original    | 5.74          |

This suggested that anime adapted from Light Novels and Manga generally received higher ratings than Original anime.

---

## Importance of Sample Size

To avoid misleading results from categories with very few anime, only source categories with at least 100 anime were considered for comparison.

This reduced the impact of unusually high or low averages caused by small sample sizes.

---

## Data Quality Investigation

During analysis, several anime entries were found with:

* `score = 0`
* `scored_by = 0`

These entries were not poorly rated anime. Instead, they appeared to represent anime that had not received any ratings.

Example:

```text
score = 0
scored_by = 0
```

Because these entries were included in average calculations, they lowered the mean score of some source categories.

---

## Mean vs Median Comparison

The median score for several source categories was higher than the mean score.

Example:

| Source   | Mean | Median |
| -------- | ---- | ------ |
| Original | 5.74 | 5.97   |

This indicated that unusually low values (mainly score = 0 entries) were pulling averages downward.

---

## Recalculating After Cleaning

A cleaned dataset was created by removing entries with:

```python
score > 0
```

After recalculating averages:

| Source      | Cleaned Average Score |
| ----------- | --------------------- |
| Light Novel | 7.21                  |
| Manga       | 6.98                  |
| Original    | 5.90                  |

The averages increased and moved closer to their median values.

---

## Key Takeaways

* Light Novel adaptations achieved the highest average ratings among major source categories.
* Manga adaptations also performed strongly and consistently.
* Original anime showed lower average ratings despite having a large sample size.
* Entries with `score = 0` represented missing rating information rather than poor ratings.
* Mean values can be affected by missing or extreme values, making median an important metric for comparison.
* Data cleaning can significantly change analytical conclusions and should be performed before drawing final insights.
